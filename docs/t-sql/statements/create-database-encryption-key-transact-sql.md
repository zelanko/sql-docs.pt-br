---
description: CREATE DATABASE ENCRYPTION KEY (Transact-SQL)
title: CREATE DATABASE ENCRYPTION KEY (Transact-SQL)
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASE_ENCRYPTION_KEY_TSQL
- ENCRYPTION_KEY_TSQL
- sql13.swb.dbencryptionkeyo.f1
- ENCRYPTION KEY
- DATABASE ENCRYPTION KEY
- CREATE_DATABASE_ENCRYPTION_KEY_TSQL
- CREATE DATABASE ENCRYPTION KEY
- sql13.swb.dbencryptionkeyg.f1
- CREATE DATABASE ENCRYPTION
- CREATE_DATABASE_ENCRYPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key
- CREATE DATABASE ENCRYPTION KEY statement
- database encryption key, create
ms.assetid: 2ee95a32-5140-41bd-9ab3-a947b9990688
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest'
ms.openlocfilehash: e3ed7051503f4e4242cf75d22cca2fd5017f5c55
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93067400"
---
# <a name="create-database-encryption-key-transact-sql"></a>CREATE DATABASE ENCRYPTION KEY (Transact-SQL)

[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

 Cria uma chave de criptografia que é usada para criptografar um banco de dados de maneira transparente. Para obter mais informações sobre criptografia de banco de dados transparente, consulte [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Syntax for SQL Server  

CREATE DATABASE ENCRYPTION KEY  
       WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   ENCRYPTION BY SERVER   
    {  
        CERTIFICATE Encryptor_Name |  
        ASYMMETRIC KEY Encryptor_Name  
    }  
[ ; ]  
```  
  
> [!Note]
> [!INCLUDE [Synapse preview note](../../includes/synapse-preview-note.md)]
   
```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  

CREATE DATABASE ENCRYPTION KEY  
       WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name   
[ ; ]  
```  
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

WITH ALGORITHM = { AES_128 \| AES_192 \| AES_256 \| TRIPLE_DES_3KEY  }  
Especifica o algoritmo de criptografia que é usado para a chave de criptografia.

> [!NOTE]
> Começando com o SQL Server 2016, todos os algoritmos, exceto AES_128, AES_192 e AES_256, foram preteridos. Para usar algoritmos mais antigos (não recomendado) você deve definir o nível de compatibilidade do banco de dados para 120 ou inferior.  
  
ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name  
Especifica o nome do criptografador usado para criptografar a chave de criptografia do banco de dados.  
  
ENCRYPTION BY SERVER ASYMMETRIC KEY Encryptor_Name  
Especifica o nome da chave assimétrica usada para criptografar a chave de criptografia do banco de dados. Para criptografar a chave de criptografia de banco de dados com uma chave assimétrica, essa chave deve residir em um provedor de gerenciamento extensível de chaves.  
  
## <a name="remarks"></a>Comentários  
Uma chave de criptografia de banco de dados é exigida para que um banco de dados possa ser criptografado com o uso da TDE ( *Criptografia de banco de dados transparente* ). Quando for criptografado de maneira transparente, todo o banco de dados será criptografado no nível de arquivo, sem nenhuma modificação especial de código. O certificado ou a chave assimétrica usados para criptografar a chave de criptografia de banco de dados devem estar localizados no banco de dados do sistema mestre.  
  
As instruções de criptografia de banco de dados são permitidas apenas em bancos de dados de usuários.  
  
A chave de criptografia de banco de dados não pode ser exportada do banco de dados. Ela está disponível apenas para o sistema, para usuários com permissões de depuração no servidor e para usuários com acesso aos certificados que criptografam e descriptografam a chave de criptografia de banco de dados.  
  
A chave de criptografia de banco de dados não precisa ser gerada novamente quando um dbo (proprietário de banco de dados) é alterado.  
  
Uma chave de criptografia do banco de dados é criada automaticamente para um banco de dados [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Você não precisa criar uma chave usando a instrução CREATE DATABASE ENCRYPTION KEY.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão CONTROL no banco de dados e a permissão VIEW DEFINITION na chave assimétrica ou no certificado usado para criptografar a chave de criptografia do banco de dados.  
  
## <a name="examples"></a>Exemplos  
Para obter exemplos adicionais usando a TDE, veja [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md), [Habilitar TDE no SQL Server usando EKM](../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md) e [Gerenciamento Extensível de Chaves usando o Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
O exemplo a seguir cria uma chave de criptografia de banco de dados denominada `AES_256` e protege a chave privada com um certificado denominado `MyServerCert`.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
[Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md)   
[Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
[Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
[Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)   
[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
    
