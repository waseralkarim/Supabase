# Supabase Studio/WebUI Authentication

Supabase doesn't come with build-in authentication setup. So, if you want to setup authentication you can follow this guide.

### Install `htpasswd` on Ubuntu/Debian

Run:

```bash
sudo apt update
sudo apt install apache2-utils -y
```

---

### Then create the password file:

```bash
sudo htpasswd -c /etc/nginx/.htpasswd admin
```

It will prompt:

```
New password:
Re-type new password:
Adding password for user admin
```

---

### Verify file:

```bash
cat /etc/nginx/.htpasswd
```

You’ll see something like:

```
admin:$apr1$k9s8d...$2rE4xG2O9bEkdYAfFZ5c91
```

Then in your nginx config file add it:

```bash
# Supabase Studio UI
    location / {
        auth_basic "Restricted Area";
        auth_basic_user_file /etc/nginx/.htpasswd;
```
