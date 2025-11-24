verify if `oci` is installed:
```bash
oci --version
```

generate API key:
```bash
oci setup config
```

`User OIDC`:
```bash
ocid1.user.oc1..aaaaaaaaw5ejkxx2hlwaadm5qktixtkikbgajdwxsx2q4qt4cwvzna5aelka
```

`Tenancy OCID`:
```bash
ocid1.tenancy.oc1..aaaaaaaatn5kz34nk6v5il3h7qmis5j4kl25pgolvtxrwq5kkkt3e2krbiba
```

`Region:` 
```bash
us-phoenix-1
```

then leave everything else is default

get the `api_public_key` just created:
```bash
cat ~/.oci <your_api_key_public.key>
```

copy this key, go to `cloud.oracle.com` > `Profile icon (top right)` > `User Settings` > `API Keys` > `Add API KEY`

Then paste the `api_public_key` just copied above

Done. Confirm if authenticated:
```bash
oci iam availability-domain list
```

if it returns a `json` > connected.