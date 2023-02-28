# privatepages-chart

Helm chart for installing [privatepages](https://github.com/privatepages/privatepages) on your k8s cluster

oauth2-proxy documentation [https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/overview](https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/overview)


## Installation

Create your values file, for example: my.yaml

    ---
    privatepages:
      env:
        API_SECRET: secret!
        # dd if=/dev/urandom bs=32 count=1 2>/dev/null | base64 | tr -d -- '\n' | tr -- '+/' '-_'; echo
        LOG_LEVEL: error
        HTTP_UPLOAD_MAX_SIZE: 10 # Mb
    oauth2proxy:
      env:
        OAUTH2_PROXY_GITHUB_ORG: yourorg
        # OAUTH2_PROXY_GITHUB_TEAM: yourteam
        OAUTH2_PROXY_REDIRECT_URL: https://your-privatepages-domain.tld/oauth2/callback
        OAUTH2_PROXY_CLIENT_ID: xxxx
        OAUTH2_PROXY_CLIENT_SECRET: zzzz
        # client id and secret from your github app https://github.com/settings/applications/new
        OAUTH2_PROXY_COOKIE_SECRET: yyyy
        # https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/overview
        # dd if=/dev/urandom bs=32 count=1 2>/dev/null | base64 | tr -d -- '\n' | tr -- '+/' '-_'; echo
    ingress:
      enabled: true
      annotations:
        kubernetes.io/ingress.class: nginx
        kubernetes.io/tls-acme: "true"
      hosts:
        - host: your-privatepages-domain.tld
          paths:
            - path: /
              pathType: Prefix
        tls:
          - secretName: your-privatepages-domain.tld-tls
            hosts:
              - your-privatepages-domain.tld
    # example

Use it

    # from chart src
    helm upgrade privatepages . -i --values my.yaml -n privatepages

    # from chart release
    WIP


## Oauth

Create github oauth app https://github.com/settings/applications/new

For logout remove cookies and revoke access of github app https://github.com/settings/applications or use /oauth2/sign_out

Also see [docs](https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/overview)


## Ingress

To terminate TLS, I recommend using a [cert-manager](https://cert-manager.io/docs/usage/ingress)


## To Do

* API_SECRET store in k8s secret 
* add cf schema headers !! (to many redirects)
