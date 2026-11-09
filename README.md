# MakanSihat — From Your Plate to Your Macros

**App guide · Version 1.0.0 · 9 November 2026**

MakanSihat helps you track Malaysian meals, from a complete nasi campur plate to a single piece of ayam goreng. Browse the food catalogue, choose your portions, add extra lauk, and see calories, protein, carbohydrates, and fat for each meal and day.

This guide accompanies the standalone npm edition. The editable application uses **TypeScript, React, CSS, and JSON**, with **Vite** for development and builds. It runs independently of ChatGPT or Sites and requires no API key or database.

## 1. Choose your download

| File | Use it for |
| --- | --- |
| `MakanSihat-GitHub.zip` | Editing the app, running development mode, or uploading the source to GitHub. |
| `makansihat-1.0.0.tgz` | Installing and running the already-built app through npm. |
| `BUILD-VERIFICATION.txt` | Reviewing the checks completed for this release. |
| `SECURITY-AUDIT.txt` | Reviewing the pre-publication secret and privacy audit. |
| `SHA256SUMS.txt` | Checking the integrity of the two release archives. |

The source ZIP contains a top-level `makansihat` folder. Keep its hidden `.github` folder when copying the project into a repository.

## 2. Run the editable app locally

### Requirements

- Node.js **22.18.0 or newer**; Node.js **24 LTS** is the recommended version for this release.
- npm **10 or newer**.
- A modern web browser.
- Git if you want to push to GitHub or use `npm run deploy`.

Confirm your installed versions in a terminal:

```sh
node --version
npm --version
```

### Start development mode

1. Extract `MakanSihat-GitHub.zip`.
2. Open a terminal inside the extracted `makansihat` folder, where `package.json` is located.
3. Run:

```sh
npm ci
npm run dev
```

Open the **Local** address printed by Vite, usually `http://127.0.0.1:5173`. The terminal must remain running while you use the app. Source edits appear through Vite's development updates. Press **Ctrl+C** to stop the server.

Run `npm ci` again after pulling changes that update the lockfile. Use `npm install` when intentionally adding or changing dependencies, then commit the updated lockfile.

### Build and run the production version

From the same project folder:

```sh
npm run check
npm run build
npm start
```

The build is written to `dist/`. Open **http://127.0.0.1:3000**. Rebuild after changing source files before starting the production server again.

Choose another port if needed:

```sh
npm start -- --port 8080
```

For a server or container that must accept connections on its network interface:

```sh
npm start -- --host 0.0.0.0 --port 8080
```

Use the machine's reachable hostname or IP address in your browser; `0.0.0.0` is a binding address. Public deployments should use HTTPS through the hosting platform or reverse proxy.

## 3. Run the prebuilt npm package

Open a terminal in the folder containing `makansihat-1.0.0.tgz`, then choose one method.

**Install the app command:**

```sh
npm install -g ./makansihat-1.0.0.tgz
makansihat --port 3000
```

**Run without a global installation:**

```sh
npx --package ./makansihat-1.0.0.tgz makansihat --port 3000
```

Open `http://127.0.0.1:3000`. The package includes the built website, CLI, and licence notices; it does not require a separate build. Use the source ZIP when you want to edit the application.

To inspect CLI options after installation:

```sh
makansihat --help
makansihat --version
```

These commands use a local tarball. This release has **not been published to the npm registry**, and availability of the package name `makansihat` has not been confirmed.

## 4. Track your food

The included catalogue contains **196 Malaysian foods and drinks**, including **71 à la carte items**. It covers several Malaysian cuisines and supports custom entries for foods outside the catalogue.

### Log ayam goreng on its own

1. Search for **ayam goreng**, or browse the à la carte selection.
2. Choose the item whose preparation and serving description match your food.
3. Set the portion and select Breakfast, Lunch, Dinner, or Snacks.
4. Confirm the diary date and choose **Add to my diary**.

Only the selected food and its listed serving are counted. Check the serving description before entering a quantity; one serving is not automatically one gram or one whole plate. Gram-based entry is available when the food has a reference weight.

### Build a dish with extra lauk

1. Find your base dish and choose **Add lauk**.
2. Search for and select the à la carte items you want to add.
3. Set the quantity of each extra independently.
4. Review the combined calories and macros, then save the plate to your diary.

For example, you can start with nasi lemak and add ayam goreng plus another egg. Extras count **in addition to** the ingredients already included in the base serving. Changing the base dish from one serving to two does not automatically double the attached lauk; adjust each extra separately.

The whole plate is saved as one diary entry that you can edit or remove.

### Add your own food

Choose **Custom food**, then enter its name, serving description, and calories per serving. Protein, carbohydrate, and fat values are optional and are entered in grams per serving.

Tick **This is an à la carte item** if you want the custom food to appear in the lauk picker. Otherwise it remains available as a regular custom food.

Leave a macro blank when you do not know it. Enter `0` only when its amount is known to be zero.

### Read the totals

- Food cards and portion views show calories and macros.
- The diary groups entries by meal and shows daily totals.
- The app includes favourites, an editable daily calorie guide, and a seven-day calorie view.
- A macro total with missing information is marked incomplete; a displayed lower bound such as `≥` means the known amount may be less than the actual total.

Most nutrition values are estimates for typical servings. Recipe, oil, sauces, and portion differences affect the actual values. Calorie references and macro references are tracked separately; a referenced calorie figure does not verify the estimated macros. Photo examples may show a related preparation rather than the exact serving.

## 5. npm command reference

Run these from the source project folder:

| Command | What it does |
| --- | --- |
| `npm ci` | Installs dependency versions from `package-lock.json`. |
| `npm run dev` | Starts the Vite development server. |
| `npm run typecheck` | Checks TypeScript without producing build files. |
| `npm test` | Runs the automated tests. |
| `npm run check` | Runs TypeScript checking and tests. |
| `npm run build` | Creates the production website in `dist/`. |
| `npm start` | Serves the existing production build with the included Node CLI. |
| `npm run preview` | Previews the production build locally through Vite. |
| `npm run format` | Formats project files with Prettier. |
| `npm run deploy` | Checks, builds, and publishes the website to the Git origin's `gh-pages` branch. |
| `npm pack` | Checks, builds, and creates the distributable npm tarball. |

`npm run preview` is for local previews. `npm run deploy` publishes a website; `npm publish` publishes a package to a registry. Installing dependencies does not publish either one.

## 6. Put MakanSihat on GitHub

Create an empty **public** repository in your GitHub account, for example `makansihat`. Put the extracted project contents at the repository root so `package.json` and `.github/` are directly inside it.

From that folder, replace the account and repository placeholders and run:

```sh
git init
git add .
git commit -m "Add MakanSihat"
git branch -M main
git remote add origin https://github.com/YOUR_ACCOUNT/YOUR_REPOSITORY.git
git push -u origin main
```

These commands assume a fresh project without an existing Git remote. If you already cloned the target repository, keep its existing Git configuration and commit and push the project files there. Use your preferred commit identity; a GitHub no-reply email can keep your personal email out of public commits.

### Publish the website with GitHub Actions

1. In the repository, open **Settings → Pages**.
2. Set **Source** to **GitHub Actions**.
3. Open **Actions** and run the included Pages workflow if the initial push happened before Pages was enabled.
4. Open the deployment URL reported by the successful workflow.

The included `.github/workflows/pages.yml` installs dependencies, runs checks, builds the app, and deploys eligible `main` builds. Pull requests run checks without publishing. The workflow uses GitHub's provided token and needs no manually created deployment secret; repository settings must allow Pages.

### Alternative: publish with npm

First disable the included Pages workflow or remove `.github/workflows/pages.yml`, then use this publishing route:

```sh
npm ci
npm run deploy
```

This requires an `origin` remote and working Git push authentication. In **Settings → Pages**, choose **Deploy from a branch**, select **gh-pages**, and choose **/ (root)**.

### Other static hosts and URL paths

Use `npm ci` as the install command, `npm run build` as the build command, and `dist` as the output directory. Include all generated assets, images, attribution, and licence files when uploading a build.

The default asset base is `./`, supporting both a domain root and a GitHub project path. If your host requires a fixed prefix, create `.env.local` in the source folder:

```dotenv
VITE_BASE_PATH=/YOUR_REPOSITORY/
```

Use `/` for a domain root. A fixed prefix should begin and end with `/`. Rebuild after changing it. When serving that prefix with the included Node CLI, also pass `--base-path /YOUR_REPOSITORY/`.

`VITE_` values are included in the public browser build. Keep credentials out of them.

## 7. Project map

| Location | What to edit |
| --- | --- |
| `src/App.tsx` | Main interface, diary, food browsing, and app interactions. |
| `src/styles.css` | Colours, typography, layouts, and responsive styles. |
| `src/main.tsx` | React entry point. |
| `components/lauk-picker.tsx` | Lauk selection interface. |
| `lib/calories.ts` | Nutrition, portions, and plate calculations. |
| `lib/assets.ts` | Asset paths for root and subpath hosting. |
| `data/foods.json` | Food catalogue and nutrition provenance. |
| `data/food-images.json` and `data/dessert-drink-images.json` | Food-to-photo mappings. |
| `public/foods/` | Food pictures, attribution, and photo licences. |
| `bin/makansihat.mjs` | Built-app server and CLI. |
| `tests/` | Nutrition, plate, asset, and server tests. |
| `.github/workflows/pages.yml` | GitHub checks and Pages deployment. |

After editing a food, keep its serving description, nutrition values, source details, and image attribution consistent. Run `npm run check` and `npm run build` before sharing your changes.

To create a fresh npm tarball from the source:

```sh
npm pack
```

Update the package version before distributing a new release. Registry publication also requires an available package name or a scope you own and authentication to your registry. The local tarball can be shared without registry publication.

## 8. Saved data, privacy, and release checks

The diary, favourites, custom foods, and daily calorie guide are saved in **your browser's local storage**. There is no account sync or server-side diary database. Clearing site data removes these records. A different browser profile or website origin has separate storage, so moving the app to a new domain does not transfer an existing diary.

The storage key remains `makankira-v1` to preserve compatible records on the same origin after the app rename. This identifier is not a secret. Food images are bundled locally; the stylesheet requests DM Sans from Google Fonts and falls back to system fonts when unavailable.

The delivered source ZIP and npm tarball were scanned and manually reviewed on **9 November 2026**. No hardcoded secrets, credentials, or private account information were found in those publication files. The accompanying `SECURITY-AUDIT.txt` describes the scope and archive hashes; future changes need their own review.

Release verification completed with **23 automated tests passing, 0 failing, and 1 skipped** because file-symlink permission was unavailable on the Windows verification host. Fresh source installation, production builds, npm CLI installation, and root/subpath asset loading were also checked. See `BUILD-VERIFICATION.txt` for details.

## 9. Troubleshooting

| Problem | What to check |
| --- | --- |
| `node` or `npm` is not recognised | Install a supported Node.js version, reopen the terminal, and check both version commands. |
| npm cannot find `package.json` | Change into the extracted `makansihat` project folder. |
| PowerShell blocks `npm.ps1` | Use `npm.cmd` in place of `npm`, or run the commands in Command Prompt. |
| `npm ci` fails | Confirm Node/npm versions, an intact lockfile, and network access to the npm registry; read the reported error before changing dependencies. |
| `npm start` cannot find the build | Run `npm run build` first, or use the prebuilt tarball. |
| A port is already in use | Stop the other process or run `npm start -- --port 8080`. |
| The app is blank when opening `index.html` | Start the development or production server and open its HTTP URL. |
| GitHub Pages shows 404 | Confirm a successful workflow, the correct Pages source, and the complete project including `.github/`. |
| Pictures disappear after deployment | Include all of `dist/`, check the hosting base path, and rebuild if it changed. |
| A custom food is missing from the lauk picker | Mark it as an à la carte item. |
| Macros are incomplete | Supply the missing custom-food macro values if known; blank means unknown. |
| The diary is empty on another device or URL | Records are local to each browser profile and origin. |

## 10. Licence and redistribution

The authored application code is licensed under **MIT**. Photos, fonts, and dependencies retain their own licences; the entire media collection is not covered by the code's MIT licence.

Keep `LICENSE`, `THIRD_PARTY_NOTICES.md`, photo attribution records, and the included photo licence files when redistributing the project. Preserve `public/foods/GFDL-1.2.txt` and `public/foods/GFDL-photo-notices.txt` where applicable. Some historical photo notices refer to the earlier MakanKira name and remain part of the attribution record.

For additional release documentation, read `README.md` and `DEPLOYMENT.md` inside the source ZIP.
