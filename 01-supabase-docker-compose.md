# Supabase Docker Compose

## Installing and running Supabase

For updated installation checkout Supabase official documention first: https://supabase.com/docs/guides/self-hosting/docker#accessing-supabase-studio

Follow these steps to start Supabase on your machine:

```bash
# Get the code using git sparse checkout
git clone --filter=blob:none --no-checkout https://github.com/supabase/supabase
cd supabase
git sparse-checkout set --cone docker && git checkout master
cd ..

# Make your new supabase project directory
mkdir supabase-project

# Tree should look like this
# .
# ├── supabase
# └── supabase-project

# Copy the compose files over to your project
cp -rf supabase/docker/* supabase-project

# Copy the fake env vars
cp supabase/docker/.env.example supabase-project/.env

# Switch to your project directory
cd supabase-project

# Pull the latest images
docker compose pull

# Start the services (in detached mode)
docker compose up -d
```

If you are using rootless docker, edit `.env` and set `DOCKER_SOCKET_LOCATION` to your docker socket location. For example: `/run/user/1000/docker.sock`. Otherwise, you will see an error like `container supabase-vector exited (0)`.

After all the services have started you can see them running in the background:

```bash
docker compose ps
```

### Accessing Supabase Studio[#](https://supabase.com/docs/guides/self-hosting/docker#accessing-supabase-studio)

You can access Supabase Studio through the API gateway on port `8000`. For example: `http://<your-ip>:8000`, or [localhost:8000](http://localhost:8000/) if you are running Docker locally.

You will be prompted for a username and password. By default, the credentials are:

- Username: `supabase`
- Password: `this_password_is_insecure_and_should_be_updated`

You should change these credentials as soon as possible using the [instructions](https://supabase.com/docs/guides/self-hosting/docker#dashboard-authentication) below.

### Accessing the APIs[#](https://supabase.com/docs/guides/self-hosting/docker#accessing-the-apis)

Each of the APIs are available through the same API gateway:

- REST: `http://<your-ip>:8000/rest/v1/`
- Auth: `http://<your-domain>:8000/auth/v1/`
- Storage: `http://<your-domain>:8000/storage/v1/`
- Realtime: `http://<your-domain>:8000/realtime/v1/`
