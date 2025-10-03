
Run this on google cloud console

```sql
INSERT INTO `as-erp-468422.ERPTest.Users` (

  UsersID_PK, UserSupervisorID_FK, UsersPasscode, UsersMonitorCust, UserForcePassChange, UserDateToExpired, RecStatusNo_FK, UsersLastName, UsersFirstName, UsersMidName, UsersLocDesc, UserPassChangeDate, UsersCreatedDt, UsersCreatedBy, UsersLastUpdDt, UsersLastUpdBy, defForCustomer, ViewAllQuotes, RPRMview, crtNewQnumOnly, EditNewBOM, UpdateStdCost, RMViewHisNote, RMViewPOBatch, EditSOPkgAfterBOM, EditPOAfterRecv, CloseOrVoidSO, WinLogonID, UserLogonDt, UserLogOffDt, EditRFQDoc, EditPkgBatch, UsersToken, UsersWebPwd, UsersForgotPwdId, UsersDepartment, UsersEmail, UsersFCMToken, LikeBackground, RecvNotification, ApprovePO, Signature, TitleID, Picture, sPicture, Language, UsersPhoneNum

) VALUES (

  'khoa', 'Nhut.Bui', 'cb5698002feb2880c904218cfc237100', NULL, FALSE, 999, 5, 'TEST', 'ADMIN', NULL, NULL, DATETIME '2025-08-13 14:07:59.000', DATETIME '2025-08-13 14:07:59.000', 'Poei_Tuyen', DATETIME '2025-08-13 14:07:59.000', 'quocnguyen', NULL, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, FALSE, TRUE, TRUE, 'admin', DATETIME '2025-08-13 14:07:59.000', DATETIME '2025-08-13 14:07:59.000', TRUE, FALSE, 'yfuzt0o22misxj5kqq1mfsd0', '84b49183dab64d0d37d311f7bb682f5c', NULL, 'ADMIN', 'quocnguyen@rpi.inc', NULL, TRUE, TRUE, TRUE, NULL, 'ERP-D', NULL, NULL, 'en', '7148298232'

);
```

run on mssql server

make sure iam role has `bigquery.table.updatedata`

```sql

SELECT * FROM OPENQUERY([AS_BigQuery_link],
	'INSERT INTO `as-erp-468422.ERPTest.Users` (
		UsersID_PK, UserSupervisorID_FK, UsersPasscode, UsersMonitorCust, UserForcePassChange, UserDateToExpired, RecStatusNo_FK, UsersLastName, UsersFirstName, UsersMidName, UsersLocDesc, UserPassChangeDate, UsersCreatedDt, UsersCreatedBy, UsersLastUpdDt, UsersLastUpdBy, defForCustomer, ViewAllQuotes, RPRMview, crtNewQnumOnly, EditNewBOM, UpdateStdCost, RMViewHisNote, RMViewPOBatch, EditSOPkgAfterBOM, EditPOAfterRecv, CloseOrVoidSO, WinLogonID, UserLogonDt, UserLogOffDt, EditRFQDoc, EditPkgBatch, UsersToken, UsersWebPwd, UsersForgotPwdId, UsersDepartment, UsersEmail, UsersFCMToken, LikeBackground, RecvNotification, ApprovePO, Signature, TitleID, Picture, sPicture, Language, UsersPhoneNum
	) VALUES (
		''khoa'', ''Nhut.Bui'', ''cb5698002feb2880c904218cfc237100'', NULL, FALSE, 999, 5, ''TEST'', ''ADMIN'', NULL, NULL, DATETIME ''2025-08-13 14:07:59.000'', DATETIME ''2025-08-13 14:07:59.000'', ''Poei_Tuyen'', DATETIME ''2025-08-13 14:07:59.000'', ''quocnguyen'', NULL, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, TRUE, FALSE, TRUE, TRUE, ''admin'', DATETIME ''2025-08-13 14:07:59.000'', DATETIME ''2025-08-13 14:07:59.000'', TRUE, FALSE, ''yfuzt0o22misxj5kqq1mfsd0'', ''84b49183dab64d0d37d311f7bb682f5c'', NULL, ''ADMIN'', ''quocnguyen@rpi.inc'', NULL, TRUE, TRUE, TRUE, NULL, ''ERP-D'', NULL, NULL, ''en'', ''7148298232''
	)'
);
```