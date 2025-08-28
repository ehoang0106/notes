
```cmd
bcp "ERPTest.dbo.AppsTree" out "C:\temp\UserDeptTemplate.csv" -S "11.0.0.90" -U "khoa" -P "xzkiller" -c -t, -C 65001
```

`"ERPTest.dbo.AppsTree"` is `[database_name].[tablen_name]`

## Import

```
bcp ERPTest.dbo.UserDeptTemplate in C:\temp\UserDeptTemplate.csv -S 11.0.0.90 -U khoa -P xzkiller -c -t, -C 65001

```