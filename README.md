# vscode-remote-workspace

[![Share via Facebook](https://raw.githubusercontent.com/mkloubert/vscode-remote-workspace/master/img/share/Facebook.png)](https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace&quote=Git%20Notify) [![Share via Twitter](https://raw.githubusercontent.com/mkloubert/vscode-remote-workspace/master/img/share/Twitter.png)](https://twitter.com/intent/tweet?source=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace&text=Git%20Notify:%20https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace&via=mjkloubert) [![Share via Google+](https://raw.githubusercontent.com/mkloubert/vscode-remote-workspace/master/img/share/Google+.png)](https://plus.google.com/share?url=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace) [![Share via Pinterest](https://raw.githubusercontent.com/mkloubert/vscode-remote-workspace/master/img/share/Pinterest.png)](http://pinterest.com/pin/create/button/?url=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace&description=Visual%20Studio%20Code%20extension%2C%20which%20receives%20and%20shows%20git%20events%20from%20webhooks.) [![Share via Reddit](https://raw.githubusercontent.com/mkloubert/vscode-remote-workspace/master/img/share/Reddit.png)](http://www.reddit.com/submit?url=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace&title=Git%20Notify) [![Share via LinkedIn](https://raw.githubusercontent.com/mkloubert/vscode-remote-workspace/master/img/share/LinkedIn.png)](http://www.linkedin.com/shareArticle?mini=true&url=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace&title=Git%20Notify&summary=Visual%20Studio%20Code%20extension%2C%20which%20receives%20and%20shows%20git%20events%20from%20webhooks.&source=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace) [![Share via Wordpress](https://raw.githubusercontent.com/mkloubert/vscode-remote-workspace/master/img/share/Wordpress.png)](http://wordpress.com/press-this.php?u=https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace&quote=Git%20Notify&s=Visual%20Studio%20Code%20extension%2C%20which%20receives%20and%20shows%20git%20events%20from%20webhooks.) [![Share via Email](https://raw.githubusercontent.com/mkloubert/vscode-remote-workspace/master/img/share/Email.png)](mailto:?subject=Git%20Notify&body=Visual%20Studio%20Code%20extension%2C%20which%20receives%20and%20shows%20git%20events%20from%20webhooks.:%20https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmkloubert.vscode-remote-workspace)


[![Latest Release](https://vsmarketplacebadge.apphb.com/version-short/mkloubert.vscode-remote-workspace.svg)](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-remote-workspace)
[![Installs](https://vsmarketplacebadge.apphb.com/installs/mkloubert.vscode-remote-workspace.svg)](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-remote-workspace)
[![Rating](https://vsmarketplacebadge.apphb.com/rating-short/mkloubert.vscode-remote-workspace.svg)](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-remote-workspace#review-details)

Multi protocol support for handling remote files like local ones in [Visual Studio Code](https://code.visualstudio.com).

## Table of contents

1. [Install](#install-)
2. [How to use](#how-to-use-)
   * [Azure](#azure-)
     * [Remarks](#remarks-)
   * [Dropbox](#dropbox-)
   * [FTP](#ftp-)
   * [S3 Buckets](#s3-buckets-)
     * [credential_type](#credential_type-)
     * [Parameters](#parameters-)
   * [SFTP](#sftp-)
   * [Slack](#slack-)
     * [Remarks](#remarks-1-)
3. [Support and contribute](#support-and-contribute-)
4. [Related projects](#related-projects-)
   * [vscode-helpers](#vscode-helpers-)

## Install [[&uarr;](#table-of-contents)]

Launch VS Code Quick Open (`Ctrl + P`), paste the following command, and press enter:

```bash
ext install vscode-remote-workspace
```

Or search for things like `vscode-remote-workspace` in your editor.

## How to use [[&uarr;](#table-of-contents)]

Create (or update) a `.code-workspace` file and open it by using `File >> Open Workspace...` in the GUI:

```json
{
    "folders": [{
        "uri": "sftp://my-user:my-password@example.com",
        "name": "My SFTP folder"
    }],
    "settings": {}
}
```

### Azure [[&uarr;](#how-to-use-)]

URL Format: `azure://[account:key@][container][/path/to/file/or/folder]`

```json
{
    "folders": [{
        "uri": "azure://my-account:my-storage-key@my-container/",
        "name": "My Azure folder"
    }],
    "settings": {}
}
```

For accessing local storage emulator, use something like that:

```json
{
    "folders": [{
        "uri": "azure://mycontainer/",
        "name": "My local Azure folder"
    }],
    "settings": {}
}
```

#### Remarks [[&uarr;](#azure-)]

If you create a new folder, a file called `.vscode-remote-workspace` with 0 size is created there, to keep sure to detect that new folder later.
Before you delete that file, you should store another file there, otherwise the directory will disappear.

### Dropbox [[&uarr;](#how-to-use-)]

URL Format: `dropbox://token[/path/to/file/or/folder]`

```json
{
    "folders": [{
        "uri": "dropbox://<API-TOKEN>/",
        "name": "My Dropbox folder"
    }],
    "settings": {}
}
```

### FTP [[&uarr;](#how-to-use-)]

URL Format: `ftp://[user:password@]host[:port][/path/to/a/folder]`

```json
{
    "folders": [{
        "uri": "ftp://my-user:my-password@ftp.example.com/",
        "name": "My FTP folder"
    }],
    "settings": {}
}
```

### S3 Buckets [[&uarr;](#how-to-use-)]

URL Format: `s3://[credential_type@]bucket[/path/to/file/or/folder][?option1=value1&option2=value2]`

```json
{
    "folders": [{
        "uri": "s3://my-bucket/?acl=public-read",
        "name": "My S3 Bucket"
    }],
    "settings": {}
}
```

#### credential_type [[&uarr;](#s3-buckets-)]

Default value: `shared`

| Name | Description | Class in [AWS SDK](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/index.html) |
| ---- | --------- | --------- |
| `environment` | Represents credentials from the environment. | [EnvironmentCredentials](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EnvironmentCredentials.html) |
| `file` | Represents credentials from a JSON file on disk. | [FileSystemCredentials](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/FileSystemCredentials.html) |
| `shared` | Represents credentials loaded from shared credentials file. | [SharedIniFileCredentials](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/SharedIniFileCredentials.html) |

##### Parameters [[&uarr;](#s3-buckets-)]

| Name | Description | Example | 
| ---- | --------- | --------- | 
| `acl` | The [ACL](https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html) for new or updated files to use. Default: `private` | `acl=public-read` | 
| `file` | If credential type is set to `file`, this defines the path to the `.json` file, which should be used. Relative paths will be mapped to the `.aws` sub folder inside the user's home directory. | `file=aws.json` |
| `profile` | If credential type is set to `shared`, this defines the name of the section inside the `.ini` file, which should be used. Default: `default` | `profile=mkloubert` |
| `var_prefix` | If credential type is set to `environment`, this defines the custom prefix for the environment variables (without `_` suffix!), which contain the credentials. Default: `AWS` | `var_prefix=MY_AWS_PREFIX` |

### SFTP [[&uarr;](#how-to-use-)]

URL Format: `sftp://[user:password@]host[:port][/path/to/a/folder]`

```json
{
    "folders": [{
        "uri": "sftp://my-user:my-password@sftp.example.com/",
        "name": "My SFTP folder"
    }],
    "settings": {}
}
```

### Slack [[&uarr;](#how-to-use-)]

URL Format: `slack://token@channel[/]`

```json
{
    "folders": [{
        "uri": "slack://<API-TOKEN>@<CHANNEL-ID>",
        "name": "My Slack channel"
    }],
    "settings": {}
}
```

#### Remarks [[&uarr;](#slack-)]

The protocol only supports read and list operations.

## Support and contribute [[&uarr;](#table-of-contents)]

If you like the extension, you can support the project by sending a [donation via PayPal](https://paypal.me/MarcelKloubert) to [me](https://github.com/mkloubert).

To contribute, you can [open an issue](https://github.com/mkloubert/vscode-remote-workspace/issues) and/or fork this repository.

To work with the code:

* clone [this repository](https://github.com/mkloubert/vscode-remote-workspace)
* create and change to a new branch, like `git checkout -b my_new_feature`
* run `npm install` from your project folder
* open that project folder in Visual Studio Code
* now you can edit and debug there
* commit your changes to your new branch and sync it with your forked GitHub repo
* make a [pull request](https://github.com/mkloubert/vscode-remote-workspace/pulls)

## Related projects [[&uarr;](#table-of-contents)]

### vscode-helpers [[&uarr;](#related-projects-)]

[vscode-helpers](https://github.com/mkloubert/vscode-helpers) is a NPM module, which you can use in your own [VSCode extension](https://code.visualstudio.com/docs/extensions/overview) and contains a lot of helpful classes and functions.