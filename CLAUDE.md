# tutti-sapienza-frontend

The very beginning of a React website (a "frontend", meaning the part that runs in the visitor's browser) intended to connect to a crypto wallet and a blockchain smart contract called TuttiSapienza. Right now it is still the unmodified Create React App starter page: the Web3 (blockchain) files exist but are all empty. The repo does not say what Tutti Sapienza is or who the site is for, so ask Sean rather than guessing.

## Working with the owner

Sean is a teacher who is learning to code. Explain what you are doing in plain language, define technical terms the first time you use them, and keep changes small enough to review.

## How the project fits together

Tech stack: React 19 built with Create React App (`react-scripts` 5.0.1), plain JavaScript (no TypeScript), plain CSS. npm is the package manager (`package-lock.json`).

- `public/index.html` is the HTML shell. It still has the starter title "React App"; `public/manifest.json` also has starter names.
- `src/index.js` is the entry point. It renders `<App />` into the page.
- `src/App.js` is the only component with code, and it is still the starter "Learn React" page.
- `src/App.css` has already been rewritten for a planned landing page (dark theme, `.landing-page`, `.connect-button`, `.mint-button`, `.disconnect-button`, `.vision-grid`, Discord/GitHub/Twitter buttons). Nothing uses these class names yet. They are the best clue to the intended design: a landing page with connect-wallet and mint buttons.
- `src/App.test.js` is the only test. It checks that the "learn react" link is on the page.
- Empty placeholder files (0 bytes, not imported anywhere):
  - `src/pages/LandingPage.js`
  - `src/components/contracts/utils/ConnectButton.js`
  - `src/context/Web3Context.js`
  - `src/utils/alchemyConfig.js`
  - `src/Contracts/TuttiSapienzaABI.json` (an ABI is the description of a smart contract's functions; this one is empty, which is not valid JSON, so importing it will fail until it is filled in)

Installed but not yet used in any code: `ethers` 5, `alchemy-sdk`, `@alch/alchemy-web3` (blockchain libraries), `react-router-dom` 7 (page routing), and `tailwindcss` 4 with `postcss` and `autoprefixer` (CSS tooling; there is no Tailwind or PostCSS config file).

Deployment: nothing in the repo shows how or where this is deployed. There is no CI (automated checks) config, no hosting config and no `homepage` field in `package.json`.

## Commands

```bash
npm install          # one time: installs dependencies
npm start            # runs the site locally at http://localhost:3000
npm run build        # makes the production files in build/
```

```bash
npm test             # runs the tests in watch mode (keeps running until you quit)
CI=true npm test     # runs the tests once and exits
```

There is no separate lint command. ESLint (a tool that flags code problems) uses the `react-app` rules from `package.json` and reports in the terminal during `npm start` and `npm run build`. Do not run `npm run eject`; it cannot be undone.

## Conventions

- The repo has no contributor rules of its own. `README.md` is the unedited Create React App README: its commands are correct, but it says nothing about this project.
- Follow the folder layout the placeholders set up: pages in `src/pages/`, shared state in `src/context/`, helpers in `src/utils/`, contract ABIs in `src/Contracts/` (capital C; folder names are case-sensitive on Linux).
- When `App.js` stops showing the "Learn React" link, update `src/App.test.js` in the same change or the test will fail.

## Things to be careful about

- Unknowns: the repo contains no contract address, no blockchain network name (mainnet or a test network) and no ABI. Ask Sean for these; never invent them.
- Real money: once wallet and mint code exists, it can ask a visitor's wallet to sign transactions that spend real funds. Build and test against a test network first, and get Sean's go-ahead before pointing anything at a main network.
- Never put a wallet private key or seed phrase anywhere in this project.
- Create React App copies every environment variable whose name starts with `REACT_APP_` into the public JavaScript, so anyone visiting the site can read it. An Alchemy API key used here is therefore public; restrict it in the Alchemy dashboard. No environment variable names are defined yet and there is no `.env.example`.
- `.gitignore` ignores `.env.local` and the other `.env.*.local` files but not plain `.env`. Put keys in `.env.local`, or add `.env` to `.gitignore` first.
- Aging dependencies: Create React App is no longer maintained, `@alch/alchemy-web3` is a legacy library that pulls in web3 1.x, and `ethers` is on version 5 (version 6 changed many function names, so check which version an example was written for). Expect warnings from `npm install`. Do not run `npm audit fix --force`, which can break the build.
- The repo has a single commit (April 2025), and the project was only run through static reading when this guide was written, so the commands above are unverified on a fresh install.
