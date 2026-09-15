# terraform-shared-modules

A collection of reusable Terraform modules for common AWS patterns.

The goal here isn't to reinvent infrastructure — it's to package up things
that have already been solved once (often painfully) so they don't need to be
solved again. If a module in here saves you from re-deriving an IAM policy,
an event pattern, or a wiring diagram between a handful of AWS services,
it's done its job.

## Layout

- `modules/` — the reusable modules themselves, one directory per module.
- `examples/` — small, runnable root configurations that exercise a module
  end to end, useful both as documentation and for local validation.

## Modules

| Module                                                                   | Description                                                                 |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| [guardduty-malware-protection](modules/guardduty-malware-protection)      | GuardDuty Malware Protection on an S3 bucket, with an EventBridge → SQS → Lambda pipeline that moves scanned objects to a safe or quarantine bucket. |

## Usage

Reference a module by relative path (or a Git URL with a `ref` once
versioned) from your own root configuration, e.g.:

```hcl
module "malware_protection" {
  source = "git::https://github.com/sidssn/terraform-shared-modules.git//modules/guardduty-malware-protection?ref=main"

  # ...
}
```

Each module has its own README with inputs, outputs, and usage examples.

## Contributing

These modules are written to be generic and reusable rather than tied to any
one project. If you spot a gap, an unsafe default, or a pattern that's
missing, contributions are welcome.
