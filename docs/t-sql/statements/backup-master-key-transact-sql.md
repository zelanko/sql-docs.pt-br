---
description: BACKUP MASTER KEY (Transact-SQL)
title: BACKUP MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BACKUP MASTER KEY
- DUMP_MASTER_KEY_TSQL
- BACKUP_MASTER_KEY_TSQL
- DUMP MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- BACKUP MASTER KEY statement
- exporting Database Master Keys
- encryption [SQL Server], Database Master Key
- cryptography [SQL Server], Database Master Key
- backing up master keys [SQL Server]
- database master key [SQL Server], exporting
ms.assetid: 0e25fe22-2536-4d7e-ba4a-1921e880f367
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8c7d0bd39ebda34677469a45687fd78f0e4124cc
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126193"
---
# <a name="backup-master-key-transact-sql"></a>BACKUP MASTER KEY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exporta a chave mestra do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
BACKUP MASTER KEY TO FILE = 'path_to_file'   
    ENCRYPTION BY PASSWORD = 'password'  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 FILE ='*path_to_file*'  
 Especifica o caminho completo, inclusive o nome de arquivo, para o arquivo para o qual a chave mestra será exportada. Esse pode ser um caminho local ou um caminho de UNC a um local de rede.  
  
 PASSWORD ='*password*'  
 É a senha usada para criptografar a chave mestra no arquivo. Esta senha está sujeita à verificação de complexidade. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).  
  
## <a name="remarks"></a>Comentários  
 A chave mestra deve estar aberta e, portanto, descriptografada antes de ser feito o back up. Se for criptografada com a chave mestra de serviço, a chave mestra não terá que ser aberta explicitamente. No entanto, se a chave mestra só for criptografada com uma senha, ela deve ser aberta explicitamente.  
  
 Recomendamos que você faça o backup da chave mestra assim que ela for criada e armazene o backup em um local externo seguro.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte cria um backup da chave mestra `AdventureWorks2012`. Como esta chave mestra não está criptografada pela chave mestra de serviço, é necessário especificar uma senha quando ela for aberta.  
  
```sql  
USE AdventureWorks2012;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'sfj5300osdVdgwdfkli7';  
BACKUP MASTER KEY TO FILE = 'c:\temp\exportedmasterkey'   
    ENCRYPTION BY PASSWORD = 'sd092735kjn$&adsg';  
GO   
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
