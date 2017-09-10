---
title: FILE_ID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILE_ID
- FILE_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], files
- file IDs [SQL Server]
- FILE_ID function
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_ID
ms.assetid: 6a7382cf-a360-4d62-b9d2-5d747f56f076
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2544da5cb252b27f42a82e1fa400d7c28f503f20
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="fileid-transact-sql"></a>FILE_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o número de identificação (ID) de arquivo para o nome de arquivo lógico fornecido no banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FILE_ID ( file_name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_name*  
 É uma expressão do tipo **sysname** que representa o nome do arquivo para o qual retornar a ID de arquivo.  
  
## <a name="return-types"></a>Tipos de retorno  
 **smallint**  
  
## <a name="remarks"></a>Comentários  
 *file_name* corresponde ao nome do arquivo lógico exibido na coluna nome nas exibições do catálogo sys. master_files ou sys. database_files.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o número de identificação de arquivo atribuído a catálogos de texto completo é maior que 32.767. Porque o tipo de retorno da função FILE_ID **smallint**, essa função não pode ser usada para arquivos de texto completo. Use [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) em vez disso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a ID de arquivo para o arquivo `AdventureWorks_Data`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT FILE_ID('AdventureWorks2012_Data')AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [File_name &#40; Transact-SQL &#41;](../../t-sql/functions/file-name-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
