# FlytWERX ACS Data

Production data source for the FlytWERX ACS Maneuver Standards Checker.

## What is included

This repository is complete for the current **Private Pilot / Airplane / ASEL** checker experience and is designed so future certificate/rating datasets can be added without replacing this file or changing the schema.

Current UI categories:

- Takeoffs
- Landings
- Maneuvers
- Stalls
- Emergency Operations

The dataset includes:

- selector ordering
- canonical maneuver IDs
- crosswind aliases
- up to four performance-standard cards per maneuver
- tolerance-bar endpoint data
- six evaluator-criteria lines
- six post-flight review variables
- FAA document/task metadata
- source URL
- page disclaimer
- source verification date

## Current FAA source

Private Pilot for Airplane Category Airman Certification Standards  
FAA-S-ACS-6C  
Effective May 31, 2024

Official source:
https://www.faa.gov/training_testing/testing/acs/private_airplane_acs_6.pdf

The FAA ACS page should always be checked before publishing a new dataset version.

## Important data rule

The FAA ACS is the source of truth for certification standards. This repository is a structured FlytWERX presentation layer.

Numeric tolerances and task mappings are based on FAA-S-ACS-6C. The `reviewVariables` fields are FlytWERX debrief guidance, not quoted FAA evaluation standards.

Crosswind Takeoff and Crosswind Landing are retained as user-friendly selector options, but they map to the applicable FAA task because FAA-S-ACS-6C does not define separate crosswind takeoff or crosswind landing tasks.

## Repository structure

```text
flytwerx-acs-data/
├── README.md
├── NOTICE.md
├── data/
│   ├── index.json
│   └── private-pilot-airplane.json
├── schema/
│   └── acs-data.schema.json
└── webflow/
    └── acs-checker-loader.html
```

## Webflow

Paste the contents of `webflow/acs-checker-loader.html` into:

**Page Settings → Custom Code → Before `</body>`**

Then change only `ACS_DATA_URL` to your GitHub raw URL.

Example:

```text
https://raw.githubusercontent.com/YOUR-USERNAME/flytwerx-acs-data/main/data/private-pilot-airplane.json
```

## Updating the FAA data later

Do not edit the Webflow page for ACS data changes.

1. Verify the current FAA ACS publication.
2. Update the JSON file.
3. Change `verifiedAgainstFAA`.
4. Commit to GitHub.
5. Publish a new repository release/tag if desired.

The Webflow page fetches the current JSON at load time.
