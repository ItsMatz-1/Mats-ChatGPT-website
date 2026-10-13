# APEX F1

A premium editorial Formula 1 season guide built with Next.js App Router, TypeScript, and Tailwind CSS. The first version focuses on season standings, the upcoming race and nearby calendar rounds, and the constructor grid.

## Run locally

```bash
cd work/apex-f1
npm install
npm run dev
```

Open http://localhost:3000. To make a production build, run `npm run build` and then `npm start`.

## Architecture

- `app/page.tsx` is a server-rendered homepage. It fetches the season once and passes the response into the editorial sections.
- `lib/f1.ts` contains the isolated Jolpica API client, data types, date formatter, and season aggregation.
- `app/globals.css` holds the responsive visual system and reduced-motion handling.
- The season is derived from the server's current calendar year rather than repeated as a fixed year.

## Data source and limits

Season calendars and championship standings come from the public [Jolpica-F1 API](https://github.com/jolpica/jolpica-f1), an Ergast-compatible API. The application requests the documented `/ergast/f1/{season}/driverStandings/1`, `/constructorStandings/1`, and `/races` endpoints in JSON format. Jolpica documents request throttling and does not provide live telemetry through these compatibility endpoints. Requests are made on the server and cached for one hour; if a request fails, sections show an unavailable state rather than guessed results. API records can be delayed and should be read as the season/round returned by the data provider, not as real-time race timing.

The public API currently requires no key, so there are no environment variables. Its usage limits and availability may change; check the Jolpica documentation before a high-traffic launch.

## Deployment

Import this project into Vercel and set the project root to `work/apex-f1` if deploying from the parent folder. Vercel detects Next.js automatically; no environment variables are required. For a standalone repository, move the contents of `work/apex-f1` to the repository root before deployment.

## Notes

The circuit silhouette is an illustrative graphic and is not labeled as a real circuit. Photography is loaded from Unsplash. This is an independent fan project and is not affiliated with Formula 1, the FIA, teams, or drivers.
