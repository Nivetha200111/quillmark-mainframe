# Dataset map

> **SYNTHETIC.** Written for the Diocle hackathon project.

This repository is an export of the fictional Quillmark z/OS libraries. Each folder is a partitioned dataset (PDS) and each file a member, with no file extension, exactly as members are named on the mainframe. COBOL source and copybooks keep their sequence numbers in columns 73-80.

| Folder (dataset) | Contents |
|---|---|
| `QMK.PROD.COBOL` | Batch and online COBOL programs: ACCTMTCH, INTACCR, DAYCTRL, TXNPOST, FEESCHD, PKDPOST (batch); CUSTMNT (VSAM update); STMTGEN (DB2); ACCTINQ (CICS) |
| `QMK.PROD.COPYLIB` | Record layouts (copybooks) |
| `QMK.PROD.DCLGEN` | DB2 DCLGEN for QMK.TRANSACTION |
| `QMK.PROD.JCLLIB` | Jobs: QMKD010 daily cycle, QMKD020 posting, QMKW010 weekly, QMKM010 month end, QMKVDEF VSAM and GDG definitions |
| `QMK.PROD.PROCLIB` | Cataloged procedures with symbolic parameters (QMKINT, QMKCTL, QMKPOST) |
| `QMK.PROD.CNTLLIB` | DFSORT and IDCAMS control cards |
| `QMK.PROD.DB2.DDL` | DB2 schema |
| `QMK.PROD.BMS`, `QMK.PROD.CSD` | CICS mapset and resource definitions |
| `QMK.PROD.IMS.DBD`, `QMK.PROD.IMS.COPYLIB` | IMS customer database definition and segment layouts |
| `QMK.PROD.REXX`, `QMK.PROD.EZTLIB` | Operations REXX exec and an Easytrieve report |
| `SCHEDULE` | CA-7 style job flow |
| `DATA` | Sample extracts as they sit on z/OS: EBCDIC (cp037), RECFM=FB, packed and binary fields as raw bytes. See `DATA/LISTCAT.txt`. |
| `OPS` | Operations runbook |
