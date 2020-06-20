---
title: Alterando tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
author: rothja
ms.author: jroth
ms.openlocfilehash: e6e28e6d1bb923fb226e7df7964853685f23178b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050383"
---
# <a name="altering-memory-optimized-tables"></a>Alterando tabelas com otimização de memória
  Não há suporte para as operações de ALTER nas tabelas com otimização de memória. Isso inclui operações como alteração do bucket_count, adição ou remoção de um índice, e adição ou remoção de uma coluna. Este tópico fornece diretrizes sobre como atualizar tabelas com otimização de memória.  
  
## <a name="updating-the-definition-of-a-memory-optimized-table"></a>Atualizando a definição de uma tabela com otimização de memória  
 A atualização da definição de uma tabela com otimização de memória exige que você crie uma nova tabela com a definição de tabela atualizada, copie os dados na nova tabela e comece a usar a nova tabela. A menos que a tabela seja somente leitura, isso requer a interrupção da carga de trabalho na tabela, de modo a garantir que nenhuma alteração seja feita na tabela enquanto a cópia dos dados é realizada.  
  
 O procedimento a seguir destaca as etapas necessárias para atualizar uma tabela. Neste exemplo, a atualização adiciona um índice. Esse procedimento preserva o nome da tabela e requer duas operações de cópia de dados: uma vez em uma tabela temporária e outra na nova tabela. A alteração de bucket_count de um índice, ou a adição ou remoção de uma coluna são executadas da mesma forma.  
  
1.  Interrompa a carga de trabalho na tabela.  
  
2.  Gere o script para a tabela e adicione o novo índice ao script.  
  
3.  Gere o script para os objetos associados ao esquema (principalmente procedimentos armazenados compilados nativamente) que fazem referência a T e suas permissões.  
  
     Os objetos associados ao esquema que fazem referência à tabela podem ser encontrados com a seguinte consulta:  
  
    ```sql  
    declare @t nvarchar(255) = N'<table name>'  
  
    select r.referencing_schema_name, r.referencing_entity_name  
    from sys.dm_sql_referencing_entities (@t, 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
    where r.is_caller_dependent = 0 and m.is_schema_bound=1;  
    ```  
  
     As permissões de um procedimento armazenado podem ser colocadas em script usando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
    ```sql  
    declare @sp nvarchar(255) = N'<procedure name>'  
    declare @permissions nvarchar(max) = N''  
  
    select @permissions += dp.state_desc + N' ' + dp.permission_name + N' ON ' +   
       quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) + N' TO ' +  
       quotename(u.name) + N'; ' + char(13)  
    from sys.database_permissions as dp  
  
    join sys.database_principals as u  
       on u.principal_id = dp.grantee_principal_id  
  
    join sys.objects as o  
       on o.object_id = dp.major_id  
    where dp.class = 1 /* object */  
       and dp.minor_id = 0 and o.object_id=object_id(@sp);  
  
    select @permissions  
    ```  
  
4.  Crie uma cópia da tabela e copie os dados da tabela original na cópia da tabela. A cópia pode ser criada usando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] <sup>1</sup>.  
  
    ```sql  
    select * into dbo.T_copy from dbo.T  
    ```  
  
     Se houver memória suficiente disponível, `T_copy` o poderá ser uma tabela com otimização de memória, o que torna a cópia de dados mais rápida.<sup> 2</sup>  
  
5.  Descarte os objetos associados ao esquema que fazem referência à tabela original.  
  
6.  Descarte a tabela original.  
  
7.  Crie a nova tabela (`T`) com o script que contém o novo índice.  
  
8.  Copie os dados de `T_copy` em `T`.  
  
9. Recrie os objetos associados ao esquema de referência e aplique as permissões.  
  
10. Inicie a carga de trabalho em `T`.  
  
 <sup>1</sup> Observe que `T_copy` é persistido no disco neste exemplo. Se um backup de `T` estiver disponível, `T_copy` poderá ser uma tabela temporária ou não durável.  
  
 <sup>2</sup> deve haver memória suficiente para `T_copy` . A memória não é liberada imediatamente em `DROP TABLE`. Se `T_copy` tiver otimização de memória, haverá necessidade de memória suficiente para duas cópias adicionais de `T`. Se `T_copy` for uma tabela baseada em disco, haverá necessidade de memória suficiente apenas para uma cópia adicional de `T`, devido ao coletor de lixo que precisa ser atualizado depois de descartar a versão antiga de `T`.  
  
## <a name="changing-schema-powershell"></a>Alterando o esquema (PowerShell)  
 Os scripts do PowerShell a seguir preparam e geram alterações de esquema gerando o script da tabela e das permissões associadas.  
  
```powershell
prepare_schema_change.ps1 <serverName> <databaseName> <schemaName> <tableName>
```
  
 Esse script usa como argumentos uma tabela e gera o script do objeto e de suas permissões, além de fazer referência a objetos associados ao esquema e suas permissões na pasta atual. Um total de 7 scripts é gerado para atualizar o esquema da tabela de entrada:  
  
-   Copie os dados em uma tabela temporária (um heap).  
  
-   Descarte os objetos associados ao esquema que fazem referência à tabela.  
  
-   Descarte a tabela.  
  
-   Recrie a tabela com o novo esquema e reaplique as permissões.  
  
-   Copie os dados da tabela temporária na tabela recriada.  
  
-   Recrie os objetos associados ao esquema que fazem referência à tabela e suas permissões.  
  
-   Descarte a tabela temporária.  
  
 O script da etapa 4 deve ser atualizado para refletir as alterações desejadas de esquema. Se houver qualquer alteração nas colunas da tabela, os scripts das etapas 5 (copiar dados de tabela temporária) e 6 (recriar procedimentos armazenados) devem ser atualizados conforme necessário.  
  
```powershell
# Prepare for schema changes by scripting out the table, as well as associated permissions
# Usage: prepare_schema_change.ps1 server_name db_name schema_name table_name  
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage prepare_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
$object_heap = "$object$(Get-Random)"  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | Out-Null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$scripter = New-Object ("Microsoft.SqlServer.Management.SMO.Scripter") ($server)  
  
## initialize table variable  
$tableUrn = $server.Databases[$database].Tables[$object, $schema]  
if($tableUrn.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
## initialize scripting object  
$scriptingOptions = New-Object ("Microsoft.SqlServer.Management.SMO.ScriptingOptions")
$scriptingOptions.Permissions = $True  
$scriptingOptions.ScriptDrops = $True  
  
$scripter.Options = $scriptingOptions;  
  
Write-Host "(1) Scripting SELECT INTO $object_heap for table [$object] to 1_copy_to_heap_for_$schema`_$object.sql"  
Echo "SELECT * INTO $schema.$object_heap FROM $schema.$object WITH (SNAPSHOT)" | Out-File "1_copy_to_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(2) Scripting DROP for procs schema-bound to [$object] 2_drop_procs_$schema`_$object.sql"  
## query referencing schema-bound objects  
$dt = $server.Databases[$database].ExecuteWithResults("select r.referencing_schema_name, r.referencing_entity_name  
from sys.dm_sql_referencing_entities ('$schema.$object', 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
where r.is_caller_dependent = 0 and m.is_schema_bound=1;")  
  
## initialize out file  
Echo "" | Out-File "2_drop_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
ForEach ($t In $dt.Tables)  
{    
   ForEach ($r In $t.Rows)  
   {    
      ## script object   
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      $scripter.Script($so) | Out-File -Append "2_drop_procs_$schema`_$object.sql"  
   }  
}  
Write-Host "--done--"  
Write-Host ""  
Write-Host "(3) Scripting DROP table for [$object] to 3_drop_table_$schema`_$object.sql"
$scripter.Script($tableUrn) | Out-File "3_drop_table_$schema`_$object.sql";
Write-Host "--done--"  
Write-Host ""  
  
## now script creates  
$scriptingOptions.ScriptDrops = $False  
  
Write-Host "(4) Scripting CREATE table and permissions for [$object] to !please_edit_4_create_table_$schema`_$object.sql"  
Write-Host "***** rename this script to 4_create_table.sql after completing the updates to the schema"
$scripter.Script($tableUrn) | Out-File "!please_edit_4_create_table_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(5) Scripting INSERT INTO table from heap and UPDATE STATISTICS for [$object] to 5_copy_from_heap_$schema`_$object.sql"  
Write-Host "[update this script if columns are added to or removed from the table]"  
Echo "INSERT INTO [$schema].[$object] SELECT * FROM [$schema].[$object_heap]; UPDATE STATISTICS [$schema].[$object] WITH FULLSCAN, NORECOMPUTE" | Out-File "5_copy_from_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(6) Scripting CREATE PROC and permissions for procedures schema-bound to [$object] to 6_create_procs_$schema`_$object.sql"  
Write-Host "[update the procedure definitions if columns are renamed or removed]"  
## initialize out file  
Echo "" | Out-File "6_create_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
ForEach ($t In $dt.Tables)  
{    
   ForEach ($r In $t.Rows)  
   {    
      ## script the schema-bound object  
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      ForEach($s In $scripter.Script($so))  
        {  
            Echo $s | Out-File -Append "6_create_procs_$schema`_$object.sql"  
            Echo "GO" | Out-File -Append "6_create_procs_$schema`_$object.sql"  
        }  
   }  
}  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(7) Scripting DROP $object_heap to 7_drop_heap_$schema`_$object.sql"  
Echo "DROP TABLE $schema.$object_heap" | Out-File "7_drop_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
```  
  
 O script de PowerShell a seguir executa as alterações do esquema que foram incluídas em script no exemplo anterior. Esse script é considerado argumento de uma tabela, além de executar os scripts de alteração do esquema que foram gerados para essa tabela e os procedimentos armazenados associados.  
  
 Uso: execute_schema_change.ps1 *server_name * * db_name `schema_name` table_name*  
  
```powershell
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage execute_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | Out-Null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$database = $server.Databases[$database]  
$table = $database.Tables[$object, $schema]  
if($table.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
$1 = Get-Item "1_copy_to_heap_$schema`_$object.sql"  
$2 = Get-Item "2_drop_procs_$schema`_$object.sql"  
$3 = Get-Item "3_drop_table_$schema`_$object.sql"  
$4 = Get-Item "4_create_table_$schema`_$object.sql"  
$5 = Get-Item "5_copy_from_heap_$schema`_$object.sql"  
$6 = Get-Item "6_create_procs_$schema`_$object.sql"  
$7 = Get-Item "7_drop_heap_$schema`_$object.sql"  
  
Write-Host "(1) Running SELECT INTO heap for table [$object] from 1_copy_to_heap_for_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $1.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(2) Running DROP for procs schema-bound from [$object] 2_drop_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $2.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(3) Running DROP table for [$object] to 4_drop_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $3.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(4) Running CREATE table and permissions for [$object] from 4_create_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $4.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(5) Running INSERT INTO table from heap for [$object] and UPDATE STATISTICS from 5_copy_from_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $5.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(6) Running CREATE PROC and permissions for procedures schema-bound to [$object] from 6_create_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $6.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(7) Running DROP heap from 7_drop_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $7.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Memory-Optimized Tables](memory-optimized-tables.md)  
