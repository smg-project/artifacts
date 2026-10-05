# smg-project/artifacts

Evidence that would clutter the code repositories: vendor conformance reports, benchmark outputs and other raw
artifacts referenced from issues and roadmap updates in [smg-project/smg](https://github.com/smg-project/smg).

- `verification/<date>-<image>/` — official vendor verifier runs against a released SMG image; each folder has a README
  with the stack, the invocation and the numbers.
- `bellwether/<command>/<date>/` — reports from [bellwether](https://github.com/smg-project/bellwether): coverage matrices (`gaps`) and, later, verify reports; each folder has a README with the sources, the command and the headline.
