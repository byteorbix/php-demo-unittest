## PHP Demo Project with Unit Tests and CI Integration

Here are the steps to set up your environment in Visual Studio Code for this PHP project.


### 1. Install Required Extensions
Install these VS Code extensions:
- **[PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client)** – IntelliSense, code navigation
- **[PHPUnit Test Explorer](https://marketplace.visualstudio.com/items?itemName=recca0120.vscode-phpunit)** – Run/debug PHPUnit tests
- **[PHP Debug](https://marketplace.visualstudio.com/items?itemName=xdebug.php-debug)** – Debugging with Xdebug


### 2. Install Dependencies
Open the integrated terminal (**Ctrl+`**) and run:
```sh
composer install
```


### 3. Configure VS Code Settings
Create a `.vscode/settings.json` file:
```json
{
    "php.validate.executablePath": "php",
    "phpunit.phpunit": "vendor/bin/phpunit",
    "phpunit.args": ["--configuration", "phpunit.xml"],
    "intelephense.environment.phpVersion": "8.2"
}
```

### 4. Create a PHPUnit Configuration File
```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="vendor/phpunit/phpunit/phpunit.xsd"
         bootstrap="vendor/autoload.php"
         colors="true">
    <testsuites>
        <testsuite name="Unit">
            <directory>tests</directory>
        </testsuite>
    </testsuites>
    <source>
        <include>
            <directory>src</directory>
        </include>
    </source>
</phpunit>
```


### 5. Configure Debugging (Optional)
Create a `.vscode/launch.json` for Xdebug support:
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003
        },
        {
            "name": "PHPUnit Debug",
            "type": "php",
            "request": "launch",
            "program": "${workspaceFolder}/vendor/bin/phpunit",
            "args": ["--configuration", "phpunit.xml"],
            "port": 9003
        }
    ]
}
```

---

### 6. Verify Setup
Run tests via the terminal:
```sh
composer test
```
Or use the **Testing** panel in VS Code (beaker icon) to run/debug individual tests.

### 7. CI Integration
There is a GitHub Workflow definded, that gets triggered when pushing to the repository. It will then run the unit tests and report on failure and success.