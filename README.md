ULID
====

[![Build Status](https://travis-ci.org/savonarola/ulid.svg?branch=master)](https://travis-ci.org/savonarola/ulid)

An OTP library for generating [Universally Unique Lexicographically Sortable Identifiers](https://github.com/alizain/ulid).

Build
-----

    $ make

Run tests
---------

    $ make test

Usage
-----

Add to `rebar`:

```erlang
{deps, [
    ...
    {ulid, ".*", {git, "git://github.com/savonarola/ulid", {branch, "master"}}},
    ...
]}.
```

Generate universally unique identifiers:

```erlang
1> ulid:generate().
<<"01ASXPR2ZJDBYGBJ795A00QQZB">>

2> ulid:generate_list().
"01ASXPR7TP4M3CVJEDH6A7E3K6"
```

First 10 characters are encoded timestamp with millisecond precision, so these identifiers (generally) ascend from millisecond to millisecond (but unordered whithin same millisecond). Using generator, one can generate monotonically increasing identifiers (i.e. identifiers generated by the same generator are **always** ascending, assuming time is monotonic):

```erlang
1> Gen0 = ulid:new(),
    {Gen1, Ulid1} = ulid:generate(Gen0),
    {Gen2, Ulid2} = ulid:generate(Gen1),
    {Gen3, Ulid3} = ulid:generate_list(Gen2),
    [Ulid1, Ulid2, Ulid3].
[<<"01ASXQ4J7ZT1XEZJFJFHE7G5R0">>,
 <<"01ASXQ4J7ZT1XEZJFJFHE7G5R1">>,
  "01ASXQ4J7ZT1XEZJFJFHE7G5R2"]
```


