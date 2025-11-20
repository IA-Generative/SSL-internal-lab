# SSL Internal Lab Certificate Flow

This repository stores two exports of a Mermaid diagram that describes how internal TLS certificates are obtained and consumed inside the lab network:

- **`Untitled diagram _ Mermaid Chart-2025-10-06-092613.svg`** – the source SVG export intended for high-quality viewing or further editing.
- **`Untitled diagram _ Mermaid Chart-2025-10-06-093124.png`** – a PNG export suitable for quick sharing or embedding where raster images are preferred.

## Diagram overview

### Why this diagram exists

- Provide a single visual reference for how DNS-01 certificates are requested, validated, and distributed inside the lab's private Kubernetes environment.
- Clarify the split between public-facing dependencies (Let's Encrypt and the DNS provider) and private consumers (gateway/ingress and internal users).
- Serve as an onboarding aid for engineers who need to understand the TLS path before operating or modifying the cluster network.

The diagram maps the DNS-01 certificate issuance path for a private Kubernetes cluster. Key components and swimlanes include:

- A public ACME authority (**Let's Encrypt**) initiating DNS-based validation against the **public DNS provider** (e.g., Cloudflare or OVH).
- A **DNS** zone boundary and a broader **Réseau_interne** grouping that contains a **Cluster_privé** segment for Kubernetes workloads.
- Internal automation (**cert-manager Kubernetes**) requesting certificates and delivering them to the **Ingress / Gateway** service that fronts internal applications via a **private IP**.
- **Utilisateurs internes** who rely on internal DNS resolution to reach the gateway.

## Certificate lifecycle steps

1. Let's Encrypt triggers DNS-01 validation and verifies the `_acme-challenge` TXT record through the public DNS service.
2. Once the challenge is acknowledged, the DNS provider signals validation success back to Let's Encrypt.
3. A validated certificate is issued to the in-cluster cert-manager, which applies it to the private ingress or gateway endpoint.
4. Internal users resolve the internal DNS entries that point at the gateway and consume services over the newly issued TLS certificate.

## Viewing the diagrams

Both exports can be opened directly in any modern web browser or image viewer. If you need to reference node labels or edge annotations programmatically, prefer the SVG version because the semantic labels are preserved in the markup.
