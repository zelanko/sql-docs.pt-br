---
title: Restaurar um banco de dados protegido por TDE no Parallel Data Warehouse
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Use as etapas a seguir para restaurar um banco de dados que é criptografado usando criptografia transparente de dados."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: ffb681ca-8598-4614-b06c-660376333fc3
caps.latest.revision: "4"
ms.openlocfilehash: 31f81447bd4fdaf5a2528f5828cc3d70618240c6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="restore-a-database-protected-by-tde"></a>Restaurar um banco de dados protegido por TDE
Use as etapas a seguir para restaurar um banco de dados que é criptografado usando criptografia transparente de dados.  
  
O [usando criptografia transparente de dados](transparent-data-encryption.md#using-tde) exemplo tem o código para habilitar a TDE o `AdventureWorksPDW2012` banco de dados. O código a seguir continua este exemplo, criando um backup do banco de dados no dispositivo Analytics Platform System (APS) original e, em seguida, restaurar o certificado e o banco de dados em um dispositivo diferente.  
  
A primeira etapa é criar um backup do banco de dados de origem.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
Prepare o novo SQL Server PDW para TDE, criando uma chave mestra, habilitando a criptografia e, em seguida, criando uma credencial de rede.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
As duas últimas etapas recrie o certificado usando os backups do SQL Server PDW original. Use a senha que você usou quando criou o backup do certificado.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>Consulte também  
[BANCO DE DADOS DE BACKUP](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md) 
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[CRIAR CERTIFICADO](../t-sql/statements/create-certificate-transact-sql.md)  
[RESTAURAR BANCO DE DADOS](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
