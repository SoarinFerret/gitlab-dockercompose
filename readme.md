# GitLab Docker-Compose using Lets-Encrypt

Very similar to other projects, but with the benefit of default settings for ADFS and setup for lets-encrypt DNS challenge instead of HTTP challenge.

## Setup & Installation

### 0. Prerequistes

The following items must be met:

* Install Git, Docker & Docker-Compose
* A Let's Encrypt Compatibale DNS provider

## 1. Clone the Repo

```
git clone https://github.com/SoarinFerret/gitlab-dockercompose.git
cd gitlab-dockercompose
```

## 2. Copy && Edit the necessary files

Any file with a `.default` name will need to be renamed and modified. The files you will create are:

* `.env`
* `gitlab.rb`
* `letsencrypt-domains.conf`
* `envfiles/gitlab.env`
* `envfiles/le-dns.env`
* `envfiles/postgres.env`
* `envfiles/runner.env`

### 2.1 .env

Main thing to edit in this file is the `GITLAB_HOSTNAME` and optionally any tags.

### 2.2 gitlab.rb

Lots of things to edit in this file. Here are a list of settings to search for and update:

  * `external_url`
  * `registry_external_url`
  * `gitlab_rails['smtp_enable']` (and if true:)
    * `gitlab_rails['smtp_address']`
    * `gitlab_rails['smtp_port']`
    * `gitlab_rails['smtp_user_name']`
    * `gitlab_rails['smtp_password']`
    * `gitlab_rails['smtp_domain']`
    * `gitlab_rails['smtp_authentication']`
    * `gitlab_rails['smtp_enable_starttls_auto']`
    * `gitlab_rails['smtp_tls']`
    * `gitlab_rails['gitlab_email_from']`
  * `gitlab_rails['omniauth_enabled']` (and if true:)
    * `gitlab_rails['omniauth_allow_single_sign_on']`
    * `gitlab_rails['omniauth_auto_sign_in_with_provider']`
    * `gitlab_rails['omniauth_block_auto_created_users']`
    * `gitlab_rails['omniauth_auto_link_saml_user']`
    * `gitlab_rails['omniauth_providers']`
  * `gitlab_rails['db_password']`
  * `nginx['ssl_certificate']`
  * `nginx['ssl_certificate_key']`
  * `registry_nginx['ssl_certificate']`
  * `registry_nginx['ssl_certificate_key']`

### 2.3 letsencrypt-domains.conf

Look [here](https://github.com/adferrand/docker-letsencrypt-dns) for how to update this file.

### 2.4 envfiles/gitlab.env

Optionally change the timezone.

### 2.5 envfiles/le-dns.env

Look [here](https://github.com/adferrand/docker-letsencrypt-dns) for how to update this file.

### 2.6 envfiles/postgres.env

Update the password to something unique and secure.

### 2.7 envfiles/runner.env

Change this to your GitLab hostname.

# Reference Links:

* https://github.com/mgcrea/docker-compose-gitlab-ce
* https://github.com/adferrand/docker-letsencrypt-dns
* https://smartersoft.nl/2017/11/configure-sso-with-gitlab/