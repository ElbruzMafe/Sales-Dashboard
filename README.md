# Sales Dashboard

A small Next.js dashboard that charts mock yearly sales figures, with a minimum
threshold filter and a switch between bar, line and pie views.

I built this in an afternoon as a front-end assessment, and kept it around because
it is a compact example of how I lay out a React codebase: components split by
responsibility rather than by page, chart state kept in one place, and no state
library for something this size.

## Live demo

https://https-public.vercel.app

## Features

- Mock sales data for 2022, 2023 and 2024
- Filter rows out by a minimum sales threshold
- Switch between bar, line and pie charts without reloading
- Components organised along atomic design lines (`molecules/` for the filter
  input, `organisms/` for the chart plus its controls)
- Charts resize with the viewport via Recharts' `ResponsiveContainer`

## Tech stack

Next.js 15 (App Router), React 19, TypeScript, Tailwind CSS 4, Recharts.

## Running it

```bash
npm install
npm run dev
```

Then open http://localhost:3000 — the dashboard is the root route.

To check the production build:

```bash
npm run build
npm run start
```

## Project structure

```
.
├── app/
│   ├── layout.tsx              # root layout, pulls in globals.css
│   ├── page.tsx                # the dashboard route
│   └── globals.css             # Tailwind entry point
└── src/
    ├── components/
    │   ├── molecules/SalesFilter.tsx    # threshold input
    │   └── organisms/SalesChart.tsx     # chart type switch + rendering
    └── data/salesData.ts       # the mock dataset
```

`@/*` resolves to `src/*`, which is why the route files sit at the top level and
everything they import lives under `src/`.

## Known limitations

- The data is hardcoded in `src/data/salesData.ts`. There is no API layer, so
  "filtering" is an array filter, not a query.
- Only three data points, one series. The pie chart in particular is doing very
  little work with three slices.
- The threshold input accepts any number and silently ignores non-numeric input
  rather than showing a validation message.
- No tests.
