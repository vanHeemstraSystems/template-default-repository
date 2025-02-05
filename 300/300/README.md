# 300 - Creating a New React Monorepo

**Warning**: Make sure you have installed and created the directory structure of ```hatch``` already. See [HATCH.md](../../HATCH.md)

Create a new React monorepo with the following command:

```
$ cd hatch-project/src # navigate to the 'hatch-project/src' sub-directory, previously created by hatch
$ npx create-nx-workspace@latest hatch_project --preset=react-monorepo
```

When prompted, provide the following answers:

```
NX   Let's create a new workspace [https://nx.dev/getting-started/intro]


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

MORE ...
