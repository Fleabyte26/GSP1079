# GSP1079
Fix for step 8 issue

# GSP1079 – Step 8 Promotion Error

## Error
This release is not deployed to a target in the active delivery pipeline.

## Cause
The lab uses a serial delivery pipeline (test → staging → prod).
The first promotion must explicitly target the first stage.

## Fix
```bash
gcloud beta deploy releases promote \
  --delivery-pipeline web-app \
  --release web-app-001 \
  --to-target test

Notes
Failed rollouts from earlier attempts can be ignored
This is a workaround, not a full lab solution

THE FIX

What the real problem was (root cause)

The lab instructions are incomplete.
They tell students to run:

gcloud beta deploy releases promote \
  --delivery-pipeline web-app \
  --release web-app-001


But your delivery pipeline is a serial pipeline:

test → staging → prod


In Cloud Deploy:

A release must already be deployed to a target before it can be promoted.

At Step 8:

web-app-001 exists ✅

BUT it has never been deployed to any target ❌

So Cloud Deploy correctly throws:

This release is not deployed to a target in the active delivery pipeline.
Include the --to-target parameter


This is not user error — it’s an instructional gap in the lab.

✅ The correct workaround (the fix)

Because test is the first stage, the first promotion must explicitly target it:

gcloud beta deploy releases promote \
  --delivery-pipeline web-app \
  --release web-app-001 \
  --to-target test


After that:

Promotion to staging works

Promotion to prod works

“Check my progress” passes
