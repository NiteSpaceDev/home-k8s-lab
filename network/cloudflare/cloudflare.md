# issues
The official cloudflare-tunnel charts are really bad, and the documentation around them is worse.

# What doesn't work:
* Some places show cloudflared, some show cloudflare.
    * Things go under cloudflare in the values
* Only specifying 'secretName'
    * Need both secretName and tunnelName
* Specifying tunnelId or account
    * This just makes it look for the cert.pem, which has no documentation on how to put it in a secret


# Setup
* Create a tunnel from the commandline:
    * cloudflared tunnel login
    * cloudflared tunnel create exampletunnel
* Create secret
    * kubectl create secret generic tunnel-credentials \
  --from-file=credentials.json=~/.cloudflared/uuid.json \
  --namespace=cloudflare
    * This can be wrapped into fluxcd w/ sops as needed - just make sure the secret has credentials.json
        * (not documented anywhere associated with the chart / values )