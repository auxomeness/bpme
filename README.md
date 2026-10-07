# Node + React Boilerplate

An npm workspace starter for an Express backend and a React + Vite frontend, written in JavaScript. It provides the project structure and basic startup configuration without sample routes, business logic, database models, or demo UI. MongoDB is an optional documented extension point.

## Requirements

- Node.js 20.19 or newer
- npm 10 or newer

## Check Node before the exam

Open a terminal and check that both commands work:

```bash
node --version
npm --version
```

Use Node.js `20.19.0` or newer and npm `10` or newer. The repository's `.nvmrc` records the minimum tested Node version. If `node` or `npm` is not recognized, or Node is older than `20.19.0`, install or update Node.js from the [official Node.js download page](https://nodejs.org/en/download). Then close and reopen the terminal and run both checks again. npm is installed with Node.js.

Before the timed exam, from this project folder, install dependencies and run the checks once:

```bash
npm ci
npm run lint
npm test
npm run build
```

If those commands pass, the project is ready. During the exam, start both apps with `npm run dev`.

## Get started

```bash
npm ci
npm run dev
```

The backend runs at `http://localhost:3000`; the Vite app runs at `http://localhost:5173`. No API routes or frontend screens are included yet; add your features in the provided structure.

Environment files are optional for local defaults. To customize settings, copy `backend/.env.example` to `backend/.env` and `frontend/.env.example` to `frontend/.env` (PowerShell: use `Copy-Item backend/.env.example backend/.env` and `Copy-Item frontend/.env.example frontend/.env`).

## Scripts

| Command | Purpose |
| --- | --- |
| `npm run dev` | Run backend and frontend together with reload / HMR |
| `npm run build` | Check backend syntax and build the frontend |
| `npm run lint` | Run ESLint across both workspaces |
| `npm test` | Run workspace tests; succeeds when no tests have been added yet |

Run a workspace by itself with `npm run dev --workspace backend` or `npm run dev --workspace frontend`.

## Project structure

```text
node-react-boilerplate/
├── backend/
│   ├── src/
│   │   ├── controllers/     # Handle HTTP requests and responses
│   │   ├── models/          # Database schemas/models (optional)
│   │   │   └── README.md    # Notes on adding MongoDB later
│   │   ├── routes/          # Define API paths and connect them to controllers
│   │   ├── services/        # Hold business rules and application logic
│   │   ├── validators/      # Check incoming request data
│   │   └── server.js        # Configure and start the Express server
│   ├── .env.example         # Backend environment variable template
│   └── package.json         # Backend dependencies and commands
├── frontend/
│   ├── src/
│   │   ├── App.jsx          # Root React component; empty starting point
│   │   └── main.jsx         # Mounts the React app in the browser
│   ├── .env.example         # Frontend environment variable template
│   ├── index.html           # HTML document Vite serves
│   ├── package.json         # Frontend dependencies and commands
│   └── vite.config.js       # Vite and React development/build settings
├── .nvmrc                  # Suggested Node.js version
├── eslint.config.js        # Shared JavaScript lint rules
├── package-lock.json       # Locked dependency versions for npm ci
├── package.json            # npm workspaces and shared commands
└── README.md               # Setup and project guide
```

### Backend request flow

When you add an API feature, keep each layer focused:

1. **Route** matches the HTTP method and URL, then applies the validator and controller.
2. **Validator** checks that request parameters and body data have the expected shape.
3. **Controller** reads the request, calls the service, and builds the HTTP response.
4. **Service** implements the feature's business rules. It can call a model when persistence is needed.
5. **Model** defines how application data is stored and retrieved. MongoDB models belong here if MongoDB is selected.

The `routes/`, `controllers/`, `services/`, and `validators/` folders are empty placeholders. `models/` contains a short note about adding database support later. The starter has no API routes, sample business logic, or active database connection.

### Frontend purpose

- **`main.jsx`** starts React and attaches the root component to the `root` element in `index.html`.
- **`App.jsx`** is the empty top-level component where the app's screens can be added.
- **`vite.config.js`** configures Vite's React support, development server, and production build.

### Root configuration

- **Root `package.json`** defines the backend and frontend as npm workspaces and provides commands to run, build, lint, and test both together.
- **`package-lock.json`** makes installs reproducible; use `npm ci` to install the locked dependencies.
- **`.nvmrc`** identifies the Node.js version used as the setup baseline.
- **`eslint.config.js`** applies the shared JavaScript lint rules to the project.

## Environment variables

The API uses `PORT` and `FRONTEND_ORIGIN`. The frontend can use `VITE_API_URL` when it starts making API requests. Copy each workspace's `.env.example` to `.env` only when you want to override the local defaults.

## Adding MongoDB later

Install Mongoose when the project needs persistence, add a `MONGODB_URI` to the backend environment, implement connection lifecycle handling, and add schemas under `backend/src/models/`. The starter does not connect to a database.
