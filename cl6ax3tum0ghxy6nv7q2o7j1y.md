## 7 Laravel Packages to Improve Coding Standards and Reduce Bugs

Frustrated with fixing the same kind of issues and spending more time to improve your App coding standard? This is a common issue for larger apps with more number developers working on it. We spend more time maintaining the coding standard across the team and reducing bugs, To make this simple we have a few packages to automate these.

As we all know, the [Laravel](https://laravel.com/) community is growing rapidly daily, and the packages developed for Laravel are also increasing. We will look into a few packages in this article to improve PHP coding standards and automate some tasks that were done manually.


## Larastan

![Screenshot 2022-07-31 at 1.45.24 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343141304/b6mxwJOBa.png align="left")

[Larastan](https://github.com/nunomaduro/larastan) is a Coding Standards Fixer tool, It's a [PHPStan](https://phpstan.org/) wrapper for Laravel. Larastan focuses on finding errors in your code. It catches whole classes of bugs even before you write tests for the code.

### Highlights

1. Adds static typing to Laravel to improve developer productivity and code quality.
2. Supports most of Laravel's magic methods.
3. Discovers bugs in your code.

**Github - 4.1K ⭐️**


## PHPStan

[PHPStan](https://github.com/phpstan/phpstan) is a static code analysis tool, It focuses on finding errors in your code without actually running it. It catches whole classes of bugs even before you write tests for the code. It moves PHP closer to compiled languages in the sense that the correctness of each line of the code can be checked before you run the actual code.

### Highlights

1. Find bugs before they reach production.
2. Gradual Integration
3. Legacy compatibility
4. Third-party framework integrations

![Screenshot 2022-07-31 at 12.30.18 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343173193/XwtSjPhcg.png align="left")

**Github - 11.2K ⭐️**


## PHP CodeSniffer

[PHP CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) is also a coding standard tool. It tokenizes PHP files and detects violations of a defined set of coding standards. 

PHP CpdeSniffer is a set of two PHP scripts. The main `phpcs` script tokenizes PHP, JavaScript and CSS files to detect violations of a defined coding standard, and a second `phpcbf` script automatically corrects coding standard violations. PHP CodeSniffer is an essential development tool that ensures your code remains clean and consistent.

![php-sniffer.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343234181/C10W08yZM.png align="left")

**Github - 9.6K ⭐️**


## Phan

[Phan](https://github.com/phan/phan) is a static analyzer for PHP. Phan prefers to avoid false positives and attempts to prove incorrectness rather than correctness. 

Phan looks for common issues and will verify type compatibility on various operations when type information is available or can be deduced. Phan has a good understanding of flow control and can track values in a few use cases (e.g. arrays, integers, and strings).

**Github - 5.3K ⭐️**


## PHP Inspections


![ea-logo.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343263010/QJsK3r4bU.png align="center")

[PHP Inspections](https://github.com/kalessil/phpinspectionsea) is a static code analyzer and code review tool for PhpStorm IDE.
 
### Highlights

1. Architecture related issues
2. Weak types of control and possible code construct simplifications
3. Performance issues
4. Validation of magic methods usage
5. Validation of exception handling workflow
6. Compatibility issues
7. Variety of time-consuming bugs
8. Security issues

**Github - 1.3K ⭐️**


## PHP Insights


![Screenshot 2022-07-31 at 1.04.10 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343283717/x6t_G4APh.png align="left")

[PHP Insights](https://github.com/nunomaduro/phpinsights) is a static analysis tool of your code directly from your terminal. By running a single command it displays the Quality of Code, Complexity of Code, Architecture and Coding Style.

### Highlights

1. Analysis of code quality and coding style
2. Beautiful overview of code architecture and its complexity
3. Designed to work out-of-the-box with Laravel, Symfony, Yii, Magento, and more
4. Contains built-in checks for making code reliable, loosely coupled, simple, and clean.


![Screenshot 2022-07-31 at 1.02.58 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343303951/fn33Wtyo9.png align="left")
**Github - 4.7K ⭐️**

## PEST

![Screenshot 2022-07-31 at 1.17.53 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343322109/yCe1GSP_J.png align="left")

[Pest](https://github.com/pestphp/pest) is an elegant PHP Testing Framework with a focus on simplicity. It has a good interface to display test results and easily understandable APIs to write tests. 

Pest also has [IDE plugins](https://pestphp.com/docs/ide-plugins) for PHP Strom and VS Code.


![Screenshot 2022-07-31 at 1.17.00 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343339102/f5rj6vz_b.png align="left")
**Github - 5.1K ⭐️**

## Laravel Pint

![Screenshot 2022-07-31 at 1.26.50 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343354569/zF9XtJ7RF.png align="left")

[Laravel Pint](https://github.com/laravel/pint) is an opinionated PHP code style fixer for minimalists. Pint is built on top of [PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) and makes it simple to ensure that your code style stays clean and consistent. Pint is a new addition to the [Laravel framework](https://laravel.com/docs/9.x/pint#introduction). 

It will be available pre-installed on fresh installs.
By default, Pint does not require any configuration and will fix code style issues in your code by following the opinionated coding style of Laravel.


![Screenshot 2022-07-31 at 1.27.29 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659343376414/Nvq05K0yD.png align="left")

**Github - 2K ⭐️**


## Conclusion

There are multiple open source tools to maintain coding standards and reduce bugs in Laravel. Choose a tool from above that best fits your project and environment. This will drastically decrease the developer's time spent on finding issues.

Thank you for reading.
