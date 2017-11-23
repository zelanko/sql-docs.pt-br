---
title: SOLTE a biblioteca externa (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
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
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: ac2814f7c0b0d1bf6de60d52ea65e54caab0f72d
ms.contentlocale: pt-br
ms.lasthandoff: 10/10/2017

---
# <a name="drop-external-library-transact-sql"></a>SOLTE a biblioteca externa (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

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

Adicionar um pacote R personalizado, chamado `customPackage`, um banco de dados:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 'C:\Users\Username\CustomPackages\customPackage.zip';
```

Excluir o `customPackage` biblioteca.

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

## <a name="see-also"></a>Consulte também  
[Criar biblioteca externa (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER biblioteca externa (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  


