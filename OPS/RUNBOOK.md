# Quillmark batch operations runbook (fictional)

> **SYNTHETIC.** Written for the Diocle hackathon project. Quillmark Trust & Savings does not exist.

## Daily cycle (QMKD020, then QMKD010)
| Step | Program | Normal RC | If it fails |
|---|---|---|---|
| QMKD020 POST010 | TXNPOST (PROC QMKPOST) | 0 | Restart the job from the top; output is a new generation of QMK.PROD.TXN.POSTED. |
| QMKD010 SORT005 | DFSORT, cards QMK.PROD.CNTLLIB(SORTTXN) | 0 | Check QMK.PROD.TXN.DAILY arrived; rerun from SORT005. |
| QMKD010 MTCH010 | ACCTMTCH | 0 or **4** | RC 4 means exceptions were written to QMK.PROD.TXN.EXCEPTIONS(+1): normal. RC > 4 holds the cycle; delete the (+1) generations of the master and exceptions before restarting at SORT005. |
| QMKD010 INT020 | INTACCR (PROC QMKINT) | 0 | Restart at INT020. |
| QMKD010 CTL030 | DAYCTRL (PROC QMKCTL) | 0 | The GL control total must equal the sum of posted interest; if GL disagrees, do not rerun, page finance. |

## Weekly (QMKW010) and month end (QMKM010)
PKDPOST reads the packed extract; CUSTMNT updates the customer KSDS in place (take a REPRO backup first). FEESCHD runs at month end; STMTGEN runs under the DB2 TSO attach (plan QMKSTMT).

## Online
Transaction QINQ (ACCTINQ, mapset ACCTSET) reads QMK.PROD.CUST.KSDS read-only. CSD group QMKGRP.

## Known quirks (do not "fix" in a rewrite without sign-off)
- Interest is COMPUTE ROUNDED: half away from zero, including negative half cents.
- Fees are COMPUTE without ROUNDED: truncated to the cent.
- Several amounts silently lose high-order digits on overflow; the fee cap is applied after that.
- The GL control total adds each account's rounded interest, not the unrounded sum.
- Account IDs sort in EBCDIC order: letters before digits.
