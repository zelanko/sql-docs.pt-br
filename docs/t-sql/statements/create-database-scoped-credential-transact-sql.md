---
description: CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)
title: CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=aps-pdw-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 72f2f72300982473696132d327881a2f2b867dd9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426828"
---
# <a name="create-database-scoped-credential-transact-sql"></a>CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Cria uma credencial de banco de dados. Uma credencial de banco de dados não é mapeada para um usuário do banco de dados ou logon do servidor. A credencial é usada pelo banco de dados para acessar o local externo sempre que o banco de dados está executando uma operação que requer acesso.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxe

```syntaxsql
CREATE DATABASE SCOPED CREDENTIAL credential_name
WITH IDENTITY = 'identity_name'
    [ , SECRET = 'secret' ]

```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

*credential_name* Especifica o nome da credencial no escopo do banco de dados que está sendo criada. *credential_name* não pode começar com a tecla jogo da velha (#). As credenciais de sistema começam com ##.

IDENTITY **='** _identity\_name_ **'** Especifica o nome da conta a ser usada ao se conectar fora do servidor. Para importar um arquivo do armazenamento de Blobs do Azure usando uma chave compartilhada, o nome de identidade deve ser `SHARED ACCESS SIGNATURE`. Para carregar dados no SQL DW, qualquer valor válido pode ser usado para a identidade. Para mais informações sobre assinaturas de acesso compartilhado, consulte [Usando SAS (Assinatura de Acesso Compartilhado)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

> [!NOTE]
> WITH IDENTITY não será necessário se o contêiner no armazenamento de Blobs do Azure estiver habilitado para acesso anônimo. Para obter um exemplo de como consultar o armazenamento de Blobs do Azure, confira [Importar dados em uma tabela de um arquivo armazenado no Armazenamento de Blobs do Azure](../functions/openrowset-transact-sql.md#j-importing-into-a-table-from-a-file-stored-on-azure-blob-storage).

SECRET **='** _secret_ **'** Especifica o segredo necessário para a autenticação de saída. `SECRET` é necessário para importar um arquivo de armazenamento de Blobs do Azure. Para fazer o carregamento do armazenamento de Blobs do Azure no SQL DW ou no Parallel Data Warehouse, o Segredo deve ser a Chave de Armazenamento do Azure.
> [!WARNING]
> O valor da chave SAS pode começar com um '?' (ponto de interrogação). Quando você usa a chave SAS, deve remover o '?' à esquerda. Caso contrário, seus esforços poderão ser bloqueados.

## <a name="remarks"></a>Comentários

Uma credencial no escopo do banco de dados é um registro que contém as informações de autenticação necessárias para conectar-se a um recurso fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A maioria das credenciais inclui um usuário e uma senha do Windows.

Antes de criar uma credencial no escopo do banco de dados, o banco de dados deve ter uma chave mestra para proteger a credencial. Para obter mais informações, veja [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md).

Quando IDENTITY for um usuário do Windows, o segredo poderá ser a senha. O segredo é criptografado com a chave mestre de serviço. Se a chave mestre de serviço for gerada novamente, o segredo será criptografado novamente com a nova chave mestre de serviço.

Informações sobre credenciais no escopo do banco de dados ficam visíveis na exibição do catálogo [database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).

Estas são algumas aplicações das credenciais no escopo do banco de dados:

- O [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usa uma credencial no escopo do banco de dados para acessar o armazenamento de blobs do Azure não público ou clusters Hadoop protegidos por Kerberos com PolyBase. Para obter mais informações, veja [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).

- O [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] usa uma credencial no escopo do banco de dados para acessar o armazenamento de blobs do Azure não público com PolyBase. Para obter mais informações, veja [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md).

- O [!INCLUDE[ssSDS](../../includes/sssds-md.md)] usa as credenciais no escopo do banco de dados para seu recurso de consulta global. Essa é a capacidade de consultar entre vários fragmentos de banco de dados.

- O [!INCLUDE[ssSDS](../../includes/sssds-md.md)] usa credenciais no escopo do banco de dados para gravar arquivos de evento estendidos para o armazenamento de blobs do Azure.

- O [!INCLUDE[ssSDS](../../includes/sssds-md.md)] usa as credenciais no escopo do banco de dados para pools elásticos. Para obter mais informações, veja [Controlar o crescimento explosivo com bancos de dados elásticos](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)

- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) usam credenciais no escopo do banco de dados para acessar dados do armazenamento de blobs do Azure. Para obter mais informações, veja [Exemplos de acesso aos dados em massa no armazenamento de blobs do Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md). 

## <a name="permissions"></a>Permissões

Exige a permissão **CONTROL** no banco de dados.

## <a name="examples"></a>Exemplos

### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>a. Como criar uma credencial no escopo do banco de dados para seu aplicativo

O exemplo a seguir cria a credencial no escopo do banco de dados chamada `AppCred`. A credencial no escopo do banco de dados contém o usuário do Windows `Mary5` e uma senha.

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',
    SECRET = '<EnterStrongPasswordHere>';
```

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>B. Como criar uma credencial no escopo do banco de dados para uma Assinatura de Acesso Compartilhado

O exemplo a seguir cria uma credencial no escopo do banco de dados que pode ser usada para criar uma [fonte de dados externa](../../t-sql/statements/create-external-data-source-transact-sql.md), que pode executar operações em massa, como [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). As Assinaturas de Acesso Compartilhado não podem ser usadas com o PolyBase no SQL Server, APS ou SQL DW.

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.
CREATE DATABASE SCOPED CREDENTIAL MyCredentials
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```

### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. Como criar uma credencial no escopo do banco de dados para a conectividade do PolyBase com o Azure Data Lake Storage

O exemplo a seguir cria uma credencial no escopo do banco de dados que pode ser usada para criar uma [fonte de dados externa](../../t-sql/statements/create-external-data-source-transact-sql.md), que pode ser usada pelo PolyBase no SQL Data Warehouse do Azure.

O Azure Data Lake Store usa um Aplicativo do Azure Active Directory para Autenticação de Serviço.
[Crie um aplicativo AAD](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory) e documente seu client_id, o OAuth_2.0_Token_EndPoint e a Chave antes de tentar criar uma credencial no escopo do banco de dados.

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;
```

## <a name="more-information"></a>Mais informações

- [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)
- [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)
- [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)
- [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)
- [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
