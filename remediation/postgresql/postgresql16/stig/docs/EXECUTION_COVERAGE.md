# PostgreSQL 16 V1R3 executable coverage

Generated from the current branch task files to prove that every V1R3 V-ID has an executable owner. This is a coverage/traceability artifact, not proof that each control is automatically remediated or assessment-verified.

| V-ID | STIG ID | Executable owner(s) |
|---|---|---|
| V-261857 | CD16-00-000100 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261858 | CD16-00-000200 | tasks/audit.yml :: PostgreSQL 16 STIG | Flag site-owned authorization evidence<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit HBA authentication methods<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261859 | CD16-00-000300 | tasks/audit.yml :: PostgreSQL 16 STIG | Flag site-owned authorization evidence<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261860 | CD16-00-000400 | tasks/remediation.yml :: PostgreSQL 16 STIG | Check pgAudit extension availability<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Require pgAudit to be available<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Read shared_preload_libraries<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Build merged shared_preload_libraries<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure merged shared_preload_libraries<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure literal audit identity prefix<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Report restart-required pgAudit preload change<br>tasks/audit.yml :: PostgreSQL 16 STIG | Audit current pgAudit/logging state<br>tasks/audit.yml :: PostgreSQL 16 STIG | Report pgAudit/logging state |
| V-261861 | CD16-00-000500 | tasks/remediation.yml :: PostgreSQL 16 STIG | Check pgAudit extension availability<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Require pgAudit to be available<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes<br>tasks/audit.yml :: PostgreSQL 16 STIG | Audit current pgAudit/logging state<br>tasks/audit.yml :: PostgreSQL 16 STIG | Report pgAudit/logging state |
| V-261862 | CD16-00-000600 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261863 | CD16-00-000700 | tasks/remediation.yml :: PostgreSQL 16 STIG | Check pgAudit extension availability<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Require pgAudit to be available<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Read shared_preload_libraries<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Build merged shared_preload_libraries<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure merged shared_preload_libraries<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit catalog auditing<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Report restart-required pgAudit preload change<br>tasks/audit.yml :: PostgreSQL 16 STIG | Audit current pgAudit/logging state<br>tasks/audit.yml :: PostgreSQL 16 STIG | Report pgAudit/logging state |
| V-261864 | CD16-00-000800 | tasks/audit.yml :: PostgreSQL 16 STIG | Audit current pgAudit/logging state<br>tasks/audit.yml :: PostgreSQL 16 STIG | Report pgAudit/logging state<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261865 | CD16-00-000900 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings<br>tasks/audit.yml :: PostgreSQL 16 STIG | Audit current pgAudit/logging state<br>tasks/audit.yml :: PostgreSQL 16 STIG | Report pgAudit/logging state |
| V-261866 | CD16-00-001000 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure literal audit identity prefix |
| V-261867 | CD16-00-001100 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure literal audit identity prefix |
| V-261868 | CD16-00-001200 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure literal audit identity prefix |
| V-261869 | CD16-00-001300 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure literal audit identity prefix |
| V-261870 | CD16-00-001400 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit detail settings |
| V-261871 | CD16-00-001500 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings<br>tasks/remediation.yml :: PostgreSQL 16 STIG | Configure literal audit identity prefix |
| V-261872 | CD16-00-001600 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit detail settings<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization-defined audit-detail evidence |
| V-261873 | CD16-00-001700 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require audit infrastructure evidence |
| V-261874 | CD16-00-001800 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require audit infrastructure evidence |
| V-261875 | CD16-00-002000 | tasks/remediation.yml :: PostgreSQL 16 STIG | Protect stderr audit log file creation mode |
| V-261876 | CD16-00-002100 | tasks/remediation.yml :: PostgreSQL 16 STIG | Protect stderr audit log file creation mode |
| V-261877 | CD16-00-002200 | tasks/remediation.yml :: PostgreSQL 16 STIG | Protect stderr audit log file creation mode |
| V-261878 | CD16-00-002300 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit PostgreSQL-owned filesystem objects<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261879 | CD16-00-002400 | tasks/remediation.yml :: PostgreSQL 16 STIG | Protect stderr audit log file creation mode<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit PostgreSQL-owned filesystem objects |
| V-261880 | CD16-00-002500 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261881 | CD16-00-002600 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit PostgreSQL-owned filesystem objects<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261882 | CD16-00-002700 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261883 | CD16-00-002800 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit PostgreSQL-owned filesystem objects<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261884 | CD16-00-002900 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261885 | CD16-00-003000 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261886 | CD16-00-003200 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit installed database extensions<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261887 | CD16-00-003300 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit server version<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Report installed server version<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261888 | CD16-00-003400 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit installed database extensions<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261889 | CD16-00-003500 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261890 | CD16-00-003600 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261891 | CD16-00-003800 | tasks/remediation.yml :: PostgreSQL 16 STIG | Store newly set passwords with SCRAM-SHA-256<br>tasks/audit.yml :: PostgreSQL 16 STIG | Audit stored password representation<br>tasks/audit.yml :: PostgreSQL 16 STIG | Report non-SCRAM password role count without hashes |
| V-261892 | CD16-00-003900 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit HBA authentication methods |
| V-261893 | CD16-00-004000 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit HBA authentication methods<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require PKI and transport-protection evidence |
| V-261894 | CD16-00-004100 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit PostgreSQL-owned filesystem objects<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require PKI and transport-protection evidence |
| V-261895 | CD16-00-004200 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit HBA authentication methods<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require PKI and transport-protection evidence |
| V-261896 | CD16-00-004400 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Read host FIPS indicator<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Report host FIPS indicator<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require FIPS and cryptographic-module evidence |
| V-261897 | CD16-00-004500 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit HBA authentication methods<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261898 | CD16-00-004600 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261899 | CD16-00-004700 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings |
| V-261900 | CD16-00-004900 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit HBA authentication methods<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require PKI and transport-protection evidence |
| V-261901 | CD16-00-005200 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit installed database extensions<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require data-at-rest protection evidence |
| V-261902 | CD16-00-005300 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261903 | CD16-00-005400 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require documented data-transfer procedure evidence |
| V-261904 | CD16-00-005600 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit PostgreSQL-owned filesystem objects<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261905 | CD16-00-005700 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261906 | CD16-00-005800 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261907 | CD16-00-005900 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261908 | CD16-00-006000 | tasks/remediation.yml :: PostgreSQL 16 STIG | Limit client-visible PostgreSQL error detail |
| V-261909 | CD16-00-006100 | tasks/remediation.yml :: PostgreSQL 16 STIG | Limit client-visible PostgreSQL error detail |
| V-261910 | CD16-00-006200 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261911 | CD16-00-006400 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261912 | CD16-00-006500 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261913 | CD16-00-006600 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261914 | CD16-00-006700 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261915 | CD16-00-006800 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261916 | CD16-00-006900 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261917 | CD16-00-007000 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require audit infrastructure evidence |
| V-261918 | CD16-00-007200 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require audit infrastructure evidence |
| V-261919 | CD16-00-007300 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require audit infrastructure evidence |
| V-261920 | CD16-00-007400 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require audit infrastructure evidence |
| V-261921 | CD16-00-007500 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings |
| V-261922 | CD16-00-007600 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings |
| V-261923 | CD16-00-007700 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261924 | CD16-00-007800 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit role security attributes and connection limits<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261925 | CD16-00-007900 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261926 | CD16-00-008000 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require organization access-control evidence |
| V-261927 | CD16-00-008100 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261928 | CD16-00-008300 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require PKI and transport-protection evidence |
| V-261929 | CD16-00-008400 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit HBA authentication methods<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require PKI and transport-protection evidence |
| V-261930 | CD16-00-008500 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit installed database extensions<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require data-at-rest protection evidence |
| V-261931 | CD16-00-008600 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit installed database extensions<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require data-at-rest protection evidence |
| V-261932 | CD16-00-008800 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require PKI and transport-protection evidence |
| V-261933 | CD16-00-008900 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require PKI and transport-protection evidence |
| V-261934 | CD16-00-009000 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require application and database-design evidence |
| V-261935 | CD16-00-009100 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit server version<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Report installed server version<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261936 | CD16-00-009200 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit server version<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Report installed server version<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |
| V-261938 | CD16-00-009400 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261939 | CD16-00-009500 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261940 | CD16-00-009600 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261941 | CD16-00-009700 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261942 | CD16-00-009800 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261943 | CD16-00-009900 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261944 | CD16-00-010000 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261945 | CD16-00-010100 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261946 | CD16-00-010200 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261947 | CD16-00-010300 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261948 | CD16-00-010400 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261949 | CD16-00-010500 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261950 | CD16-00-010600 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261951 | CD16-00-010700 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261952 | CD16-00-010800 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261953 | CD16-00-010900 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261954 | CD16-00-011000 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261955 | CD16-00-011100 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261956 | CD16-00-011200 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings |
| V-261957 | CD16-00-011300 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261958 | CD16-00-011400 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings |
| V-261959 | CD16-00-011500 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261960 | CD16-00-011600 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings |
| V-261961 | CD16-00-011700 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure connection audit settings |
| V-261962 | CD16-00-011800 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261963 | CD16-00-011900 | tasks/evidence.yml :: PostgreSQL 16 STIG | Require negative audit-event verification |
| V-261964 | CD16-00-012000 | tasks/remediation.yml :: PostgreSQL 16 STIG | Configure pgAudit event classes |
| V-261965 | CD16-00-012200 | tasks/audit.yml :: PostgreSQL 16 STIG | Flag FIPS/crypto platform evidence<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Read host FIPS indicator<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Report host FIPS indicator<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require FIPS and cryptographic-module evidence |
| V-261966 | CD16-00-012300 | tasks/audit.yml :: PostgreSQL 16 STIG | Flag FIPS/crypto platform evidence<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Read host FIPS indicator<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Report host FIPS indicator<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require FIPS and cryptographic-module evidence |
| V-261967 | CD16-00-012400 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit organization-sensitive server settings<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require audit infrastructure evidence |
| V-283674 | CD16-00-009300 | tasks/technical_audit.yml :: PostgreSQL 16 STIG | Audit server version<br>tasks/technical_audit.yml :: PostgreSQL 16 STIG | Report installed server version<br>tasks/evidence.yml :: PostgreSQL 16 STIG | Require software and filesystem governance evidence |

Coverage checkpoint: **111/111 V-IDs have executable ownership**.
