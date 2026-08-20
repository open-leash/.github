<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2563EB,45:4F46E5,100:7C3AED&height=230&section=header&text=Leash&fontSize=64&fontColor=ffffff&fontAlignY=38&desc=The%20antivirus%20for%20AI.&descSize=20&descAlignY=58" width="100%" alt="Leash" />

<p>
  <a href="https://openleash.com"><img src="https://img.shields.io/badge/Website-openleash.com-2563EB?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Website" /></a>
  <a href="https://docs.openleash.com"><img src="https://img.shields.io/badge/Docs-docs.openleash.com-4F46E5?style=for-the-badge&logo=readthedocs&logoColor=white" alt="Docs" /></a>
  <a href="https://github.com/open-leash/leash"><img src="https://img.shields.io/badge/Star-Leash-181717?style=for-the-badge&logo=github&logoColor=white" alt="Star Leash" /></a>
</p>

<h3>Control your AI.</h3>

Leash monitors AI-agent actions and stops dangerous operations before they cause damage.

</div>

---

## Start here

Leash's complete Personal Open Source product lives in one flagship repository:

| Repository | What it contains |
|---|---|
| ⭐ [`open-leash/leash`](https://github.com/open-leash/leash) | Engine, desktop and mobile clients, local proxy, provider sync worker, shared contracts, installers, and end-to-end development tooling. |
| 📚 [`open-leash/docs-web`](https://github.com/open-leash/docs-web) | Public installation, configuration, architecture, API, and self-hosting documentation. |

One clone gives contributors the full public runtime:

```text
apps/engine                 client-facing decision and audit runtime
apps/desktop                macOS and Windows desktop client
apps/mobile                 iOS and Android approval companion
apps/local-proxy            provider traffic enforcement relay
apps/provider-sync-worker   optional hosted-provider activity scheduler
apps/flow-viewer            local development flow inspection
packages/shared             versioned public contracts
```

## What Leash protects

- Destructive file, database, cloud, and tool actions
- Secrets, credentials, private data, and unsafe code
- Prompt injection and suspicious external instructions
- Rules that require approval or restrict agent behavior
- Runaway AI usage and unnecessary token spend

These capabilities ship as reviewed, first-party **Features** inside Leash Engine. They do not require per-Feature containers, image pulls, runtime secrets, or a third-party marketplace.

## Personal Open Source

Personal Open Source is free and local-first. It runs the real Engine and Postgres for one person, uses the user's own model-provider key, and does not require a Leash account or hosted control plane.

```bash
git clone https://github.com/open-leash/leash.git
cd leash
npm install
npm run dev:mode:individual-open-source
```

See the [documentation](https://docs.openleash.com) for platform requirements and installation options.

## Leash Cloud

Leash Cloud offers a managed Personal plan and a Business plan. Business administration, tenancy, identity-provider sync, billing, policy, dashboards, and CISO tooling are operated privately and are not published in the open-source repository.

The private Cloud services consume the public Engine; the public core never imports private Cloud packages.

## Contributing

Issues and pull requests belong in [`open-leash/leash`](https://github.com/open-leash/leash). Keeping the public product together makes changes across Engine, desktop, mobile, proxy, and contracts easier to review and test end to end.

If Leash is useful to you, star the flagship repository—it helps more people discover the project.

<div align="center">

<a href="https://github.com/open-leash/leash"><strong>github.com/open-leash/leash</strong></a>

</div>
