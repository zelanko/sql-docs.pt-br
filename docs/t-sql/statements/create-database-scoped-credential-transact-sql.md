---
title: CRIAR a CREDENCIAL de escopo do banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE SCOPED CREDENTIAL
- DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_TSQL
- CREATE_DATABASE_SCOPED_CREDENTIAL
- CREATE_DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL
helpviewer_keywords:
- DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], DATABASE SCOPED CREDENTIAL statement
ms.assetid: fe830577-11ca-44e5-953b-2d589d54d045
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7e1eeda5d365f5c625e68c498c741754bf59c9d7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-scoped-credential-transact-sql"></a>CRIAR a CREDENCIAL de escopo do banco de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Cria uma credencial de banco de dados. Uma credencial de banco de dados não é mapeada para um usuário de logon ou de banco de dados do servidor. A credencial é usada pelo banco de dados para acessar o local externo sempre que o banco de dados está executando uma operação que requer acesso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
 
CREATE DATABASE SCOPED CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Especifica o nome da credencial no escopo do banco de dados que está sendo criada. *credential_name* não pode começar com o sinal de número (#). As credenciais de sistema começam com ##.  
  
 IDENTIDADE **='***identity_name***'**  
 Especifica o nome da conta a ser usada ao conectar o servidor externamente. Para importar um arquivo de armazenamento de BLOBs do Azure, o nome de identidade deve ser `SHARED ACCESS SIGNATURE`.  Para obter mais informações sobre assinaturas de acesso compartilhado, consulte [assinaturas usando de acesso compartilhado (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).  
  
 SEGREDO **='***segredo***'**  
 Especifica o segredo necessário para a autenticação de saída. `SECRET`é necessário para importar um arquivo de armazenamento de BLOBs do Azure.   
>  [!WARNING]
>  O valor da chave SAS pode começar com um '?' (ponto de interrogação). Quando você usa a chave SAS, você deve remover à esquerda '?'. Caso contrário, seus esforços podem estar bloqueados.  
  
## <a name="remarks"></a>Comentários  
 Uma credencial no escopo do banco de dados é um registro que contém as informações de autenticação é necessária para conectar a um recurso fora [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A maioria das credenciais inclui um usuário e uma senha do Windows.  
  
 Antes de criar um banco de dados, a credencial com escopo, o banco de dados deve ter uma chave mestra para proteger a credencial. Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 Quando IDENTITY for um usuário do Windows, o segredo poderá ser a senha. O segredo é criptografado com a chave mestre de serviço. Se a chave mestre de serviço for gerada novamente, o segredo será criptografado novamente com a nova chave mestre de serviço.  
   
 Informações sobre credenciais no escopo do banco de dados são visíveis no [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) exibição do catálogo.  
  
 
 Hereare as credenciais no escopo de alguns aplicativos de banco de dados:  
  
- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]usa uma credencial no escopo do banco de dados para acessar o armazenamento de BLOBs do Azure não-públicos ou clusters de Hadoop protegidos por Kerberos com o PolyBase. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).  

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]usa uma credencial no escopo do banco de dados para acessar o armazenamento de BLOBs do Azure não-públicos com o PolyBase. Para obter mais informações, consulte [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]usa as credenciais no escopo para seu recurso de consulta global de banco de dados. Essa é a capacidade de consultar em vários fragmentos de banco de dados.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]usa credenciais no escopo do banco de dados para gravar arquivos de evento estendido para o armazenamento de BLOBs do Azure.  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]usa as credenciais no escopo de pools Elásticos de banco de dados. Para obter mais informações, consulte [controlar o crescimento explosivo com bancos de dados Elásticos](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)  

- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) credenciais para acessar dados de armazenamento de BLOBs do Azure no escopo do banco de dados de uso. Para obter mais informações, consulte [exemplos de Bulk acesso aos dados no armazenamento de BLOBs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md). 
  
## <a name="permissions"></a>Permissões  
 Requer **controle** no banco de dados.  
  
## <a name="examples"></a>Exemplos  
### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>A. Criar um banco de dados, a credencial para o seu aplicativo com escopo.
 O exemplo a seguir cria a credencial no escopo do banco de dados chamada `AppCred`. A credencial no escopo do banco de dados contém o usuário do Windows `Mary5` e uma senha.  
  
```tsql  
-- Create a db master key if one does not already exist, using your own password.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';  
  
-- Create a database scoped credential.  
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>B. Criar um banco de dados de credencial com escopo de uma assinatura de acesso compartilhado.   
O exemplo a seguir cria uma credencial no escopo do banco de dados que pode ser usada para criar um [fonte de dados externa](../../t-sql/statements/create-external-data-source-transact-sql.md), que pode executar operações em massa, como [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).   
```tsql
CREATE DATABASE SCOPED CREDENTIAL MyCredentials  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```
  
### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. Criar um banco de dados de credencial com escopo de conectividade do PolyBase para repositório Azure Data Lake.  
O exemplo a seguir cria uma credencial no escopo do banco de dados que pode ser usada para criar um [fonte de dados externa](../../t-sql/statements/create-external-data-source-transact-sql.md), que pode ser usado pelo PolyBase no Azure SQL Data Warehouse.

Repositório Azure Data Lake usa um aplicativo do Azure Active Directory para autenticação de serviços.
Por favor, [criar um aplicativo AAD](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory) e documentar o client_id, OAuth_2.0_Token_EndPoint e chave antes de tentar criar uma credencial no escopo do banco de dados.

```tsql
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>'
    SECRET = '<key>'
;
```  
  
  
  
## <a name="more-information"></a>Mais informações  
 [Credenciais &#40; mecanismo de banco de dados &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

