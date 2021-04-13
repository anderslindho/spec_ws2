# fake spec

What utility do we use in the e3 team?
What utility does others use?
Are these two the same? And do they have the same reqs.?
  e.g. the e3 team should _always_ have a spec, but what about others?

A good goal is to have everyone use the same. This would require the tools being flexible to meet all use-cases.

---

Use build tool:

``` sh
$ build-e3 --specification 2021-q1.yaml --targets /epics /epics-dev /epics-test
```

``` sh
$ build-e3-module --name=asyn --tags=4.37.0,4.41.0
# it will try to build:
# - asyn 4.37.0+0 OK
# - asyn 4.41.0+0 OK
$ build-e3-module --name=asyn --tags=4.37.0+0,4.37.0+0
# it will try to build:
# - asyn 4.37.0+0 OK
# - asyn 4.37.0+1 OK
# :: this case is dangerous in case you e.g. run it twice
# OR
# - asyn 4.37.0+0 OK
# - asyn 4.37.0+0 exists NOK
```

## How to add a module

Scenario: Someone requests new build of fug

- we increase build no. in module (?); not really a build-number, more e3 digit (4th digit)
- we tag
- we add this to specification
- for CSLab/TN there is a listener that sees a commit to a spec. repo?

If something already exists (e.g. build no. not incremented) it doesn't do anything

### Second approach: incremental build

It only shows the set-difference (one-way diff)

modules:
- fug
  1.0.0
  1.0.0

diff -> 1.0.0
