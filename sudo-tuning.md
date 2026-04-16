- sudo tuning file: /etc/sudoers.d/99-tuning
- validated with: visudo -cf /etc/sudoers
- benchmark command: time for i in {1..100}; do sudo true; done

## Per-setting improvement summary

| Setting change | Before (sec) | After (sec) | Delta (sec) | Improvement | Decision | Notes |
|---|---:|---:|---:|---:|---|---|
| timestamp_timeout=30 + timestamp_type=global | 1.718 (single) | 1.709 (single) | -0.009 | 0.5% faster | kept | Single-run only |
| !use_pty | 1.790 (single) | 1.529 (single) | -0.261 | 14.6% faster | kept | Large win in single-run comparison |
| !pam_session + !pam_setcred | 1.529 (single) | 1.335 (single) | -0.194 | 12.7% faster | kept | Clear win in single-run comparison |
| !syslog + !log_allowed + !log_denied | 1.790 (single) | 1.439 (single) | -0.351 | 19.6% faster | kept | Measured once; high noise risk |
| !env_reset | 1.419/1.395/1.288 (avg 1.367) | 1.304/1.313/1.272 (avg 1.296) | -0.071 | 5.2% faster | kept | 3-run A/B result |
| !authenticate | 1.407/1.263/1.282 (avg 1.317) | 1.378/1.285/1.268 (avg 1.310) | -0.007 | 0.5% faster | kept | Small gain; near noise floor |
| !match_group_by_gid | 1.281 (disabled avg) | 1.296 (enabled avg) | +0.015 | 1.2% slower | rejected | Reverted after A/B |
| !always_set_home | 1.281 (control avg) | 1.304 (candidate avg) | +0.023 | 1.8% slower | rejected | Reverted after A/B |

- active options now: timestamp_timeout=30, timestamp_type=global, !use_pty, !pam_session, !pam_setcred, !syslog, !log_allowed, !log_denied, !env_reset, !authenticate
- latest single run with retained config: 1.366 sec