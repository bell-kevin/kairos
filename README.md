<a name="readme-top"></a>

# kairos

https://idealtime.org

*Find the opportune hour.*

The Greeks had two words for time. **Chronos** is the kind that passes. **Kairos** (καιρός) is the opening - the right, critical moment for the thing. In archery it named the aperture the arrow had to pass through.

Weather apps answer *"what will the weather be?"* kairos answers the question you actually had: ***"when should I do it?"***

Give it a place, and it scores **every hour of the coming week** against what each activity genuinely needs - temperature, wind, rain chance, humidity, UV, cloud cover, daylight, dry spells, even moonlight - then shows you the openings.

## What it can express that a forecast can't

Every condition is one shape: a **trapezoid band** - full score inside the ideal range, tapering to zero at the hard bounds, zero beyond. That single shape, applied to both measured and *derived* metrics, covers a surprising amount of everyday judgment:

- **Mow the lawn** wants at least 3 *dry hours behind* the current hour (6+ ideal) - wet grass clumps. A look-**back** constraint.
- **Wash the car** wants 8+ *dry hours ahead* (24 ideal) - don't wash before a storm. A look-**ahead** constraint.
- **Line-dry laundry** actually *wants* wind: ideal 4–15 mph. An inverted band.
- **Golden-hour photos** want the sun between −3° and +5° altitude *and* 15–60% cloud, because some clouds make the light. Two mid-range bands.
- **Stargazing** wants astronomical darkness (sun below −18°), low cloud, *and* a dim moon - a full moon washes out the sky.
- **Sleep with the windows open** is scored too. Windows cross midnight freely.

Hour scores combine as a weighted geometric mean, so one dealbreaker zeroes an hour while everything else blends smoothly - and the app always tells you **which constraint is the limiting factor** ("wind 22 mph - over ideal"). No black boxes.

## Features

- **This week's openings** - one line per activity: its single best window and score, with a **one-click `.ics` export** to drop the window straight onto your calendar.
- **The week chart** - 7 days × 24 hours. Ink density is fit; night and twilight hours are slate-shaded (the chart *shows* darkness — you can see sunrise and sunset move through the week); best windows get a brass aperture ring.
- **The "why" panel** - tap any hour for every constraint's value, sub-score, and the limiting factor.
- **Ten editable presets** and fully custom activities: every bound is yours to change, in °F or °C.
- **Export / import** your activity library as JSON - share your definition of a perfect running hour.
- **Local-first.** Your place, activities, and cached forecast live in `localStorage` and never leave the browser. No accounts, no tracking, no backend. If the network drops, you get your last saved forecast, labeled as such.

## The astronomy is computed on your device

- **Sun altitude** per hour from the NOAA low-accuracy solar equations (Spencer 1971) - verified to within ±3 minutes of published sunrise/sunset times. Daylight, twilight, golden hour, and astronomical darkness all derive from it.
- **Moon illumination** from the mean synodic cycle - accurate to a few hours of phase, plenty to tell a full moon from a new one.

No astronomy library, no API for sun/moon - about 120 lines of commented math in [`src/lib/solar.ts`](src/lib/solar.ts) and [`src/lib/lunar.ts`](src/lib/lunar.ts).

## Stack

Vite + React + TypeScript, strict mode. **Zero runtime dependencies beyond `react` and `react-dom`.** No UI framework, no chart library, no date library, no astronomy library. Hand-rolled CSS with custom properties; automatic dark mode; `prefers-reduced-motion` respected.

Weather comes from [Open-Meteo](https://open-meteo.com/) - a keyless, CORS-open forecast API whose server software is itself AGPL-licensed free software, which felt like the right neighbor for this project. Forecast data is CC BY 4.0, credited in the app footer.

## Run it

```sh
npm install
npm run dev      # local development
npm run build    # type-check + production build → dist/
```

The build is fully static - host `dist/` anywhere. Built and published via [bolt.new](https://bolt.new) / Netlify; no environment variables, no server, no API keys.

## License: AGPL-3.0-or-later

kairos is free software under the [GNU Affero General Public License v3](LICENSE). The AGPL is chosen deliberately for a network-served tool: if you run a modified kairos for others over a network, they're entitled to your source. Weather belongs to everyone; so should the tools for reading it.

## Roadmap

- Moon *altitude* (rise/set), so a bright moon below the horizon doesn't dent a stargazing score
- PWA install + service-worker offline shell
- Multiple saved places
- Warning-type activities (frost watch for gardeners: alert when a night dips below 36 °F)
- Shareable read-only links encoding an activity in the URL fragment

## Data & credits

- Weather: [Open-Meteo.com](https://open-meteo.com/), CC BY 4.0
- Solar math: NOAA Global Monitoring Laboratory solar calculator equations
- Type: [Bricolage Grotesque](https://github.com/ateliertriay/bricolage) and [IBM Plex Mono](https://github.com/IBM/plex), both SIL OFL

--------------------------------------------------------------------------------------------------------------------------
== We're Using GitHub Under Protest ==

This project is currently hosted on GitHub.  This is not ideal; GitHub is a
proprietary, trade-secret system that is not Free and Open Souce Software
(FOSS).  We are deeply concerned about using a proprietary system like GitHub
to develop our FOSS project. I have a [website](https://bellKevin.me) where the
project contributors are actively discussing how we can move away from GitHub
in the long term.  We urge you to read about the [Give up GitHub](https://GiveUpGitHub.org) campaign 
from [the Software Freedom Conservancy](https://sfconservancy.org) to understand some of the reasons why GitHub is not 
a good place to host FOSS projects.

If you are a contributor who personally has already quit using GitHub, please
email me at **kevinBell@Linux.com** for how to send us contributions without
using GitHub directly.

Any use of this project's code by GitHub Copilot, past or present, is done
without our permission.  We do not consent to GitHub's use of this project's
code in Copilot.

![Logo of the GiveUpGitHub campaign](https://sfconservancy.org/img/GiveUpGitHub.png)

<p align="right"><a href="#readme-top">back to top</a></p>
