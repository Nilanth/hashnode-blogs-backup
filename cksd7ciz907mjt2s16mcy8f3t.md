## No More ../../../ Import in React

Steps to configure absolute Import in Create React App without any third-party packages.

Are you importing components like `../../../../somecomponents`? Then you should update to Absolute imports. 

## Benefits of Absolute Import

1. You can move your existing code to other components with imports without any changes.
2. You can easily identify that where the component is actually placed using the import path.
3. Cleaner Code.
4. Easier to write.

## Configure Absolute Import

To support absolute import create a file named `jsconfig.json` in your root directory and add the below code. 

%[https://gist.github.com/Nilanth/e0c0dec55445cd706824d5615d5c220c]

Now let's convert the relative imports in the below component to Absolute Import

%[https://gist.github.com/Nilanth/bb2caa0406421ad145f30b0450cec5a9]

The Above imports will be changed to as below

%[https://gist.github.com/Nilanth/6142aaf9c4d2f23b4a81e062859c47f3]

Now our imports are clean and understandable. 


## Configuring in JET Brains IDEs

* For JET Brains IDEs like WebStorm, PhpStorm, RubyMine and etc, we need to add some additional configurations as below to support Absolute import

`Right-click` the `src` folder and select `Mark Directory as` and Click `Resource Root`.


![mark-directory](https://cdn.hashnode.com/res/hashnode/image/upload/v1628416169573/iF9hxF0EB.png)

* Next select **Preferences** -> **Editor** -> **Code Style** -> **JavaScript** -> **Imports** and Check **Use paths relative to the project, resource or source roots** and Click **Apply**.

![jetbrains-ide](https://cdn.hashnode.com/res/hashnode/image/upload/v1628416195808/gOb1SZGan.png)

## VS Code

No Changes need to be done in VS Code. It will automatically import the config from `jsconfig.json` file.

## Resources

1. [VS Code jsconfig.json](https://code.visualstudio.com/docs/languages/jsconfig)
2. [JET Brains CodeStyle](https://www.jetbrains.com/help/idea/settings-code-style-javascript.html#ws_js_settings_editor_code_style_imports_tab)

## Conclusion

Absolute imports make the component more readable and clean. I hope you have found this useful. Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).