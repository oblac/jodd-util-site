# BeanUtil

**BeanUtil** is a bean manipulation library that, in a nutshell, allows setting and reading bean properties. Several features make **BeanUtil** distinct:

* _fast_ (if not the fastest) bean manipulation utility
* works with both _attributes_ and _properties_
* nested properties can be arrays, lists and maps
* missing inner properties may be created
* may work silently (no exception is thrown)
* offers few populate methods
* has strong-type conversion library

### Flavors of BeanUtil

Before we jump into the details, let's quickly learn what types of `BeanUtil` exists. Implementations differ in the way how they threat private properties, if they throw exceptions and, finally, if they force the creation of missing inner properties (more details later). You can build your own implementation easily using `BeanUtilBean`, but these are already provided:

| Name                            | <p>Access<br>Privates</p> | <p>Throws</p><p>Exceptions</p> | <p>Force</p><p>Missing</p><p>Properties</p> |
| ------------------------------- | :-----------------------: | :----------------------------: | :-----------------------------------------: |
| `BeanUtil.pojo`                 |             no            |               yes              |                      no                     |
| `BeanUtil.declared`             |            yes            |               yes              |                      no                     |
| `BeanUtil.silent`               |             no            |               no               |                      no                     |
| `BeanUtil.forced`               |             no            |               yes              |                     yes                     |
| `BeanUtil.declaredSilent`       |            yes            |               no               |                      no                     |
| `BeanUtil.declaredForced`       |            yes            |               no               |                     yes                     |
| `BeanUtil.declaredForcedSilent` |            yes            |               no               |                     yes                     |
| `BeanUtil.forcedSilent`         |             no            |               no               |                     yes                     |

Let' jump into details!
