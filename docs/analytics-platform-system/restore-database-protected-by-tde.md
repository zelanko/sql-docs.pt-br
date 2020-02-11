---
title: Restaurar um banco de dados protegido por TDE
description: Use as etapas a seguir para restaurar um banco de dados que é criptografado usando Transparent Data Encryption no data warehouse paralelo do sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 53707c62e018b9923f2bb923a4df46f6917d2902
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400445"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>Restaurar um banco de dados protegido pelo TDE em paralelo data warehouse
Use as etapas a seguir para restaurar um banco de dados que é criptografado usando Transparent Data Encryption.  
  
O exemplo [usando Transparent Data Encryption](transparent-data-encryption.md#using-tde) tem código para habilitar TDE no banco `AdventureWorksPDW2012` de dados. O código a seguir continua esse exemplo, criando um backup do banco de dados no dispositivo original do sistema de plataforma de análise (APS) e, em seguida, restaurando o certificado e o banco de dados em um dispositivo diferente.  
  
A primeira etapa é criar um backup do banco de dados de origem.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
Prepare o novo SQL Server PDW para TDE criando uma chave mestra, habilitando a criptografia e criando uma credencial de rede.  
  
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
  
As duas últimas etapas recriam o certificado usando os backups do SQL Server PDW original. Use a senha que você usou quando criou o backup do certificado.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>Consulte Também  
[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[Criar chave](../t-sql/statements/create-master-key-transact-sql.md) 
mestra[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)  
[RESTAURAR BANCO DE DADOS](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
