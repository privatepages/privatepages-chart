# chart readme

Create your values my.yaml

    ---
    privatepages:
        env:
            API_SECRET: secret
            HTTP_LISTEN: :8080
            LOG_LEVEL: error
    oauth2proxy:
        env:
            OAUTH2_PROXY_METRICS_ADDRESS: ":9090"
            # OAUTH2_PROXY_REDIS_CONNECTION_URL: redis://redis:6379
            # OAUTH2_PROXY_SESSION_STORE_TYPE: redis
            OAUTH2_PROXY_EMAIL_DOMAINS: "\\*"
            OAUTH2_PROXY_PROVIDER: github
            OAUTH2_PROXY_SCOPE: "user:email read:org"
            OAUTH2_PROXY_GITHUB_ORG: yourorg
            # OAUTH2_PROXY_GITHUB_TEAM: yourteam
            OAUTH2_PROXY_REDIRECT_URL: https://your.pages/oauth2/callback
            OAUTH2_PROXY_CLIENT_ID: xxxx
            OAUTH2_PROXY_CLIENT_SECRET: zzzz
            OAUTH2_PROXY_COOKIE_SECRET: yyyy
            # https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/overview
            # dd if=/dev/urandom bs=32 count=1 2>/dev/null | base64 | tr -d -- '\n' | tr -- '+/' '-_'; echo
    ingress:
        enabled: true
        . . .

Use it

    helm upgrade  pp . -i --values my.yaml -n privatepages
