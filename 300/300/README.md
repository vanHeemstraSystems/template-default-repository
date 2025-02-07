# 300 - Creating a New React Monorepo

**Warning**: Make sure you have installed and created the directory structure of ```hatch``` already. See [HATCH.md](../../HATCH.md)<br/>
**Warning**: Make sure you have installed ```nx``` already. See [NX.md](../../NX.md).

Create a new React monorepo with the following command:

```
$ cd hatch-project/src # navigate to the 'hatch-project/src' sub-directory, previously created by hatch
$ mv hatch_project original_hatch_project # temporarily rename the hatch_project directory so nx will not complain
$ npx create-nx-workspace@latest hatch_project --preset=react-monorepo
```

When prompted, provide the following answers:

```
Need to install the following packages:
create-nx-workspace@20.4.0
Ok to proceed? (y)
```

Click y & ENTER.

```
NX   Let's create a new workspace [https://nx.dev/getting-started/intro]

? Application name hatch_project
```

Click ENTER.

```
? Which bundler would you like to use?
Vite    [ https://vitejs.dev/     ]
Webpack [ https://webpack.js.org/ ]
Rspack  [ https://www.rspack.dev/ ]
```

Highlight **Webpack** with the arrow keys and click ENTER.

```
? Test runner to use for end to end (E2E) tests ...
Playwright [ https://playwright.dev/ ]
Cypress [ https://www.cypress.io/ ]
None
```

Highlight **Playwright** with the arrow keys and click ENTER.

```
? Default stylesheet format ...
CSS
SASS(.scss)       [ https://sass-lang.com                    ]
LESS              [ https://lesscss.org                      ]
tailwind          [ https://tailwindcss.com                  ]
styled-components [ https://styled-components.com            ]
emotion           [ https://emotion.sh                       ]
styled-jsx        [ https://www.npmjs.com/package/styled-jsx ]
```

Highlight **tailwindcss** with the arrow keys and click ENTER.


```
? Which CI provider would you like to use? ...
GitHub Actions
Gitlab
Azure DevOps
BitBucket Pipelines
Circle CI

Do it later
```

Highlight **GitHub Actions** with the arrow keys and click ENTER.

It will respond with:

```
NX Creating your v20.4.0 workspace.

Installing dependencies with npm
Successfully created the workspace: hatch_project
Nx Cloud has been set up successfully
CI workflow has been generated successfully

NX Directory is already under version control. Skipping initialization of git.

NX   Your CI setup is almost complete.

Finish it by visiting: https://cloud.nx.app/connect/lvaFjW0bDV

NX   Welcome to the Nx community! 👋

🌟 Star Nx on GitHub: https://github.com/nrwl/nx
📢 Stay up to date on X: https://x.com/nxdevtools
💬 Discuss Nx on Discord: https://go.nx.dev/community
```

This will generate the following file and directory structure underneath the ```/hatch-project/src``` directory (Note: ```hatch_project``` uses that same directory as previously created by Hatch. **This is intentional!**):

```
└─ hatch-project
               └─ src
                    └─ hatch_project
                                   ├─ ...
                                   ├─ apps
                                   │  ├─ react-store
                                   │  │  ├─ public
                                   │  │  │  └─ ...
                                   │  │  ├─ src
                                   │  │  │  ├─ app
                                   │  │  │  │  ├─ app.module.css
                                   │  │  │  │  ├─ app.spec.tsx
                                   │  │  │  │  ├─ app.tsx
                                   │  │  │  │  └─ nx-welcome.tsx
                                   │  │  │  ├─ assets
                                   │  │  │  ├─ main.tsx
                                   │  │  │  └─ styles.css
                                   │  │  ├─ index.html
                                   │  │  ├─ project.json
                                   │  │  ├─ tsconfig.app.json
                                   │  │  ├─ tsconfig.json
                                   │  │  ├─ tsconfig.spec.json
                                   │  │  └─ vite.config.ts
                                   │  └─ react-store-e2e
                                   │     └─ ...
                                   ├─ nx.json
                                   ├─ tsconfig.base.json
                                   └─ package.json
```

**Important**: Move all files previously in ```original_hatch_project``` to ```hatch_project``` and delete ```original_hatch_project```!

### Key Points:
- **`hatch_project/nx.json`**: Configuration for the Nx workspace.
- **`hatch_project/package.json`**: Dependencies and scripts specific to the project.
- **`hatch_project/tsconfig.json`**: TypeScript configuration for the project.
- **`hatch_project/workspace.json` or `project.json`**: Defines the structure and projects within the workspace.

**IMPORTANT**: Move **nx.json** to ```hatch-project``` directory so it can connect with Nx Cloud.

```
└─ hatch-project
               ├─ ...
               ├─ nx.json
               └─ src
                    └─ hatch_project
                                   ├─ ...               
```

**IMPORTANT**: Modify **nx.json** so it can connect with Nx Cloud.

Here’s a sample `nx.json` configuration that supports Nx Cloud for your workspace:

```json
{
  "npmScope": "hatch_project",
  "affected": {
    "defaultBase": "main"
  },
  "tasksRunnerOptions": {
    "default": {
      "runner": "@nrwl/workspace/src/tasks-runner/default-task-runner",
      "options": {
        "cacheableOperations": ["build", "test", "lint"],
        "localCache": true
      }
    }
  },
  "projects": {
    "hatch_project": {
      "root": "src/hatch_project",
      "sourceRoot": "src/hatch_project/src",
      "projectType": "application",
      "targets": {
        "build": {
          "executor": "@nrwl/web:build",
          "options": {
            "outputPath": "dist/hatch_project",
            "index": "src/hatch_project/src/index.html",
            "main": "src/hatch_project/src/main.tsx",
            "polyfills": "src/hatch_project/src/polyfills.ts",
            "tsConfig": "src/hatch_project/tsconfig.app.json",
            "assets": ["src/hatch_project/src/favicon.ico", "src/hatch_project/src/assets"],
            "styles": ["src/hatch_project/src/styles.css"],
            "scripts": []
          }
        }
      }
    }
  }
}
```

Notice that it prepends paths with ```src/``` (e.g., ```"root": "src/hatch_project",```) to allow for our **nested** directory structure.

### Key Sections:
- **`npmScope`**: Defines the scope for your packages.
- **`affected.defaultBase`**: Specifies the default branch for determining affected projects.
- **`tasksRunnerOptions`**: Configures caching and task running options.
- **`projects`**: Contains the project configuration, specifying the root and source root paths, project type, and build targets.

Adjust paths and options as necessary to fit your specific project structure. This configuration will help Nx Cloud identify and manage your workspace correctly.

Make sure to run the **build** command from the `/hatch-project/src` directory to ensure it recognizes the workspace correctly:
```
$ nx build hatch_project
```

This structure should allow Nx Cloud to detect the workspace properly.

Run the command to **connect** your workspace to Nx Cloud from the root directory of the `hatch-project`, specifically:

```
$ cd /hatch-project/
```

The command to connect to Nx Cloud is:

```
$ nx connect-to-nx-cloud
```

This will initiate the configuration process for Nx Cloud within your workspace.

Finish the CI setup by visiting: https://cloud.nx.app/connect/lvaFjW0bDV # **Note**: the URL will differ per creation. See [Enable GitHub PR Integration](https://nx.dev/ci/recipes/source-control-integration/github) and/or watch [PNPM-CI: Connect Your Workspace to Nx Cloud for Enhanced Collaboration](https://www.youtube.com/watch?v=8mqHXYIl_qI).

## Nested app directories

You can have nested folders, no problems. 👍 Here's a [live example](https://github.com/codyslexia/nexa/tree/main/apps/graphql). You can see that apps/graphql/users is a nested directory where users is the actual project. There's also this [other example](https://github.com/nrwl/nx-incremental-large-repo/tree/master/libs/app0/lib1) from the ```nrwl``` family.
