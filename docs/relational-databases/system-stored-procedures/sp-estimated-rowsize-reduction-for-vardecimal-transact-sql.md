---
title: sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- sp_estimated_rowsize_reduction_for_vardecimal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- decimal data type, compressing
- numeric data type, compressing
- estimate decimal compression
- table compression [SQL Server]
ms.assetid: 0fe45983-f9f2-4c7f-938a-0fd96e1cbe8d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1d699e62251f8f2c750795d2389f338e9bd1bf11
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33247055"
---
# <a name="spestimatedrowsizereductionforvardecimal-transact-sql"></a>sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Estimará a redução do tamanho médio das linhas se você habilitar o formato de armazenamento vardecimal em uma tabela. Use este número para estimar a redução global do tamanho da tabela. Como a amostragem estatística é usada para calcular a redução média do tamanho da linha, considere-a apenas como uma estimativa. Em casos raros, o tamanho da linha pode aumentar após o formato de armazenamento vardecimal ser habilitado.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use compactação ROW e PAGE. Para obter mais informações, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md). Para efeitos de compactação no tamanho de tabelas e índices, consulte [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_estimated_rowsize_reduction_for_vardecimal [ [ @table_name = ] 'table'] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table=** ] **'***tabela***'**  
 É o nome de três partes da tabela para a qual o formato de armazenamento deve ser alterado. *tabela* é **nvarchar(776)**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O conjunto de resultados a seguir é retornado para fornecer informações de tamanho do banco de dados estimado e atual.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**avg_rowlen_fixed_format**|**decimal (12, 2)**|Representa o comprimento da linha em formato de armazenamento decimal fixo.|  
|**avg_rowlen_vardecimal_format**|**decimal (12, 2)**|Representa o tamanho médio da linha quando o formato de armazenamento vardecimal é usado.|  
|**row_count**|**Int**|Número de linhas na tabela.|  
  
## <a name="remarks"></a>Remarks  
 Use **sp_estimated_rowsize_reduction_for_vardecimal** para estimar o aumento resultante se você habilitar uma tabela para o formato de armazenamento vardecimal. Por exemplo, se o tamanho médio da linha puder ser reduzido em 40%, potencialmente, você poderá reduzir o tamanho da tabela em 40%. Dependendo do fator de preenchimento e do tamanho da linha, um aumento de espaço poderá não ser obtido. Por exemplo, se você tiver uma linha de 8000 bytes de comprimento e reduzir seu tamanho em 40%, ainda poderá ajustar apenas uma linha em uma página de dados, resultando em nenhum aumento.  
  
 Se os resultados de **sp_estimated_rowsize_reduction_for_vardecimal** indicar que a tabela crescerá, isso significa que muitas linhas na tabela usam aproximadamente a precisão inteira dos tipos de dados decimais e a adição da pequena sobrecarga necessária para formato de armazenamento vardecimal é maior que o aumento do formato de armazenamento vardecimal. Nesse caso raro, não habilite o formato de armazenamento vardecimal.  
  
 Se uma tabela estiver habilitada para o formato de armazenamento vardecimal, use **sp_estimated_rowsize_reduction_for_vardecimal** para estimar o tamanho médio da linha se o formato de armazenamento vardecimal estiver desabilitado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na tabela.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir estimará a redução do tamanho da linha, se a tabela `Production.WorkOrderRouting` no banco de dados `AdventureWorks2012` estiver compactada.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimated_rowsize_reduction_for_vardecimal 'Production.WorkOrderRouting' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_db_vardecimal_storage_format &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
