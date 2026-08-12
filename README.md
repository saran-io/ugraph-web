# ugraph-web

Marketing and roadmap site for [`ugraph`](../ugraph) — the CLI that builds an
agent-navigable knowledge base from a YouTube channel.

Zero build step. Three static pages plus one stylesheet.

```
ugraph-web/
├─ index.html       overview: what ugraph is, the pipeline, the format, the CLI
├─ backlog.html     product backlog — now / next / later / considering / declined
├─ changelog.html   versions, what shipped in 0.1.0, and the versioning policy
└─ assets/
   └─ style.css     the whole design system
```

## Run it

Open `index.html` directly, or serve the folder:

```sh
python3 -m http.server 4173 --directory .
# → http://localhost:4173
```

## Deploy

GitHub Pages from [`saran-io/ugraph-web`](https://github.com/saran-io/ugraph-web)
(`main` / root), custom domain **https://ugraph.build**.

The folder is the artifact — no build, no dependencies. The only network request
is the Archivo / JetBrains Mono stylesheet from Google Fonts; the CSS falls back
to the system UI and mono stacks if that is blocked.

### DNS (GoDaddy → GitHub Pages)

Apex `A` records: `185.199.108.153` `185.199.109.153` `185.199.110.153` `185.199.111.153`  
`www` `CNAME` → `saran-io.github.io`  
Repo root must contain a `CNAME` file with `ugraph.build`.

If GoDaddy Website Builder / domain forwarding (`dpsAws`) is attached, disconnect
it in the GoDaddy product UI first — those records are immutable via the DNS API.

### Daily journal

Posts live in `journal/`. Add a dated HTML file, link it from `journal/index.html`,
ship. Keep entries short: what shipped, what’s next, one honest blocker.

## Licence

The site states the base tool as **Apache-2.0**, with commercial support available.
If that changes, update the hero chip and footer on all three pages plus the closing
band on `index.html`.

## Editing notes

- **Design tokens** live in the `:root` block at the top of `assets/style.css`.
  The palette is a CLI status palette: mint `--edge` = verified, amber `--amber` =
  pending, violet `--violet` = model-driven, rose `--rose` = failing.
- **Nav, footer and the mobile-menu script are duplicated** across the three pages
  on purpose — that is the cost of having no build step. Change one, change all three.
- **Every claim on these pages is sourced from the `ugraph` package itself** (command
  surface, page types, typed edges, ledger stages, export formats, backends). If the
  code changes, the pages need updating. Illustrative content — the terminal
  transcripts and the graph figure — is labelled as such.
- **The backlog is a plan, not a record.** Only items marked `shipped` exist today.
  Keep that distinction intact when editing.
