# CF-Workers-Raw：Easy Access to GitHub private repositories
This project allows you to securely access original files in private GitHub repositories through Cloudflare Workers, without directly exposing your GitHub token.
这个项目允许你通过Cloudflare Workers安全地访问GitHub私有仓库中的原始文件，无需直接暴露你的GitHub令牌。
## Why do you need this tool?

- You have some important files stored in a private GitHub repository.
- You want to access the raw content of these files (e.g., configuration files, data files, etc.) directly via URL.
- However, you don't want to expose your GitHub token directly in the URL because it could be abused by others.

Our solution is to use Cloudflare Workers as a middle layer, which securely handles authentication for you, allowing you to securely access private files.
## How does it work? [Video tutorial](https://www.youtube.com/watch?v=T-bK5o96lqI)
Assuming your Cloudflare Workers project is deployed at `raw.090227.xyz`.

And the private file you want to access is `https://raw.githubusercontent.com/cmliu/CF-Workers-Raw/main/_worker.js`.

## Method 1: Pass the token via URL parameters
```

## Method 3: Add additional access control (recommended)
For greater security, you can set two variables:

- `GH_TOKEN`: your GitHub token
- `TOKEN`: a custom access key (such as mysecretkey)

Then, your URL will look like this:
```url
https://raw.090227.xyz/cmliu/CF-Workers-Raw/main/_worker.js?token=mysecretkey
```
Or if you prefer the full original URL:
```url
https://raw.090227.xyz/https://raw.githubusercontent.com/cmliu/CF-Workers-Raw/main/_worker.js?token=mysecretkey
```
This approach provides double security: even if someone guesses your custom key, they still won't be able to access your GitHub files because the GitHub token is stored securely in the Workers settings.

## Method 4: Add `GH_NAME`, `GH_REPO`, `GH_BRANCH` variables **Hide GitHub path information**

For greater privacy, you can set multiple variables:
- `GH_NAME`: your GitHub username (for example: **cmliu**)
Then, your URL will look like this:
```url
https://raw.090227.xyz/CF-Workers-Raw/main/_worker.js?token=sd123123
```

- `GH_REPO`: your GitHub repository name (for example: **CF-Workers-Raw**, the `GH_NAME` variable must be set as a prerequisite)
Then, your URL will look like this:
```url
https://raw.090227.xyz/main/_worker.js?token=sd123123
```

- `GH_BRANCH`: your GitHub repository name (for example: **main**, you must set the `GH_NAME` and `GH_REPO` variables as a prerequisite)
Then, your URL will look like this:
```url
https://raw.090227.xyz/_worker.js?token=sd123123
```

**If you use the complete original URL, the above variables will not take effect! **
```url
https://raw.090227.xyz/https://raw.githubusercontent.com/cmliu/CF-Workers-Raw/main/_worker.js?token=sd123123
```

## How to set these variables?

In your Cloudflare Workers admin panel:

1. Enter your Workers project.
2. Click the **Settings** tab.
3. Scroll to the **Environment Variables** section.
4. Add the following variables:
- Variable: GH_TOKEN, value: your GitHub personal access token
- Variable: TOKEN (optional), value: your custom access key

GitHub personal access tokens can be generated on the "Developer settings" > "Personal access tokens (classic)" page in GitHub settings.

## Error handling

If something goes wrong, you'll see one of the following error messages:

- **Wrong TOKEN**: The custom access key you provided is incorrect.
- **TOKEN cannot be empty**: GitHub token is required.
- **Unable to get file detecting path or TOKEN**: The file path is wrong or the token does not have permission to access the file.
- **Path cannot be empty**: You did not specify a file path to access.

# Variable description
| Variable name | Example | Required | Remarks |
|--|--|--|--|
| GH_TOKEN| `ghp_CgmlL2b5J8Z1soNUquc0bZblkbO3gKxhn13t`| ❌| Your GitHub token **token**|
| TOKEN| `nicaibudaowo` | ❌| When `GH_TOKEN` and `TOKEN` exist at the same time, they will be used as access authentication. When assigned separately, the effect is the same as `GH_TOKEN` |
| GH_NAME| `cmliu` | ❌| Your GitHub username |
| GH_REPO| `CF-Workers-Raw` | ❌| Your GitHub repository (the `GH_NAME` variable must be set as a prerequisite) |
| GH_BRANCH| `main` | ❌| Your GitHub repository (must set `GH_NAME` and `GH_REPO` variables as a prerequisite) |
| URL302 | `https://t.me/CMLiussss` |❌| Home page 302 jump |
| URL | `https://github.com/cmliu/CF-Workers-Raw/blob/main/README.md` |❌| Home Page Disguise |
| ERROR | `Unable to obtain file, check whether the path or TOKEN is correct. ` |❌| Custom error prompt |

# grateful
My own imagination, ChatGPT## Method 1: Pass the token via URL parameters
```

## Method 3: Add additional access control (recommended)
For greater security, you can set two variables:

- `GH_TOKEN`: your GitHub token
- `TOKEN`: a custom access key (such as mysecretkey)

Then, your URL will look like this:
```url
https://raw.090227.xyz/cmliu/CF-Workers-Raw/main/_worker.js?token=mysecretkey
```
Or if you prefer the full original URL:
```url
https://raw.090227.xyz/https://raw.githubusercontent.com/cmliu/CF-Workers-Raw/main/_worker.js?token=mysecretkey
```
This approach provides double security: even if someone guesses your custom key, they still won't be able to access your GitHub files because the GitHub token is stored securely in the Workers settings.

## Method 4: Add `GH_NAME`, `GH_REPO`, `GH_BRANCH` variables **Hide GitHub path information**

For greater privacy, you can set multiple variables:
- `GH_NAME`: your GitHub username (for example: **cmliu**)
Then, your URL will look like this:
```url
https://raw.090227.xyz/CF-Workers-Raw/main/_worker.js?token=sd123123
```

- `GH_REPO`: your GitHub repository name (for example: **CF-Workers-Raw**, the `GH_NAME` variable must be set as a prerequisite)
Then, your URL will look like this:
```url
https://raw.090227.xyz/main/_worker.js?token=sd123123
```

- `GH_BRANCH`: your GitHub repository name (for example: **main**, you must set the `GH_NAME` and `GH_REPO` variables as a prerequisite)
Then, your URL will look like this:
```url
https://raw.090227.xyz/_worker.js?token=sd123123
```

**If you use the complete original URL, the above variables will not take effect! **
```url
https://raw.090227.xyz/https://raw.githubusercontent.com/cmliu/CF-Workers-Raw/main/_worker.js?token=sd123123
```

## How to set these variables?

In your Cloudflare Workers admin panel:

1. Enter your Workers project.
2. Click the **Settings** tab.
3. Scroll to the **Environment Variables** section.
4. Add the following variables:
- Variable: GH_TOKEN, value: your GitHub personal access token
- Variable: TOKEN (optional), value: your custom access key

GitHub personal access tokens can be generated on the "Developer settings" > "Personal access tokens (classic)" page in GitHub settings.

## Error handling

If something goes wrong, you'll see one of the following error messages:

- **Wrong TOKEN**: The custom access key you provided is incorrect.
- **TOKEN cannot be empty**: GitHub token is required.
- **Unable to get file detecting path or TOKEN**: The file path is wrong or the token does not have permission to access the file.
- **Path cannot be empty**: You did not specify a file path to access.

# Variable description
| Variable name | Example | Required | Remarks |
|--|--|--|--|
| GH_TOKEN| `ghp_CgmlL2b5J8Z1soNUquc0bZblkbO3gKxhn13t`| ❌| Your GitHub token **token**|
| TOKEN| `nicaibudaowo` | ❌| When `GH_TOKEN` and `TOKEN` exist at the same time, they will be used as access authentication. When assigned separately, the effect is the same as `GH_TOKEN` |
| GH_NAME| `cmliu` | ❌| Your GitHub username |
| GH_REPO| `CF-Workers-Raw` | ❌| Your GitHub repository (the `GH_NAME` variable must be set as a prerequisite) |
| GH_BRANCH| `main` | ❌| Your GitHub repository (must set `GH_NAME` and `GH_REPO` variables as a prerequisite) |
| URL302 | `https://t.me/CMLiussss` |❌| Home page 302 jump |
| URL | `https://github.com/cmliu/CF-Workers-Raw/blob/main/README.md` |❌| Home Page Disguise |
| ERROR | `Unable to obtain file, check whether the path or TOKEN is correct. ` |❌| Custom error prompt |

# grateful
My own imagination, ChatGPT
