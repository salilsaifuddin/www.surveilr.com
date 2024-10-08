---
title: ur_ingest_session_imap_account
---

## Description

Immutable ingest session folder system represents an email address to be
ingested. Each session includes an email, then email is the folder that was
scanned.

<details>
<summary><strong>Table Definition</strong></summary>

```sql
CREATE TABLE "ur_ingest_session_imap_account" (
    "ur_ingest_session_imap_account_id" VARCHAR PRIMARY KEY NOT NULL,
    "ingest_session_id" VARCHAR NOT NULL,
    "email" TEXT,
    "password" TEXT,
    "host" TEXT,
    "elaboration" TEXT CHECK(json_valid(elaboration) OR elaboration IS NULL),
    "created_at" TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP,
    "created_by" TEXT DEFAULT 'UNKNOWN',
    "updated_at" TIMESTAMPTZ,
    "updated_by" TEXT,
    "deleted_at" TIMESTAMPTZ,
    "deleted_by" TEXT,
    "activity_log" TEXT,
    FOREIGN KEY("ingest_session_id") REFERENCES "ur_ingest_session"("ur_ingest_session_id"),
    UNIQUE("ingest_session_id", "email")
)
```

</details>

## Columns

| Name                              | Type        | Default           | Nullable | Children                                                                                                              | Parents                                                                             | Comment                                                 |
| --------------------------------- | ----------- | ----------------- | -------- | --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------- |
| ur_ingest_session_imap_account_id | VARCHAR     |                   | false    | [ur_ingest_session_imap_acct_folder](/surveilr/reference/db/surveilr-state-schema/ur_ingest_session_imap_acct_folder) |                                                                                     | {"isSqlDomainZodDescrMeta":true,"isVarChar":true}       |
| ingest_session_id                 | VARCHAR     |                   | false    |                                                                                                                       | [ur_ingest_session](/surveilr/reference/db/surveilr-state-schema/ur_ingest_session) | {"isSqlDomainZodDescrMeta":true,"isVarChar":true}       |
| email                             | TEXT        |                   | true     |                                                                                                                       |                                                                                     |                                                         |
| password                          | TEXT        |                   | true     |                                                                                                                       |                                                                                     |                                                         |
| host                              | TEXT        |                   | true     |                                                                                                                       |                                                                                     |                                                         |
| elaboration                       | TEXT        |                   | true     |                                                                                                                       |                                                                                     | {"isSqlDomainZodDescrMeta":true,"isJsonText":true}      |
| created_at                        | TIMESTAMPTZ | CURRENT_TIMESTAMP | true     |                                                                                                                       |                                                                                     |                                                         |
| created_by                        | TEXT        | 'UNKNOWN'         | true     |                                                                                                                       |                                                                                     |                                                         |
| updated_at                        | TIMESTAMPTZ |                   | true     |                                                                                                                       |                                                                                     |                                                         |
| updated_by                        | TEXT        |                   | true     |                                                                                                                       |                                                                                     |                                                         |
| deleted_at                        | TIMESTAMPTZ |                   | true     |                                                                                                                       |                                                                                     |                                                         |
| deleted_by                        | TEXT        |                   | true     |                                                                                                                       |                                                                                     |                                                         |
| activity_log                      | TEXT        |                   | true     |                                                                                                                       |                                                                                     | {"isSqlDomainZodDescrMeta":true,"isJsonSqlDomain":true} |

## Constraints

| Name                                              | Type        | Definition                                                                                                                             |
| ------------------------------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| ur_ingest_session_imap_account_id                 | PRIMARY KEY | PRIMARY KEY (ur_ingest_session_imap_account_id)                                                                                        |
| - (Foreign key ID: 0)                             | FOREIGN KEY | FOREIGN KEY (ingest_session_id) REFERENCES ur_ingest_session (ur_ingest_session_id) ON UPDATE NO ACTION ON DELETE NO ACTION MATCH NONE |
| sqlite_autoindex_ur_ingest_session_imap_account_2 | UNIQUE      | UNIQUE (ingest_session_id, email)                                                                                                      |
| sqlite_autoindex_ur_ingest_session_imap_account_1 | PRIMARY KEY | PRIMARY KEY (ur_ingest_session_imap_account_id)                                                                                        |
| -                                                 | CHECK       | CHECK(json_valid(elaboration) OR elaboration IS NULL)                                                                                  |

## Indexes

| Name                                                         | Definition                                                                                                                                    |
| ------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| idx_ur_ingest_session_imap_account__ingest_session_id__email | CREATE INDEX "idx_ur_ingest_session_imap_account__ingest_session_id__email" ON "ur_ingest_session_imap_account"("ingest_session_id", "email") |
| sqlite_autoindex_ur_ingest_session_imap_account_2            | UNIQUE (ingest_session_id, email)                                                                                                             |
| sqlite_autoindex_ur_ingest_session_imap_account_1            | PRIMARY KEY (ur_ingest_session_imap_account_id)                                                                                               |

## Relations

![er](../../../../../assets/ur_ingest_session_imap_account.svg)
