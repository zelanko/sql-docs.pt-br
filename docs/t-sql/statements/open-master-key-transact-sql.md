---
description: OPEN MASTER KEY (Transact-SQL)
title: OPEN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPEN MASTER KEY DECRYPTION BY PASSWORD
- OPEN_MASTER_KEY_DECRYPTION_BY_PASSWORD_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- OPEN_MASTER_KEY_TSQL
- MASTER KEY DECRYPTION
- OPEN MASTER KEY
- MASTER_KEY_DECRYPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- opening Database Master Keys
- encryption [SQL Server], Database Master Key
- cryptography [SQL Server], Database Master Key
- master key decryption
- OPEN MASTER KEY statement
- database master key [SQL Server], opening
ms.assetid: 1674753e-ca1e-4913-9ba4-b442e7106121
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7248d97eef63492664a47dbba9a736ed295f1242
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476597"
---
# <a name="open-master-key-transact-sql"></a>OPEN MASTER KEY (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Abre a chave mestra do banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'password'   
```  
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 '*password*'  
 A senha com que a chave mestra do banco de dados foi criptografada.  
  
## <a name="remarks"></a>Comentários  
 Se a chave mestra do banco de dados for criptografada com a chave mestra de serviço, ela será aberta automaticamente quando for necessária para descriptografia ou criptografia. Nesse caso, não é necessário usar a instrução **OPEN MASTER KEY**.  
  
 Quando um banco de dados é anexado ou restaurado pela primeira vez a uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma cópia da chave mestra de banco de dados (criptografada pela chave mestra de serviço) ainda não está armazenada no servidor. É necessário usar a instrução **OPEN MASTER KEY** para descriptografar a DMK (chave mestra do banco de dados). Após a descriptografia da DMK, você tem a opção de habilitar a descriptografia automática no futuro usando a instrução **ALTER MASTER KEY REGENERATE** para provisionar o servidor com uma cópia da DMK criptografada com a SMK (chave mestra de serviço). Quando um banco de dados for atualizado de uma versão anterior, a DMK deverá ser regenerada para usar o algoritmo AES mais recente. Para obter mais informações sobre como regenerar a DMK, veja [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). O tempo necessário para regenerar a chave DMK para atualizar o AES depende do número de objetos protegidos pela DMK. É necessário regenerar a chave DMK para atualizar o AES somente uma vez, isso não tem impacto sobre regenerações futuras como parte de uma estratégia de rotação de chave.  
  
 É possível excluir a chave mestra de banco de dados de um banco de dados específico do gerenciamento automático de chave usando a instrução ALTER MASTER KEY com a opção DROP ENCRYPTION BY SERVICE MASTER KEY. Posteriormente, você deve abrir a chave mestra do banco de dados explicitamente com uma senha.  
  
 Se uma transação em que a chave mestra de banco de dados foi aberta explicitamente for revertida, a chave permanecerá aberta.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir abre a chave mestra do banco de dados `AdventureWorks2012` que foi criptografado com uma senha.  
  
```sql  
USE AdventureWorks2012;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir abre o mestre do banco de dados que foi criptografado com uma senha.  
  
```sql  
USE master;  
OPEN MASTER KEY DECRYPTION BY PASSWORD = '43987hkhj4325tsku7';  
GO  
CLOSE MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

