# sudo tuning best result

## Summary
- date: 2026-04-16
- script: /workspaces/CentOS/sudo-tuning.sh
- mode: search
- iterations: 100
- bench runs: 3

## Best configuration (auto-selected)
- Defaults !use_pty
- Defaults !pam_session
- Defaults !pam_setcred
- Defaults !log_allowed

## Measurement result
- baseline average: 1.682667 sec
- final average: 1.244333 sec
- improvement: 26.05%
- delta: -0.438334 sec

## Step-by-step (selected rounds)
| Round | Added setting | Avg sec | Improvement vs baseline |
|---|---|---:|---:|
| 0 | baseline | 1.682667 | 0.00% |
| 1 | !use_pty | 1.509667 | 10.28% |
| 2 | !pam_session | 1.459000 | 13.29% |
| 3 | !pam_setcred | 1.300333 | 22.72% |
| 4 | !log_allowed | 1.244333 | 26.05% |

## Reproduce
```bash
sudo MODE=search bash /workspaces/CentOS/sudo-tuning.sh
```

## Note
- The script restores /etc/sudoers.d/99-tuning automatically when KEEP_FINAL is not 1.
- To keep the selected config after search, run with KEEP_FINAL=1.
