# cart

Checkout's cart API. Owned by `checkout`.

## Layout

    port.yml       service identity — Port builds the catalog entry from this
    chart/         the Helm chart: one definition of what this service looks like
    envs/          one values file per environment

## Deploying to a new environment

Add a directory under `envs/`:

    envs/prod/values.yaml

        service: cart
        team: checkout
        environment: checkout-prod
        replicas: 4

Open a pull request. On merge the platform's ApplicationSet notices the new
file and creates an ArgoCD Application for it.

The environment named must already exist — request it from Port's self-service
hub first. It is what created the namespace, its quota and its ArgoCD project.

## What we own, and what we do not

We own `chart/` and `envs/` — how this service is shaped and sized in each
environment.

We do not own where it lands. The ArgoCD project for our environment only
permits `Kubernis/checkout-*` as a source and only permits that one namespace
as a destination. These manifests cannot reach another team's namespace, even
by mistake.
