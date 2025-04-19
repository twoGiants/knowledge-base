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

- Git: Discard Changes : `ct + k, ct + al + backspace`
- Git Log: `al + sh + h`
