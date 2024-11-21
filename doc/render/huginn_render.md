- Open Dashboard

- `Create new project`

- Create PostgreeSQL database
    - `Create a new Service`
    - `PostgreeSQL`
    - Set `Name` (i.e. service name)
    - Set `Database` (i.e. database name; optional)
    - Set `User` (optional)
    - Set `Region` (optional)
    - Set `Instance type`
    - `Create database`

- Go to Github and fork huginn/huggin to your github account
    - Copy `.env.example` to `.env`
    - Edit `./.env`
        - Set `DOMAIN` to `0.0.0.0:3000` (alternatively, to an actual domain)
        - _I have set `ASSET_HOST` to the same value as `DOMAIN`_
        - Comment lines defining `DATABASE_ADAPTER`, `DATABASE_NAME`, `DATABASE_USERNAME`, and `DATABASE_PASSWORD` (_just in case_)
    - Edit `docker/postgres.env`
        - Set `POSTGRES_PORT_5432_TCP_ADDR` to the same value as `DATABASE_HOST`
        - Set `POSTGRES_PASSWORD` to the same value as `DATABASE_PASSWORD`
        - Set `POSTGRES_USER` to the same value as `DATABASE_USERNAME`
        - Set `HUGINN_DATABASE_PASSWORD` to the same value as `DATABASE_PASSWORD`
        - Set `HUGINN_DATABASE_USERNAME` to the same value as `DATABASE_USERNAME`
        - Set `HUGINN_DATABASE_NAME` to the same value as `DATABASE_NAME`
        - Optionally, set `DO_NOT_SEED` and `DO_NOT_CREATE_DATABASE` to `true` (_vide_ reference for more details)
    - Edit `docker/multi-process/Dockerfile` or `docker/single-process/Dockerfile`
        - This file contains two `RUN` commands which needs to be edited.
        - Remove `DATABASE_ADAPTER=postgresql` from both `RUN` command lines.
    - `Commit` & `Sync`

- Go back to Render.com and create Huginn service
    - `Create a new Service`
    - `Web service`
    - Set your forked github repository URL (i.e. `Source code`)
    - Set `Name` (i.e. service name)
    - Set `Language` to `Docker`
    - Set `Region` (optional)
    - Set `Dockerfile Path` to `./docker/multi-process/Dockerfile` or `./docker/single-process/Dockerfile`
    - Add the following `Environment Variables`:
        - DATABASE_ADAPTER = postgresql
        - DATABASE_HOST = _from steps above_
        - DATABASE_NAME = _from steps above_
        - DATABASE_PASSWORD = _from steps above_
        - DATABASE_USERNAME = _from steps above_
        - PORT = 3000

- Deploy

