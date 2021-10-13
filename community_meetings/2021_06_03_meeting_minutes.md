---
tags: SciPy
---


# 2021-06-03 What's up SciPy


- Time: 09:00 CEST
- Join via Zoom at https://zoom.us/j/93827717491?pwd=UGdkMzlnWEFjbDNQUmxpRkp6L0VLdz09 (or [dial-in](https://zoom.us/u/abpCzJ5DAn))
- [Previous community meetings](https://hackmd.io/@tupui/scipy-meetup/edit)


**Present:** 

Pamphile Roy, Tirth Patel, Bas Van Beek, Gemma

## Topics
[//]: # (The heart of SciPy, its community and code)

### Code Specifics
- State of type hinting

#### Static Typing

- Scalar-type typing: strictness vs corectness considerations
    - _e.g._ `arg: float` vs `arg: Union[float, np.floating, np.integer]`
    - The `numbers` ABCs are unfortunatelly useless here (xref [python/mypy#3186](https://github.com/python/mypy/issues/3186))
    - Exceptions: ABCs and outputs that the user is reasonably expected to narrow down (via `isinstance()` for example).

- Unsafe unions: avoid them; use `Any` or `@overload` instead
    - _i.e._ unions that are used as return-type: `def func() -> Union[TypeA, TypeB]: ...`
    - Type checkers demand that operations on union-types must be compatible with _all_ of its members, and will start throwing errors otherwise. 
      As these errors are generally false positives, all this accomplishes is forcing users to use excesive `isinstance()` checks, `typing.cast()` calls or adding `# type: ignore` comments (xref [python/mypy#1693](https://github.com/python/mypy/issues/1693)).
    - ```
      IntArray: Union[np.int64, np.ndarray]
      for i in IntArray:  # error: Item "signedinteger[_64Bit]" of ... has no attribute "__iter__"
           pass
      ```

We can start a PR in the doc about type hinting. These elements should be present.
      
---

[//]: # (Still need to decide what to do)
Please remember to archive this file and commit it to github.com/scipy/...
