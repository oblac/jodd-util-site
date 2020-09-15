# BeanUtil

**BeanUtil** is a bean manipulation library that, in a nutshell, allows setting and reading bean properties. Several features make **BeanUtil** distinct:

* _fast_ \(if not the fastest\) bean manipulation utility
* works with both _attributes_ and _properties_
* nested properties can be arrays, lists and maps
* missing inner properties may be created
* may work silently \(no exception is thrown\)
* offers few populate methods
* has strong-type conversion library

### Flavors of BeanUtil

Before we jump into the details, let's quickly learn what types of `BeanUtil` exists. Implementations differ in the way how they threat private properties, if they throw exceptions and, finally, if they force the creation of missing inner properties \(more details later\). You can build your own implementation easily using `BeanUtilBean`, but these are already provided:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:center">Access
        <br />Privates</th>
      <th style="text-align:center">
        <p>Throws</p>
        <p>Exceptions</p>
      </th>
      <th style="text-align:center">
        <p>Force</p>
        <p>Missing</p>
        <p>Properties</p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>BeanUtil.pojo</code>
      </td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">yes</td>
      <td style="text-align:center">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BeanUtil.declared</code>
      </td>
      <td style="text-align:center">yes</td>
      <td style="text-align:center">yes</td>
      <td style="text-align:center">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BeanUtil.silent</code>
      </td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BeanUtil.forced</code>
      </td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">yes</td>
      <td style="text-align:center">yes</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BeanUtil.declaredSilent</code>
      </td>
      <td style="text-align:center">yes</td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">no</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BeanUtil.declaredForced</code>
      </td>
      <td style="text-align:center">yes</td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">yes</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BeanUtil.declaredForcedSilent</code>
      </td>
      <td style="text-align:center">yes</td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">yes</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>BeanUtil.forcedSilent</code>
      </td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">no</td>
      <td style="text-align:center">yes</td>
    </tr>
  </tbody>
</table>

Let' jump into details!

