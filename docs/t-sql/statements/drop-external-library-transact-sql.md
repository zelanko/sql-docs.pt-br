---
title: SOLTE a biblioteca externa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 143e9ac0dbe042ebbb034dff847cfc01ea5a5411
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-library-transact-sql"></a>SOLTE a biblioteca externa (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

Exclui uma biblioteca de pacote existente.

## <a name="syntax"></a>Sintaxe  
```
DROP EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ];  
```

### <a name="arguments"></a>Argumentos

**nome_da_biblioteca**

Especifica o nome de uma biblioteca de pacote existente.

Bibliotecas de escopo serão o usuário. Ou seja, nomes de biblioteca são considerados exclusivos dentro do contexto de um usuário específico ou um proprietário.

**owner_name**

Especifica o nome do usuário ou função que possui a biblioteca externa.

Os proprietários de banco de dados podem excluir bibliotecas criadas por outros usuários.

### <a name="return-values"></a>Valores de retorno

Uma mensagem informativa será retornada se a instrução foi bem-sucedida.

## <a name="remarks"></a>Comentários

Ao contrário de outras `DROP` instruções no SQL Server, essa instrução oferece suporte à especificação de uma cláusula de autorização opcional. Isso permite que **dbo** ou os usuários a **db_owner** função para remover uma biblioteca de pacote carregado por um usuário regular no banco de dados.

## <a name="examples"></a>Exemplos

Adicione ggplot2 a um banco de dados:

```sql
CREATE EXTERNAL LIBRARY ggplot2 
FROM 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\ggplot2.zip';
```

Exclua a biblioteca ggplot2.

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

## <a name="see-also"></a>Consulte também  
[Criar biblioteca externa (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER biblioteca externa (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  


