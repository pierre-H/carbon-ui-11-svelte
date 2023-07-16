# Carbon UI 11 - Svelte (👷 WIP)

Adaptation of Carbon UI 11 for Svelte.
Inspired by [carbon-components-svelte](https://github.com/carbon-design-system/carbon-components-svelte).

## Why this project ?

Actually, [carbon-components-svelte](https://github.com/carbon-design-system/carbon-components-svelte) supports only Carbon UI 10 and [Carbon Charts Svelte](https://github.com/carbon-design-system/carbon-charts/tree/master/packages/svelte) use Carbon UI 11 which creates some conflits if they are both installed in the same project.

Also, Component properties of [carbon-components-svelte](https://github.com/carbon-design-system/carbon-components-svelte) are not very consistent (`size` prop has `sm` for `Input` and `small` for `Button`) which I don't realy like.

ℹ [carbon-components-svelte](https://github.com/carbon-design-system/carbon-components-svelte) is a great work and I thank @metonym for all he did in this project.

## Tools

I used only sveltekit packaging tool for the moment.
I must add tests and documentation.

## Components

| Component | Available | Tests | Documentation |
| --------- | --------- | ----- | ------------- |
| Accordion | ✅        | ❌    | ❌            |
| Button    | ✅        | ❌    | ❌            |

## Usage

Tested only with `sveltekit` (`svelte 4`).

You have to install Carbon styles : `npm install -S @carbon/styles`.

Also, you need to add sass and `npm add -D sass carbon-icons-svelte`

In you `+layout.svelte`, add :

```svelte
<script lang="ts">
	import '@carbon/styles/scss/_reset.scss';
</script>

<slot />
```

For styling customization, check the [`@carbon/styles` documentation](https://github.com/carbon-design-system/carbon/tree/main/packages/styles).

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

Everything inside `src/lib` is part of your library, everything inside `src/routes` can be used as a showcase or preview app.

## Building

To build your library:

```bash
npm run package
```

To create a production version of your showcase app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.

## Publishing

Go into the `package.json` and give your package the desired name through the `"name"` option. Also consider adding a `"license"` field and point it to a `LICENSE` file which you can create from a template (one popular option is the [MIT license](https://opensource.org/license/mit/)).

To publish your library to [npm](https://www.npmjs.com):

```bash
npm publish
```
