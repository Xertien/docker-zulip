# 1. ENV

### `DB_HOST`

**Description:** Hostname of the PostgreSQL server.
**Example:** `database` (Docker container name)

---

### `DB_HOST_PORT`

**Description:** PostgreSQL port.
**Example:** `5432`

---

### `DB_USER`

**Description:** PostgreSQL username used by Zulip.
**Example:** `zulip`

---

### `SECRETS_postgres_password`

**Description:** PostgreSQL password.
**Example:** `supersecretpgpass`

---

# 2. Network / HTTPS / SSL

### `DISABLE_HTTPS`

**Description:**

* `true` = Zulip serves over HTTP (development)
* `false` = HTTPS required

**Example:** `true`

---

### `SSL_CERTIFICATE_GENERATION`

**Description:**

* `self-signed` = generate a self-signed certificate
* `manual` = you provide your own certificates
* `disabled` = no certificate generation

**Example:** `self-signed`

---

# 3. Cache / File Queue / Redis / RabbitMQ / Memcached

### `SETTING_MEMCACHED_LOCATION`

**Description:** Memcached address.
**Example:** `"memcached:11211"`

---

### `SETTING_RABBITMQ_HOST`

**Description:** RabbitMQ host.
**Example:** `rabbitmq`

---

### `SETTING_REDIS_HOST`

**Description:** Redis host.
**Example:** `redis`

---

### `SECRETS_rabbitmq_password`

**Description:** RabbitMQ password.
**Example:** `rabbitmq123`

---

### `SECRETS_memcached_password`

**Description:** (Rarely used) Memcached password.
**Example:** `memcachedpass`

---

### `SECRETS_redis_password`

**Description:** Redis password if authentication is enabled.
**Example:** `redissecret`

---

# 4. Email (SMTP)

### `SETTING_EMAIL_HOST`

**Description:** SMTP server address.
**Example:** `smtp.gmail.com`

---

### `SETTING_EMAIL_HOST_USER`

**Description:** SMTP username.
**Example:** `bot@example.com`

---

### `SECRETS_email_password`

**Description:** SMTP password.
**Example:** `g-app-password`

---

### `SETTING_EMAIL_PORT`

**Description:** SMTP port.
**Example:** `587`

---

### `SETTING_EMAIL_USE_SSL`

**Description:** Disable SSL?
**Example:** `false`

---

### `SETTING_EMAIL_USE_TLS`

**Description:** Enable TLS?
**Example:** `true`

---

# 5. Zulip Server Ownership

### `SETTING_EXTERNAL_HOST`

**Description:** Public domain of your Zulip instance.
**Example:** `chat.example.com`

---

### `SETTING_ZULIP_ADMINISTRATOR`

**Description:** Default admin email.
**Example:** `admin@example.com`

---

### `SECRETS_secret_key`

**Description:** Django secret key (must be generated once).
**Example:** `longrandomsecretkeygoeshere`

---

### `LOADBALANCER_IPS`

**Description:** Internal IPs of your reverse proxy.
**Example:** `172.18.0.5,172.18.0.6`

---

# 6. Authentication – Google SSO

### `SETTING_SOCIAL_AUTH_GOOGLE_KEY`

**Description:** Google OAuth2 Client ID.
**Example:** `1234567890-abc123.apps.googleusercontent.com`

---

### `SECRETS_social_auth_google_secret`

**Description:** Google OAuth2 Client Secret.
**Example:** `GOOGLE_SECRET_123456`

---

# 7. Authentication – SAML (Keycloak)

### `SETTING_SOCIAL_AUTH_SAML_ORG_INFO`

**Description:**
Public information for the Service Provider (Zulip) in SAML metadata.

**Format:** Python dict

**Example:**

```json
{"fr-FR": {"displayname": "Example Chat", "name": "example-chat", "url": "https://chat.example.dev"}}
```

---

### `SETTING_SOCIAL_AUTH_SAML_ENABLED_IDPS`

**Description:**
Your SAML IdP (Keycloak) configuration.

**Full example:**

```json
{
  "keycloak": {
    "entity_id": "https://auth.example.com/realms/phenix-private",
    "url": "https://auth.example.com/realms/phenix-private/protocol/saml",
    "display_name": "Example Auth",
    "attr_email": "email",
    "attr_username": "email",
    "attr_first_name": "first_name",
    "attr_last_name": "last_name",
    "attr_user_permanent_id": "email",
    "auto_signup": true
  }
}
```

Keycloak’s public certificate must be mounted at:
`/etc/zulip/saml/idps/keycloak.crt`

---

### Example `.env`

```env
POSTGRES_USER=zulip
POSTGRES_PASSWORD=supersecretpg
SECRETS_EMAIL_PASSWORD=gmail-app-pass
RABBITMQ_DEFAULT_PASS=rabbitpass
MEMCACHED_PASSWORD=
REDIS_PASSWORD=
ZULIP_SECRET_KEY=ZULIP_SECRET_123456
SOCIAL_AUTH_GOOGLE_SECRET=GOOGLESECRET123
LOADBALANCER_IPS=172.18.0.5

SETTING_EXTERNAL_HOST=chat.example.com
SETTING_ZULIP_ADMINISTRATOR=admin@example.com

SETTING_EMAIL_HOST=smtp.gmail.com
SETTING_EMAIL_HOST_USER=bot@example.com
SETTING_EMAIL_PORT=587
SETTING_EMAIL_USE_SSL=false
SETTING_EMAIL_USE_TLS=true

SETTING_SOCIAL_AUTH_GOOGLE_KEY=12345.apps.googleusercontent.com

SETTING_SOCIAL_AUTH_SAML_ORG_INFO={"fr-FR": {"displayname": "Example Chat", "name": "example-chat", "url": "https://chat.example.com"}}
SETTING_SOCIAL_AUTH_SAML_ENABLED_IDPS={"keycloak": {"entity_id": "https://auth.example.com/realms/phenix-private", "url": "https://auth.example.com/realms/phenix-private/protocol/saml", "display_name": "Phénix Auth", "attr_email": "email", "attr_username": "email", "attr_first_name": "first_name", "attr_last_name": "last_name", "attr_user_permanent_id": "email", "auto_signup": true}}

ZULIP_AUTH_BACKENDS=EmailAuthBackend,zproject.backends.SAMLAuthBackend
DISABLE_HTTPS=true
SSL_CERTIFICATE_GENERATION=self-signed
```
