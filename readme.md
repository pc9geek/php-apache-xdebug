## Docker Apache PHP Xdebug

This is a template for quickly getting up a working php environment with debugging enabled
usage: ```docker compose up -d```

Place your php application files in the ./app folder
access the app on localhost:8080

### here is a sample launch.json if using vscode
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "pathMappings": {
                "/var/www/html": "${workspaceFolder}/app"
            }
        }
    ]
}
```
