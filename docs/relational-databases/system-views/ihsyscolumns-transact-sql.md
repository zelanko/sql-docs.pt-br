---
title: IHsyscolumns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 416b4256f162ee76c10f56aa06a3f952b77e872b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHsyscolumns** exibição expõe informações de coluna para artigos publicados de um publicador não SQL Server. Essa exibição é armazenada no distributiondatabase.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome da coluna ou do parâmetro do procedimento.|  
|**id**|**Int**|A ID de objeto da tabela à qual essa coluna pertence ou a ID do procedimento armazenado com a qual esse parâmetro está associado.|  
|**xtype**|**tinyint**|O tipo de armazenamento físico de [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**typestat**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|A ID do tipo de dados estendido definido pelo usuário.|  
|**comprimento**|**bigint**|O comprimento máximo de armazenamento físico de [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**xprec**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**Int**|A ID da coluna ou do parâmetro.|  
|**xoffset**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**Int**|A ID do padrão para essa coluna.|  
|**domain**|**Int**|A ID da regra ou restrição CHECK para essa coluna.|  
|**number**|**Int**|O número de subprocedimentos quando o procedimento é agrupado (**0** para nenhuma entrada).|  
|**colorder**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**Int**|O deslocamento para a linha na qual essa coluna aparece.|  
|**collationid**|**Int**|A ID de agrupamento da coluna. NULL para colunas que não são baseadas em caracteres.|  
|**language**|**Int**|O identificador de idioma para a coluna.|  
|**status**|**Int**|O bitmap usado para descrever uma propriedade da coluna ou do parâmetro:<br /><br /> **0x08** = coluna permite valores nulos.<br /><br /> **0x10** = o preenchimento ANSI estava em vigor quando **varchar** ou **varbinary** colunas foram adicionadas. Espaços em branco à direita são preservados para **varchar** e zeros à direita são preservados para **varbinary** colunas.<br /><br /> **0x40** = parâmetro é um parâmetro de saída.<br /><br /> **0x80** = coluna é uma coluna de identidade.|  
|**type**|**Int**|O tipo de armazenamento físico de [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**usertype**|**tinyint**|A ID de tipo de dados definido pelo usuário [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**printfmt**|**Int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**Int**|O nível de precisão para essa coluna.|  
|**scale**|**Int**|A escala para essa coluna.|  
|**iscomputed**|**Int**|O sinalizador que indica se a coluna é computada:<br /><br /> **0** = não computada.<br /><br /> **1** = computada.|  
|**isoutparam**|**Int**|Indica se o parâmetro de procedimento é de saída:<br /><br /> **1** = true.<br /><br /> **0** = false.|  
|**isnullable**|**Int**|Indica se a coluna permite valores nulos:<br /><br /> **1** = true.<br /><br /> **0** = false.|  
|**collation**|**Int**|O nome de agrupamento da coluna. NULL para colunas que não são baseadas em caracteres.|  
|**tdscollation**|**Int**|O nome do agrupamento da coluna quando retornado em um protocolo TDS (Tabular Data Stream).|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
