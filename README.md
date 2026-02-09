# GSP1079 – Step 8 Promotion Error

## Error
This release is not deployed to a target in the active delivery pipeline.
Include the --to-target parameter


## Reason
The lab uses a serial pipeline:

test → staging → prod


The first promotion must explicitly target the first stage.  
The lab command skips this step.

## Fix
Replace the lab command:

```bash
gcloud beta deploy releases promote \
  --delivery-pipeline web-app \
  --release web-app-001
with this command:

gcloud beta deploy releases promote \
  --delivery-pipeline web-app \
  --release web-app-001 \
  --to-target test
After that, promotions to staging and prod will work and the lab will pass.

