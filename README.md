# create-svelte

This is a repo to reproduce a potential bug in SvelteKit. One of the stated use cases for the `config.kit.paths.assets` config var is for the case where assets will be hosted on a separate domain to the site itself.

The docs state:

> If a value for `config.kit.paths.assets` is specified, it will be replaced with `'/_svelte_kit_assets'` during `vite dev` or `vite preview`, since the assets don't yet live at their eventual URL.

That is what happens with `vite dev` but not with `vite preview`.

To reproduce, clone this repo then:

```bash
npm i
npm run build
npm run preview
```

Observe that the site attempts to load assets from 'https://example.com' instead of '/\_svelte_kit_assets' even though the assets _are_ emitted at that path (e.g. `http://localhost:4173/_svelte_kit_assets/favicon.png`).
