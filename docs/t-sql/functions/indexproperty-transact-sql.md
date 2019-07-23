---
title: INDEXPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a2731f569ecf602c4aaa21e233ec671596e16ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024283"
---
# <a name="indexproperty-transact-sql"></a>INDEXPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o índice nomeado ou valor de propriedade de estatísticas de um número de identificação de tabela, índice ou nome de estatísticas e nome de propriedade especificados. Retorna NULL para índices XML.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
INDEXPROPERTY ( object_ID , index_or_statistics_name , property )   
```  
  
## <a name="arguments"></a>Argumentos  
 *object_ID*  
 É uma expressão que contém o número de identificação do objeto da tabela ou exibição indexada para o qual fornecer as informações de propriedade de índice. *object_ID* é **int**.  
  
 *index_or_statistics_name*  
 É uma expressão que contém o nome do índice ou estatísticas para o qual retornar as informações de propriedade. *index_or_statistics_name* é **nvarchar(128)** .  
  
 *property*  
 É uma expressão que contém o nome da propriedade do banco de dados a ser retornada. *property* é **varchar(128)** e pode ter um destes valores.  
  
> [!NOTE]  
>  A menos que indicado o contrário, NULL é retornado quando *property* não é um nome de propriedade válido, *object_ID* não é uma ID de objeto válida, *object_ID* é um tipo de objeto sem suporte para a propriedade especificada ou o chamador não tem permissão para exibir os metadados do objeto.  
  
|Propriedade|Descrição|Valor|  
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
|**IsStatistics**|*index_or_statistics_name* são as estatísticas criadas pela instrução CREATE STATISTICS ou pela opção AUTO_CREATE_STATISTICS de ALTER DATABASE.|1 = True<br /><br /> 0 = False ou índice XML.|  
|**IsUnique**|O índice é exclusivo.|1 = True<br /><br /> 0 = False ou índice XML.|  
|**IsColumnstore**|Índice é um índice columnstore xVelocity de memória otimizada.|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False| 
|**IsOptimizedForSequentialKey**|O índice tem a otimização para inserções de última página habilitada.|**Aplica-se a**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e posterior. <br><br>1 = True<br><br>0 = False| 
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas emissoras de metadados, como INDEXPROPERTY, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os valores das propriedades **IsClustered**, **IndexDepth** e **IndexFillFactor** para o índice `PK_Employee_BusinessEntityID` da tabela `Employee` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir examina as propriedades de um dos índices na tabela `FactResellerSales`.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Estatística](../../relational-databases/statistics/statistics.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

