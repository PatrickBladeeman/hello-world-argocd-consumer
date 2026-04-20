Hello World Argo CD Consumer
============================

This repo is the consumer-side GitOps input for the KubePlus Hello World
multi-tenancy example.

What this repo manages
----------------------

- Tenant instances of `HelloWorldService`
- The Argo CD `Application` that syncs those tenant instances

What this repo does not manage
------------------------------

- KubePlus installation
- Argo CD installation
- Provider-side creation of the `HelloWorldService` API

Quick start
-----------

1. Apply the Argo CD application:

   `kubectl apply -f argocd-consumer-app.yaml -n argocd`

2. Verify the initial tenant:

   `kubectl get helloworldservices.platformapi.kubeplus -n default`
   `kubectl get pods -n hs1`

3. Test GitOps scaling:

   - edit `tenants/hs1.yaml` and change `replicas` from `1` to `2`
   - commit and push
   - wait for Argo CD to sync
   - `kubectl get pods -n hs1`
