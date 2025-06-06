# Developer setup
The app has two distinct components, the Go backend and the VueJS frontend. In the dev environment, both are run independently.


### Pre-requisites
- `go`
- `nodejs` (if you are working on the frontend) and `yarn`
- Postgres database. If there is no local installation, the demo docker DB can be used for development (`docker compose up demo-db`)


### First time setup
`git clone https://github.com/knadh/listmonk.git`. The project uses go.mod, so it's best to clone it outside the Go src path.

1. Copy `config.toml.sample` as `config.toml` and add your config.
2. `make dist` to build the listmonk binary. Once the binary is built, run `./listmonk --install` to run the DB setup. For subsequent dev runs, use `make run`.

> [mailhog](https://github.com/mailhog/MailHog) is an excellent standalone mock SMTP server (with a UI) for testing and dev.


### Running the dev environment
You can run your dev environment locally or inside containers.

After setting up the dev environment, you can visit `http://localhost:8080`.


1. Locally
- Run `make run` to start the listmonk dev server on `:9000`.
- Run `make run-frontend` to start the Vue frontend in dev mode using yarn on `:8080`. All `/api/*` calls are proxied to the app running on `:9000`. Refer to the [frontend README](https://github.com/knadh/listmonk/blob/master/frontend/README.md) for an overview on how the frontend is structured.

2. Inside containers (Using Makefile)
- Run `make init-dev-docker` to setup container for db.
- Run `make dev-docker` to setup docker container suite.
- Run `make rm-dev-docker` to clean up docker container suite.

3. Inside containers (Using devcontainer)
- Open repo in vscode, open command palette, and select "Dev Containers: Rebuild and Reopen in Container".

It will set up db, and start frontend/backend for you.


# Production build
Run `make dist` to build the Go binary, build the Javascript frontend, and embed the static assets producing a single self-contained binary, `listmonk`
