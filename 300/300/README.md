# 300 - Creating a New React Monorepo

**Warning**: Make sure you have installed and created the directory structure of ```hatch``` already. See [HATCH.md](../../HATCH.md)

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

Click y & ENTER

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

This will generate the following file and directory structure underneath the ```src``` directory (Note: ```hatch_project``` uses that same directory as previously created by Hatch. **This is intentional!**):

```
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

MORE ...
