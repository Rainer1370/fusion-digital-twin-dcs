# Public Release Sanitization Report

## Source reviewed

`canis-eos-helios-main (3)(2).zip`

## Decision

The uploaded repository should not be published or converted to public visibility in place. A curated public technical-preview repository was created instead.

## Material excluded from the public package

- Thea Energy logos and company-branded banners
- Company- and program-specific display directories and naming
- Detailed device, network, host, switch, and VLAN inventories
- Exact PV databases and facility implementation mappings
- Detailed interlock matrices, thresholds, and response actions
- Vendor BOM, quantities, estimated costs, and lead times
- Model parameters and fit results associated with named programs
- Runtime logs, PID files, local histories, and generated artifacts
- Compiled IOC binaries, objects, dependency files, and build output
- Device-specific PDU code containing hard-coded local addresses and example credentials
- Work-in-progress and duplicated IOC source trees
- Production-style launch and deployment internals

## Public material retained or recreated

- Original high-level fusion DCS and digital-twin concept
- Layer responsibilities and authority boundaries
- EPICS-centered integration rationale
- Digital-twin lifecycle and incremental deployment strategy
- Independent authorship, date, citation metadata, and collaboration invitation
- A newly created, company-neutral architecture diagram

## Recommended repository strategy

Keep the original engineering repository private. Publish this curated directory as a separate repository or as a dedicated orphan/public-release branch whose history does not contain the excluded files. Do not merely delete sensitive files in a normal commit and assume they are absent from Git history.
