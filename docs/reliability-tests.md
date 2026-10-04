# Reliability tests

## TESTED

### Software

- TypeScript compilation: PASS
- Automated tests: 126 PASS / 0 FAIL

Coverage includes:

- unit normalization;
- stale-value rejection;
- malformed response rejection;
- wrong-device rejection;
- idempotency;
- persistence/reopen behavior;
- batch/event reconciliation;
- dashboard security behavior;
- BAS-derived calculations.

### Integration service restart

Procedure:

- terminate integration-service process;
- wait for watchdog recovery;
- check HTTP endpoint.

Result: PASS.

### Vendor scale-service recovery

Procedure:

- run synthetic application probe;
- stop service;
- wait for recovery;
- rerun application probe.

Result: PASS.

### Public dashboard route recovery

Procedure:

- remove public route;
- keep local dashboard running;
- trigger watchdog threshold.

Observed sequence:

1. public HTTPS failure detected;
2. network service restarted once;
3. public HTTPS retested;
4. configured dashboard routes reapplied;
5. public HTTPS retested;
6. failure counter reset.

External result: HTTP 401.

Result: PASS.

### BAS/ERP dashboard sync after Windows account password reset

Observed sequence:

1. Password-mode Scheduled Task credential invalidated;
2. task logon failed;
3. task credential refreshed;
4. runner started;
5. DPAPI-protected BAS credential failed to decrypt;
6. BAS credential recreated;
7. scheduled sync rerun;
8. new `FISHPILOT_DASHBOARD_SYNC_OK` marker produced.

Result: PASS after credential refresh.

## IMPLEMENTED

- scheduled SQLite backup;
- bounded watchdog tasks;
- path-scoped dashboard exposure;
- logical scale IDs;
- audit/provenance persistence;
- batch/event reconciliation.

## TBD

- enterprise HA;
- zero downtime;
- automatic physical-device recovery;
- automatic credential rotation;
- automatic live-database restore;
- arbitrary scale-vendor compatibility;
- fleet orchestration.
