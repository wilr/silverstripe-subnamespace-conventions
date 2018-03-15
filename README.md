# SilverStripe Sub-namespace Naming Conventions

An opinionated document of guidelines for sub-namspace conventions for SilverStripe projects and modules. 

This is not intended to capture every possible situation, but provide a guideline for most common situations.

---

## Table of Contents

1. [Background](#background)
1. [Outline](#outline)
1. [Notes](#notes)
1. [Contributing](#contributing)
1. [References](#references)

---

## <a name="background"></a> Background

### What are namespaces?

In the broadest definition namespaces are a way of encapsulating items. This can be seen as an abstract concept in many places. 

For example, in any operating system directories serve to group related files, and act as a namespace for the files within them. As a concrete example, the file foo.txt can exist in both directory /home/greg and in /home/other, but two copies of foo.txt cannot co-exist in the same directory. In addition, to access the foo.txt file outside of the /home/greg directory, we must prepend the directory name to the file name using the directory separator to get /home/greg/foo.txt. This same principle extends to namespaces in the programming world.

In the PHP world, namespaces are designed to solve two problems that authors of libraries and applications encounter when creating re-usable code elements such as classes or functions:

 * Name collisions between code you create, and internal PHP classes/ functions/constants or third-party classes/functions/constants.
 * Ability to alias (or shorten) Extra_Long_Names designed to alleviate the  first problem, improving readability of source code.

PHP Namespaces provide a way in which to group related classes, interfaces, functions and constants. Here is an example of namespace syntax in PHP:
	
```php
namespace MyOrg\PackageName; 
```

### What are sub-namespaces?

Much like directories and files, PHP namespaces also contain the ability to specify a hierarchy of namespace names. Thus, a namespace name can be defined with sub-levels:
	
```php
namespace MyOrg\PackageName\Folder\ClassName;
```

Code can be organised as deep in a hierarchy as needed.
	
```php
namespace MyOrg\PackageName\Folder\SubFolder\ClassName;
```

The only requirement for the namespace hierarchy is the subdirectory name MUST match the case of the sub-namespace name.

### Namespaces in SilverStripe

SilverStripe introduced first-class support for namespaces in the 4.0 release [1]. Extensive work has gone into namespacing the SilverStripe Core Framework and supported modules. Third-party developers have also been encouraged to namespace their plugins for SilverStripe 4.0 support.

Some examples of namespaced classes in SilverStripe 4:
	
```php
namespace SilverStripe\Core\Config\Config;
namespace SilverStripe\Forms\TextField;
```

At the current moment, there does not exist any conventions for organising sub-namespaces. Neither SilverStripe nor PHP-FIG define any standard sub-namespace folders or recommendations. This allows developers to make their own judgement for sub-namespaces. Over time, developers have settled into their own patterns of naming schemes including myself. 

This document outlines my own reasoning and approach to organising code.

## <a name="outline"></a> Outline

<big><pre>
package
└── src/
│	├── [Control/](#d-control)
│	│	└── Middleware/
│	├── [Forms/](#d-forms)
│	├── [Exceptions/](#d-exceptions)
│	├── [Extensions/](#d-extensions)
│	├── [Helpers/](#d-helpers)
│	├── [Model/](#d-model)
│	├── [Reports/](#d-reports)
│	├── [Services/](#d-services)
│	└── [Tasks/](#d-tasks)
└── tests/
</pre></big>

**Not all of the above folders will be required for each module.**

## <a name="notes"></a> Notes

### <a name="d-control"></a> :white_check_mark: Control
	
#### Description

SilverStripe Core differs, `silverstripe-framework` defines a `Control` folder and `silverstripe-cms` defines a `Controllers` folder. For purposes of a plugin or application code, `Control` is consistent with Model and reflects that this folder stores more than just `Controller` subclasses but anything to do with the HTTP lifecycle.

#### Example

```php
use ExampleOrg\ExampleProject\Control\TestController;
use ExampleOrg\ExampleProject\Control\Middleware\TestMiddleware;
```

#### Alternatives
	
* `Controllers` - Used in core for `silverstripe-cms` however `Control` makes more sense for things related to the HTTP lifecycle

---

### <a name="d-forms"></a> :white_check_mark: Forms

#### Description

SilverStripe Core and modules such as `CMS` use the `Forms` folder consistently.

#### Example

```php
use ExampleOrg\ExampleProject\Forms\BetterForm;
use ExampleOrg\ExampleProject\Forms\BetterTextField;
```

---

### <a name="d-exceptions"></a> ::white_check_mark: Exceptions

#### Description

Any subclasses of `Exception`.

---

### <a name="d-extensions"></a> :white_check_mark: Extensions

#### Description

Any subclasses of `Extension`.

---

### <a name="d-helpers"></a> :white_check_mark: Helpers

#### Description

A helper class tends used internally to provide some work that has no business domain meaning. For example, `ArrayHelper` might provide array utilities.

---

### <a name="d-model"></a> :white_check_mark: Model

#### Description

Any subclasses of `DataObject`

---

### <a name="d-reports"></a> :white_check_mark: Reports

#### Description

Any subclasses of `Report`

---

### <a name="d-services"></a> :white_check_mark: Services

#### Description

A Service class provides a way of a client to interact with some functionality in the application. This is typically public, with some business meaning. For example, a `PaymentService` interface might allow you to `pay` or `refund` an object. `Service` is common in modules such as `QueuedJobs`.
	
#### Alternatives

* `Service/` - Used in several core modules, plural recommended.

---

### <a name="d-tasks"></a> :white_check_mark: Tasks

#### Description

Any subclasses of `BuildTask` which are runnable by the developers.

#### Alternatives

* `Task/` - Plural recommended.

---

## <a name="contributing"></a>Contributing

Please feel free to raise any Pull Requests to clarify or request more information. Tweet me at [@wilr](https://www.twitter.com/wilr).

---

## <a name="references"></a> References

* [1] https://docs.silverstripe.org/en/4/changelogs/4.0.0/
* [2] http://php.net/manual/en/language.namespaces.rationale.php
* [3] http://php.net/manual/en/language.namespaces.nested.php
