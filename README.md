# cart

Checkout's cart API. Owned by `checkout`.

## Where things are

    port.yml    service identity — Port builds the catalog entry from this
    deploy/     Kubernetes manifests, deployed by ArgoCD

## How this gets deployed

Nothing here configures ArgoCD. The platform's fleet repo holds a declaration
naming this repo, this path and the target environment; an ApplicationSet turns
that into an Application inside the tenant's own ArgoCD project.

That project only permits `Kubernis/checkout-*` as a source and only permits
`checkout-dev` as a destination — so these manifests cannot reach another team's
namespace even by accident.

We own what is inside `deploy/`. The platform owns where it lands.
