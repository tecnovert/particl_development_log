# Particl Development Log

## 2021-02-02

Merged latest Bitcoin code into Particl:
- avoid_reuse
    - Before the first received reused output would fall into the trusted balance category.
    - Now all reused outputs are marked reused

- validation.cpp
  - More functions moved to BlockManager class
  - Started a new particl namespace to contain Particl specific code and hopefully ease future merges as git has been mixing up the functions when automerging.

