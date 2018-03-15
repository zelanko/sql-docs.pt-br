---
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: 8c45da28bf795fca50454fde21eb7d2c3c798296
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Exclui uma biblioteca de pacote existente.

## <a name="syntax"></a>Sintaxe  

```
DROP EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ];  
```

### <a name="arguments"></a>Argumentos

**library_name**

Especifica o nome de uma biblioteca de pacotes existente.

As bibliotecas estão no escopo do usuário. Ou seja, os nomes de biblioteca são considerados exclusivos no contexto de um usuário ou um proprietário específico.

**owner_name**

Especifica o nome do usuário ou da função que é a proprietária da biblioteca externa.

Os proprietários de banco de dados podem excluir bibliotecas criadas por outros usuários.

### <a name="return-values"></a>Valores retornados

Uma mensagem informativa é retornada se a instrução foi bem-sucedida.

## <a name="remarks"></a>Remarks

Ao contrário de outras instruções `DROP` no SQL Server, essa instrução dá suporte à especificação de uma cláusula de autorização opcional. Isso permite que o **dbo** ou os usuários na função **db_owner** removam uma biblioteca de pacote carregada por um usuário normal no banco de dados.

## <a name="examples"></a>Exemplos

Adicione um pacote do R personalizado, chamado `customPackage`, a um banco de dados:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 'C:\Users\Username\CustomPackages\customPackage.zip';
```

Exclua a biblioteca `customPackage`.

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

## <a name="see-also"></a>Consulte também  
[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

