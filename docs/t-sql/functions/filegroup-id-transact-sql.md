---
title: FILEGROUP_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILEGROUP_ID_TSQL
- FILEGROUP_ID
dev_langs:
- TSQL
helpviewer_keywords:
- FILEGROUP_ID function
- identification numbers [SQL Server], filegroups
- filegroups [SQL Server], IDs
- IDs [SQL Server], filegroups
- names [SQL Server], filegroups
ms.assetid: 852a76d8-9e61-4a31-84ee-c7edb84a061c
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 714fd89eef4144e2c2a5cd2bba88540cd3ae2d29
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="filegroupid-transact-sql"></a>FILEGROUP_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o número de identificação (ID) de grupo de arquivos para um nome de grupo de arquivos especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FILEGROUP_ID ( 'filegroup_name' )   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *filegroup_name* **'**  
 É uma expressão do tipo **sysname** que representa o nome do grupo de arquivos para o qual retornar a ID do grupo de arquivos.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 *filegroup_name* corresponde ao **nome** coluna o **sys. filegroups** exibição do catálogo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a ID de grupo de arquivos para o grupo de arquivos nomeado `PRIMARY` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
  
SELECT FILEGROUP_ID('PRIMARY') AS [Filegroup ID];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Filegroup ID  
------------  
1  

(1 row(s) affected)
 ```  
  
## <a name="see-also"></a>Consulte também  
 [FILEGROUP_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys. filegroups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  

