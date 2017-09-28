---
title: INDEXPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INDEXPROPERTY
- INDEXPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INDEXPROPERTY function
- indexes [SQL Server], viewing
- indexes [SQL Server], properties
ms.assetid: 998d5788-4871-44a8-8125-0d9390868b84
caps.latest.revision: 56
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cbd10b32ee6b2d88a97222c3a970452a4a628b83
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="indexproperty-transact-sql"></a>INDEXPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o índice nomeado ou valor de propriedade de estatísticas de um número de identificação de tabela, índice ou nome de estatísticas e nome de propriedade especificados. Retorna NULL para índices XML.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
INDEXPROPERTY ( object_ID , index_or_statistics_name , property )   
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 É uma expressão que contém o número de identificação do objeto da tabela ou exibição indexada para o qual fornecer as informações de propriedade de índice. *object_id* é **int**.  
  
 *index_or_statistics_name*  
 É uma expressão que contém o nome do índice ou estatísticas para o qual retornar as informações de propriedade. *index_or_statistics_name* é **nvarchar (128)**.  
  
 *propriedade*  
 É uma expressão que contém o nome da propriedade do banco de dados a ser retornada. *propriedade* é **varchar (128)**, e pode ser um destes valores.  
  
> [!NOTE]  
>  A menos que indicado em contrário, NULL é retornado quando *propriedade* não é um nome de propriedade válido, *object_ID* não é uma ID de objeto válido, *object_ID* é um tipo de objeto sem suporte para a propriedade especificada ou o chamador não tem permissão para exibir os metadados do objeto.  
  
|Propriedade|Description|Valor|  
|--------------|-----------------|-----------|  
|**IndexDepth**|Profundidade do índice.|Número de níveis de índice.<br /><br /> NULL = O índice XML ou saída não é válido.|  
|**IndexFillFactor**|Valor do fator de preenchimento usado quando o índice foi criado ou reconstruído pela última vez.|Fator de preenchimento|  
|**IndexID**|ID de índice do índice em uma tabela ou exibição indexada especificada.|ID de índice|  
|**IsAutoStatistics**|Estatísticas foram geradas pela opção AUTO_CREATE_STATISTICS de ALTER DATABASE.|1 = True<br /><br /> 0 = False ou índice XML.|  
|**IsClustered**|O índice é clusterizado.|1 = True<br /><br /> 0 = False ou índice XML.|  
|**IsDisabled**|O índice está desabilitado.|1 = True<br /><br /> 0 = False<br /><br /> NULL = A entrada não é válida.|  
|**IsFulltextKey**|O índice é o texto completo e a chave de indexação semântica de uma tabela.|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False ou índice XML.<br /><br /> NULL = A entrada não é válida.|  
|**IsHypothetical**|O índice é hipotético e não pode ser usado diretamente como um caminho de acesso de dados. Os índices hipotéticos retêm estatísticas do nível de coluna e são mantidos e usados pelo Orientador de Otimização do Mecanismo de Banco de Dados.|1 = True<br /><br /> 0 = False ou índice XML<br /><br /> NULL = A entrada não é válida.|  
|**IsPadIndex**|O índice especifica o espaço a ser deixado aberto em cada nó interior.|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False ou índice XML.|  
|**IsPageLockDisallowed**|Valor de bloqueio de página definido pela opção ALLOW_PAGE_LOCKS de ALTER INDEX.|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = O bloqueio de página não é permitido.<br /><br /> 0 = O bloqueio de página é permitido.<br /><br /> NULL = A entrada não é válida.|  
|**IsRowLockDisallowed**|Valor de bloqueio de linha definido pela opção ALLOW_ROW_LOCKS de ALTER INDEX.|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = O bloqueio de linha não é permitido.<br /><br /> 0 = O bloqueio de linha é permitido.<br /><br /> NULL = A entrada não é válida.|  
|**IsStatistics**|*index_or_statistics_name* é estatísticas criadas pela instrução CREATE STATISTICS ou pela opção AUTO_CREATE_STATISTICS de ALTER DATABASE.|1 = True<br /><br /> 0 = False ou índice XML.|  
|**IsUnique**|O índice é exclusivo.|1 = True<br /><br /> 0 = False ou índice XML.|  
|**IsColumnstore**|Índice é um índice columnstore xVelocity de memória otimizada.|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas emissoras de metadados, como INDEXPROPERTY, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os valores para o **IsClustered**, **IndexDepth**, e **IndexFillFactor** propriedades para o `PK`_`Employee` \_ `BusinessEntityID` índice da `Employee` tabela o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.  
  
```  
SELECT   
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IsClustered')AS [Is Clustered],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexDepth') AS [Index Depth],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexFillFactor') AS [Fill Factor];  
  
```  
  
 Este é o conjunto de resultados:  
  
```  
Is Clustered Index Depth Fill Factor   
------------ ----------- -----------   
1            2           0  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir examina as propriedades de um dos índices no `FactResellerSales` tabela.  
  
```  
-- Uses AdventureWorks  
  
SELECT   
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsClustered') AS [Is Clustered],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsColumnstore') AS [Is Columnstore Index],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IndexFillFactor') AS [Fill Factor];  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Estatísticas](../../relational-databases/statistics/statistics.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [stats_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  


