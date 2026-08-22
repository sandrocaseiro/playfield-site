# playfield-site

The public face of [Playfield](https://github.com/sandrocaseiro/playfield): the
website, and the releases people download.

**Nothing here is edited per release.** The app's private repository publishes a
release to *this* repository — the installers as assets, the readable changelog
as the body — and that release event rebuilds the site. The download buttons and
the changelog page are read from this repository's Releases through the GitHub
API at build time, so they are always whatever the releases currently say.

To correct a changelog, edit the release on GitHub. The site rebuilds itself.

## Running it

```
npm install
npm run dev      # localhost:4321/playfield-site/
npm run build    # into dist/
```

The build reaches GitHub for the release list. Without a network, or before the
first release exists, it builds anyway with an empty download page — that is
deliberate, because the site has to go up before there is anything to download.

`RELEASES_REPO` overrides which repository it reads, which is the only way to
see the changelog page populated before this one has releases of its own.

`PUBLIC_GA_MEASUREMENT_ID` is the Google Analytics 4 measurement ID (`G-…`).
It is only read in a production build, so `npm run dev` never reports, and a
build without it ships no analytics at all and still deploys. On GitHub it lives
as a repository *variable*, not a secret — the ID is public by nature, it is in
the page source of every visit.

## What is where

| | |
|---|---|
| `src/pages/` | The three pages — landing, download, changelog |
| `src/lib/releases.ts` | The GitHub read, and everything derived from a release |
| `src/styles/tokens.css` | The application's own tokens, copied, plus what a page needs |
| `src/assets/shots/` | Screenshots of the real screens, from the app's test suite |
| `.github/workflows/deploy.yml` | Builds and publishes to Pages on a push or a release |

The screenshots are of the seed library the app falls back to outside its own
shell — public catalogue artwork and invented playtimes, no account data.
