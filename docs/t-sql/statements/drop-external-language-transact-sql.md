---
description: DROP EXTERNAL LANGUAGE (Transact-SQL) – SQL Server
title: DROP EXTERNAL LANGUAGE (Transact-SQL) – SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2019
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 785aaff078085fd5c202e7b3c043ab87e273472f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481797"
---
# <a name="drop-external-language-transact-sql"></a>DROP EXTERNAL LANGUAGE (Transact-SQL)  
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Exclui uma linguagem externa existente.

## <a name="syntax"></a>Sintaxe

```syntaxsql
DROP EXTERNAL LANGUAGE <language_name>
```

### <a name="arguments"></a>Argumentos

**language_name**

As linguagens são objetos no escopo do banco de dados. Os nomes das linguagens precisam ser exclusivos no banco de dados.

## <a name="permissions"></a>Permissões

Para excluir uma linguagem, é necessário ter o privilégio ALTER ANY EXTERNAL LANGUAGE. Por padrão, os proprietários do banco de dados ou do objeto também podem excluir uma linguagem externa.

> [!NOTE]
> Observe que, antes de remover uma linguagem externa, você precisará remover as bibliotecas externas que referenciam a linguagem externa.

### <a name="return-values"></a>Valores retornados

Uma mensagem informativa é retornada se a instrução foi bem-sucedida.

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>Comentários

Para que uma linguagem externa possa ser excluída, todas as bibliotecas externas para a linguagem especificada precisam ser excluídas.

## <a name="examples"></a>Exemplos

Crie uma linguagem externa **Java**:

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

Remova a linguagem externa:

```sql
DROP EXTERNAL LANGUAGE Java;
```

## <a name="see-also"></a>Confira também

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
