# Wdes coding-standard

The Wdes coding-standard

## How to add it

- Run `composer require --dev wdes/coding-standard`
- Create file: `phpcs.xml` with the contents below

```xml
<?xml version="1.0"?>
<ruleset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="vendor/squizlabs/php_codesniffer/phpcs.xsd">

    <!-- Show progress and sniff codes -->
    <arg value="ps"/>
    <arg name="colors"/>
    <!-- Make sniff report relative -->
    <arg name="basepath" value="."/>

    <file>.</file>
    <exclude-pattern>*/tmp/*</exclude-pattern>
    <exclude-pattern>*/vendor/*</exclude-pattern>
    <exclude-pattern>*/build/*</exclude-pattern>
    <exclude-pattern>*/node_modules/*</exclude-pattern>

    <rule ref="Wdes"></rule>
</ruleset>
```

- Remove phpcs from your dev deps if you have it, we require it for you. Use `composer remove squizlabs/php_codesniffer --dev`

- Run `./vendor/bin/phpcs` to see the coding standard errors
- Run `./vendor/bin/phpcbf` to try to fix them

## How to exclude rules

### Examples of ways to exclude rules

```xml
<?xml version="1.0"?>
<ruleset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="vendor/squizlabs/php_codesniffer/phpcs.xsd">

    <!-- Show progress and sniff codes -->
    <arg value="ps"/>
    <!-- Cache file -->
    <arg name="cache" value=".php_cs.cache"/>
    <arg name="colors"/>

    <!-- Paths to check -->
    <file>src</file>
    <file>scripts</file>
    <file>examples</file>
    <file>tests</file>

    <!-- Exclude files from phpcs -->
    <exclude-pattern>*/src/Resources/themes/*</exclude-pattern>
    <exclude-pattern>*/tests/phar/data/**/*</exclude-pattern>

    <!-- Exclude a rule from the Wdes standard -->
    <rule ref="Wdes">
        <exclude name="Generic.Formatting.MultipleStatementAlignment.NotSameWarning"/>
    </rule>

    <!-- Or lower the severity to zero -->
    <rule ref="Generic.Files.LineLength.TooLong">
        <severity>0</severity>
    </rule>

    <!-- Or exclude the rule -->
    <exclude name="PSR1.Files.SideEffects.FoundWithSymbols"/>

    <!-- Or remove the rule for all files -->
    <rule ref="Generic.PHP.NoSilencedErrors.Discouraged">
        <exclude-pattern>*</exclude-pattern>
    </rule>

</ruleset>
```
