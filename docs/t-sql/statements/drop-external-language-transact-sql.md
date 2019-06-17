---
title: DROP EXTERNAL LANGUAGE (Transact-SQL) – SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 29bb832fc1123b5261088b52232b693ca1c10138
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65994934"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Exclui uma linguagem externa existente.

## <a name="syntax"></a>Sintaxe

```text
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

## <a name="remarks"></a>Remarks

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
