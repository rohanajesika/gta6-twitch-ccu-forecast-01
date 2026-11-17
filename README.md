[![make.fun](https://make.fun/badge/gta6-twitch-ccu-forecast-01.svg)](https://make.fun/c/gta6-twitch-ccu-forecast-01)
[![rank](https://make.fun/badge/gta6-twitch-ccu-forecast-01/rohanajesika/gta6-twitch-ccu-forecast-01/rank.svg)](https://make.fun/c/gta6-twitch-ccu-forecast-01)
[![reward](https://make.fun/badge/gta6-twitch-ccu-forecast-01/rohanajesika/gta6-twitch-ccu-forecast-01/reward.svg)](https://make.fun/c/gta6-twitch-ccu-forecast-01)

# GTA VI launch-day Twitch CCU forecaster

Entry for [Forecast GTA VI's launch-day Twitch viewers hour by hour](https://make.fun/c/gta6-twitch-ccu-forecast-01) on make.fun.

`main.ts` (Node 22, standard library only) reads one case file and writes,
for each of hours 2–24 of the release day (UTC), five quantiles of the Twitch
concurrent-viewer count in the "Grand Theft Auto VI" category.

## Approach

Past big game launches are the only honest prior for how a release day's
audience moves after its first hour. Each comparable launch in the case file
ships its own release-day hourly curve, so for every hour the program takes
kernel-weighted quantiles of the comparables' log ratios to their own hour-1
print — a comparable counts more when its hour-1 audience is close in size
to this case's hour-1 print (Gaussian kernel on log hour-1 size, width 1.0).
The median ratio is lightly smoothed across neighbouring hours; the outer
quantiles are left as measured so the spread stays honest. See the header
comment in `main.ts` for the validation numbers.

## Run locally

```sh
mkdir -p out && MAKEFUN_INPUT_DIR=<kit>/input MAKEFUN_OUTPUT_DIR=out node main.ts
```

Reads every `*.in` in the input directory and writes `<id>.out` per case.
Deterministic: two runs on the same case write identical bytes.

## License

MIT — see `LICENSE`.
