---
title: ARQUIVO (Transact-SQL) | Microsoft Docs
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
- FILEPROPERTY_TSQL
- FILEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- names [SQL Server], files
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTY function
- file names [SQL Server], FILEPROPERTY
ms.assetid: b82244ed-d623-431f-aa06-8017349d847f
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7078fecb77bad44fd6aa4c3ce0baf9565f1d6d3f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="fileproperty-transact-sql"></a>FILEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o valor de propriedade de nome de arquivo especificado quando são especificados um nome de arquivo no banco de dados atual e um nome de propriedade. Retorna NULL para arquivos que não estão no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FILEPROPERTY ( file_name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_name*  
 É uma expressão que contém o nome do arquivo associado ao banco de dados atual para o qual retornar as informações de propriedade. *file_name* é **nchar(128)**.  
  
 *propriedade*  
 É uma expressão que contém o nome da propriedade do arquivo a ser retornada. *propriedade* é **varchar (128)**, e pode ser um dos valores a seguir.  
  
|Valor|Description|Valor retornado|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|O grupo de arquivos é somente leitura.|1 = True<br /><br /> 0 = False<br /><br /> NULL = A entrada não é válida.|  
|**IsPrimaryFile**|Arquivo é o arquivo primário.|1 = True<br /><br /> 0 = False<br /><br /> NULL = A entrada não é válida.|  
|**IsLogFile**|Arquivo é um arquivo de log.|1 = True<br /><br /> 0 = False<br /><br /> NULL = A entrada não é válida.|  
|**SpaceUsed**|Quantidade de espaço usado pelo arquivo especificado.|Número de páginas alocadas no arquivo|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 *file_name* corresponde ao **nome** coluna o **sys. master_files** ou **sys. database_files** exibição do catálogo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a configuração para a propriedade `IsPrimaryFile` para o nome de arquivo `AdventureWorks_Data` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
  
SELECT FILEPROPERTY('AdventureWorks2012_Data', 'IsPrimaryFile')AS [Primary File];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Primary File   
-------------  
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [FILEGROUPPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

