---
description: DROP EXTERNAL LIBRARY (Transact-SQL)
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: 3cbf3bfa6ad5cb6971d1cd7ab7d9d4d2ac490c2a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478477"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Exclui uma biblioteca de pacote existente. As bibliotecas de pacotes são usadas por runtimes externos com suporte, tais como do R, Python ou Java.

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. Há suporte para R, Python e Java nas plataformas Windows e Linux no SQL Server 2019 e posteriores.
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
> [!NOTE]
> Na Instância Gerenciada de SQL do Azure, as linguagens R e Python são compatíveis.
::: moniker-end

## <a name="syntax"></a>Sintaxe

```syntaxsql
DROP EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ];
```

### <a name="arguments"></a>Argumentos

**library_name**

Especifica o nome de uma biblioteca de pacotes existente.

As bibliotecas estão no escopo do usuário. Os nomes de bibliotecas devem ser exclusivos no contexto de um usuário ou proprietário específico.

**owner_name**

Especifica o nome do usuário ou da função que é a proprietária da biblioteca externa.

Os proprietários de banco de dados podem excluir bibliotecas criadas por outros usuários.

## <a name="permissions"></a>Permissões

Para excluir uma biblioteca, é necessário ter o privilégio ALTER ANY EXTERNAL LIBRARY. Por padrão, todos os proprietários de bancos de dados ou do objeto também podem excluir uma biblioteca externa.

### <a name="return-values"></a>Valores retornados

Uma mensagem informativa é retornada se a instrução foi bem-sucedida.

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários

Ao contrário de outras instruções `DROP` no SQL Server, essa instrução dá suporte à especificação de uma cláusula de autorização opcional. Isso permite que o **dbo** ou os usuários na função **db_owner** removam uma biblioteca de pacote carregada por um usuário normal no banco de dados.

Vários pacotes, chamados de *pacotes do sistema*, são pré-instalados em uma instância SQL. Os pacotes do sistema não podem ser adicionados, atualizados nem removidos pelo usuário.

## <a name="examples"></a>Exemplos

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15"
Adicione o pacote do R personalizado, chamado `customPackage`, a um banco de dados:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```
::: moniker-end

Exclua a biblioteca `customPackage`.

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>Confira também

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
