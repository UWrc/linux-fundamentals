## What Resources Do You Have?

After logging in, one of the first things you should do is check **what compute and storage resources are associated with your account**.  

Hyak provides command-line tools to help you understand:

- Which **accounts and partitions** you can use to schedule jobs.
- How much **compute capacity** is available to you.
- The **status and utilization of your storage allocations**.

Two commonly used tools are `hyakalloc` and `hyakstorage`.

## Checking Compute Resources with `hyakalloc` (Klone only)

The `hyakalloc` command shows which **Hyak accounts and partitions** you are a member of, along with the **current utilization** of those resources. Resource limits are directly tied to what was contributed by each group.

Run:
```bash
hyakalloc
```
A typical output may look like this:
```bash
Account resources available to user: UWNetID   

╭─────────┬──────────────┬──────┬────────┬──────┬───────╮
│ Account │    Partition │ CPUs │ Memory │ GPUs │       │
├─────────┼──────────────┼──────┼────────┼──────┼───────┤
│ account │      compute │  120 │   509G │    0 │ TOTAL │
│         │              │    0 │     0G │    0 │ USED  │
│         │              │  120 │   509G │    0 │ FREE  │
├─────────┼──────────────┼──────┼────────┼──────┼───────┤
│ account │    gpu-rtx6k │   10 │    81G │    2 │ TOTAL │
│         │              │    0 │     0G │    0 │ USED  │
│         │              │   10 │    81G │    2 │ FREE  │
╰─────────┴──────────────┴──────┴────────┴──────┴───────╯
```

This table shows:
* Which accounts you belong to
* Which partitions you can run jobs on
* The total, used, and free CPUs, memory, and GPUs

### Optional Arguments

You can refine `hyakalloc` output using flags:

```bash
hyakalloc --help
```

Common options include:
* `--ckpt` Show checkpoint availability
* `--group` Query a specific account
* `--partition` Filter by partition
* `--user` Query another user (if permitted)

### Demo Accounts
If you are using a demo or onboarding/training account, you may see output similar to:
```bash
╭─────────┬───────────┬──────┬────────┬──────┬───────╮
│ Account │ Partition │ CPUs │ Memory │ GPUs │       │
├─────────┼───────────┼──────┼────────┼──────┼───────┤
│  demo   │  pending  │   0  │   0G   │   0  │ TOTAL │
╰─────────┴───────────┴──────┴────────┴──────┴───────╯
```
This indicates that no priority compute resources are currently associated with your account. You can schedule job on community idle resources under the checkpoint partitions: `ckpt`, `ckpt-g2`, and `ckpt-all`.

## Checking Storage Usage with `hyakstorage` (Klone & Tillicum)

The `hyakstorage` command reports storage utilization and quotas for:

* Your home directory
* Shared group or project storage

Run with no arguments:
```bash
hyakstorage
```

This will display a summary of all storage locations you have access to.

### Viewing Options
```bash
hyakstorage --help
```

Commonly used flags:
* `--home` Show home directory usage
* `--gscratch` Show group/project storage usage
* `--show-group` Break down usage by group
* `--show-user` Break down usage by user
* `--by-disk` Sort by disk usage (default)
* `--by-files` Sort by number of files

You may also specify a path or group name to narrow the report.

> **NOTE: Storage Reporting Delay**
>
> Storage quotas reported by `hyakstorage` are updated **once per hour**.
> * You may hit a quota limit before it appears in `hyakstorage`
> * Cleanup efforts may not be reflected immediately
>
>If you encounter an out-of-space error (i.e., "Disk quota exceeded"), trust the error message and continue cleanup even if the quota report lags.
>
> If you are actively cleaning up files and want immediate feedback, run:
> ```bash
> du -h -d 1
> ```
> This command reports disk usage in **real time** for the current directory and is often more useful than quota tools during cleanup.