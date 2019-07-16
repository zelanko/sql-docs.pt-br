---
title: Restaurar um banco de dados protegido por TDE - Parallel Data Warehouse | Microsoft Docs
description: Use as etapas a seguir para restaurar um banco de dados é criptografado usando criptografia transparente de dados no Analytics Platform System Parallel Data Warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7c2f676f75c5a8c79bfc2f2417ff30c9806e3c80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960164"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>Restaurar um banco de dados protegido por TDE no Parallel Data Warehouse
Use as etapas a seguir para restaurar um banco de dados é criptografado usando criptografia transparente de dados.  
  
O [usando Transparent Data Encryption](transparent-data-encryption.md#using-tde) exemplo tem o código para habilitar a TDE no `AdventureWorksPDW2012` banco de dados. O código a seguir continua esse exemplo, criando um backup do banco de dados no dispositivo do Analytics Platform System (APS) original e, em seguida, restaurando o certificado e o banco de dados em um dispositivo diferente.  
  
A primeira etapa é criar um backup do banco de dados de origem.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
Prepare o novo SQL Server PDW para TDE, criando uma chave mestra, habilitando a criptografia e criar uma credencial de rede.  
  
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
[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
