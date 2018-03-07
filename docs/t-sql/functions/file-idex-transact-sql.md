---
title: FILE_IDEX (Transact-SQL) | Microsoft Docs
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
- FILE_IDEX
- FILE_IDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILE_IDEX function
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_IDEX
ms.assetid: 7532fea5-ee5e-4edd-b98b-111a7ba56c8e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75882e2c74b6a432f49b9b7e14b83af05e961af7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="fileidex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Retorna o número de identificação (ID) de arquivo para o nome de arquivo lógico especificado de dados, log ou arquivo de texto completo no banco de dados atual.  
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_name*  
 É uma expressão do tipo **sysname** que representa o nome do arquivo para o qual retornar a ID de arquivo.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
 **NULO** em erro  
  
## <a name="remarks"></a>Remarks  
 *file_name* corresponde ao nome do arquivo lógico exibido no **nome** coluna o [master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) ou [sys. database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) exibições do catálogo.  
  
 FILE_IDEX pode ser usado em uma lista de seleção, cláusula WHERE ou em qualquer local em que uma expressão for permitida. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. Recuperando a ID de um arquivo especificado  
O exemplo a seguir retorna a ID de arquivo para o arquivo `AdventureWorks_Data`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX('AdventureWorks2012_Data') AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>B. Recuperando a ID do arquivo quando o nome de arquivo não é conhecido  
O exemplo a seguir retorna a ID de arquivo do `AdventureWorks` arquivo de log, selecionando o nome de arquivo lógico a `sys.database_files` onde o tipo de arquivo é igual de exibição de catálogo `1` (log).  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX((SELECT TOP (1) name FROM sys.database_files WHERE type = 1)) AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>C. Recuperando a ID de um arquivo de catálogo de texto completo  
O exemplo a seguir retorna a ID do arquivo de um arquivo de texto completo, selecionando o nome de arquivo lógico a `sys.database_files` onde o tipo de arquivo é igual de exibição de catálogo `4` (texto completo). Este exemplo retornará NULL se um catálogo de texto completo não existir.  
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
