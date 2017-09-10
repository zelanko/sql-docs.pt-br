---
title: File_name (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILE_NAME_TSQL
- FILE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file names
- file names [SQL Server], FILE_NAME
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- displaying file names
- identification numbers [SQL Server], files
- FILE_NAME function
- logical file names [SQL Server]
ms.assetid: 68b298aa-ce47-4af5-b59f-9a1b46d48326
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a2ca12bf5c6f5cfa3e9a7b44300119d5e55e57da
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="filename-transact-sql"></a>FILE_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o nome de arquivo lógico para o número de identificação (ID) de arquivo fornecido.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FILE_NAME ( file_id )   
```  
  
## <a name="arguments"></a>Argumentos  
 *file_id*  
 É o número de identificação de arquivo cujo nome de arquivo será retornado. *file_id* é **int**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar (128)**  
  
## <a name="remarks"></a>Comentários  
 *file_ID* corresponde à coluna file_id nas exibições do catálogo sys. master_files ou sys. database_files.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os nomes de arquivo para `file`_`ID 1` e `file` \_ `ID` no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.  
  
```tsql  
  
SELECT FILE_NAME(1) AS 'File Name 1', FILE_NAME(2) AS 'File Name 2';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `File Name 1           File Name 2`  
  
 `----------------      ------------------------`  
  
 `AdventureWorks2012_Data   AdventureWorks2012_Log`  
  
 `(1 row(s) affected)`  
  
## <a name="see-also"></a>Consulte também  
 [FILE_IDEX &#40; Transact-SQL &#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
