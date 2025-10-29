# Supabase CLI

## Develop locally, deploy to the Supabase Platform, and set up CI/CD workflows

---

The Supabase CLI enables you to run the entire Supabase stack locally, on your machine or in a CI environment. With just two commands, you can set up and start a new local project:

1. `supabase init` to create a new local project
2. `supabase start` to launch the Supabase services

## Installing the Supabase CLI[#](https://supabase.com/docs/guides/local-development/cli/getting-started?queryGroups=platform&platform=linux#installing-the-supabase-cli)

The CLI is available through [Homebrew](https://brew.sh/) and Linux packages.

```bash
brew install supabase/tap/supabase
```
Inside the folder where you want to create your project, run:

```bash
supabase init
```

This will create a new `supabase` folder. It's safe to commit this folder to your version control system.

Now, to start the Supabase stack, run:

```bash
supabase start
```

This takes time on your first run because the CLI needs to download the Docker images to your local machine. The CLI includes the entire Supabase toolset, and a few additional images that are useful for local development (like a local SMTP server and a database diff tool).

## Access your project's services[#](https://supabase.com/docs/guides/local-development/cli/getting-started?queryGroups=platform&platform=linux#access-your-projects-services)

Once all of the Supabase services are running, you'll see output containing your local Supabase credentials. It should look like this, with urls and keys that you'll use in your local project:
```bash
Started supabase local development setup.

         API URL: http://localhost:54321
          DB URL: postgresql://postgres:postgres@localhost:54322/postgres
      Studio URL: http://localhost:54323
     Mailpit URL: http://localhost:54324
        anon key: eyJh......
service_role key: eyJh......
```
The local development environment includes Supabase Studio, a graphical interface for working with your database.
### Default URL:
```bash
[http://localhost:54323](http://localhost:54323/)
```
<img width="1908" height="907" alt="image" src="https://github.com/user-attachments/assets/398ef543-a441-4685-a4d6-c56b565ab0f2" />
