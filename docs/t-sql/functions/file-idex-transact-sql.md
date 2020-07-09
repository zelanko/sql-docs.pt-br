---
title: FILE_IDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e369ae57024b88ee65c4a81217661314e5533d47
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895779"
---
# <a name="file_idex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Esta função retorna o número de identificação (ID) do arquivo para o nome lógico especificado de um dado, log ou arquivo de texto completo do banco de dados atual. 
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_name*  
Uma expressão do tipo **sysname** que retorna o valor da ID do arquivo “FILE_IDEX” para o nome do arquivo. 
  
## <a name="return-types"></a>Tipos de retorno  
**int**  
  
**NULL** em caso de erro  
  
## <a name="remarks"></a>Comentários  
*file_name* corresponde ao nome de arquivo lógico exibido na coluna **name** nas exibições do catálogo [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) ou [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).  
  
Use `FILE_IDEX` em uma lista SELECT, uma cláusula WHERE ou qualquer lugar com suporte ao uso de uma expressão. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>a. Recuperando a ID de um arquivo especificado  
Este exemplo retorna a ID de arquivo para o arquivo `AdventureWorks_Data`.  
  
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
Este exemplo retorna a ID de arquivo do arquivo de log `AdventureWorks`. O snippet de código Transact-SQL (T-SQL) seleciona o nome do arquivo lógico da exibição de catálogo `sys.database_files`, em que o tipo de arquivo é igual a `1` (log).  
  
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
Este exemplo retorna a ID de arquivo de um arquivo de texto completo. O snippet de código T-SQL seleciona o nome do arquivo lógico da exibição de catálogo `sys.database_files`, em que o tipo de arquivo é igual a `4` (texto completo). Este código retornará “NULL” se um catálogo de texto completo não existir.
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
