# app-hpe-ngsm (application repo)

Mock Application repo for the HPE Unify RO demo, mirroring the
disastor/app-taskflow reference architecture.

- `deployer.yaml` - one job per component (hpcm-admin, ngsm-base, cpe,
  pbs), each conditionally deployed from a system-generated release
  manifest, calling that component's own deploy.yaml in its own repo.
- `release-wf.yml` - the staged workflow. One real stage today
  (HPC-Test-Cluster), with an approval gate before it.

Both validated against Unify's live schema via workflow_validate.

## Before this actually runs

1. Push ngsm-base, hpcm-admin, cpe, and pbs as four separate repos.
2. Create a Component in Unify for each, pointing at its repo.
3. Create an Application ("NGSM" or similar) and register all four.
4. Create a Release against the Application, selecting a version for
   each component - this is what generates the real manifest JSON.
5. Push this repo (app-hpe-ngsm) and confirm the manifest key
   convention (currently assumed to be each artifact's registered
   `name`, e.g. "ngsm-base") - adjust deployer.yaml if the real
   generated manifest uses something else.
6. Replace `disastor` in deployer.yaml with the actual org/user the
   four component repos live under, if different.
