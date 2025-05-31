# VSCodium

Install any extension not available from the VSCodium store:

1. Install in VSCode and be aware its license allows it to be installed somewhere else.
1. Copy:

    ```sh
    cp -r ~/.var/app/com.visualstudio.code/data/vscode/extensions/<extension-name> ~/.vscode-oss/extensions
    ```

1. Install in VSCodium with `ct+sh+p` and `Install from Location...`.
1. Select the extension directory `~/.vscode-oss/<extension-name>`.

## Keyboard Shortcuts

- Git discard changes: `ct + k, ct + al + backspace`
- Git log: `al + sh + h`
- Git open changes for file: `ct + sh + al + g`
- Git open all changes in a list: `ct + sh + al + g`

- Mario block jump: `ct + al + up|do|le|ri`

- Move tab: `sh + me + le|ri`
