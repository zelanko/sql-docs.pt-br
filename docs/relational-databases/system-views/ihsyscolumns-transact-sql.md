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
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs: TSQL
helpviewer_keywords: IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 347a3b691f2933cc4e3fbedcb3ddb59171da0108
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHsyscolumns** exibição expõe informações de coluna para artigos publicados de um publicador não SQL Server. Essa exibição é armazenada no distributiondatabase.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome da coluna ou do parâmetro do procedimento.|  
|**id**|**int**|A ID de objeto da tabela à qual essa coluna pertence ou a ID do procedimento armazenado com a qual esse parâmetro está associado.|  
|**tipoX**|**tinyint**|O tipo de armazenamento físico de [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|A ID do tipo de dados estendido definido pelo usuário.|  
|**comprimento**|**bigint**|O comprimento máximo de armazenamento físico de [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**XScale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|A ID da coluna ou do parâmetro.|  
|**deslocamento x**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reservado**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|A ID do padrão para essa coluna.|  
|**domínio**|**int**|A ID da regra ou restrição CHECK para essa coluna.|  
|**número**|**int**|O número de subprocedimentos quando o procedimento é agrupado (**0** para nenhuma entrada).|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deslocamento**|**int**|O deslocamento para a linha na qual essa coluna aparece.|  
|**collationid**|**int**|A ID de agrupamento da coluna. NULL para colunas que não são baseadas em caracteres.|  
|**idioma**|**int**|O identificador de idioma para a coluna.|  
|**status**|**int**|O bitmap usado para descrever uma propriedade da coluna ou do parâmetro:<br /><br /> **0x08** = coluna permite valores nulos.<br /><br /> **0x10** = o preenchimento ANSI estava em vigor quando **varchar** ou **varbinary** colunas foram adicionadas. Espaços em branco à direita são preservados para **varchar** e zeros à direita são preservados para **varbinary** colunas.<br /><br /> **0x40** = parâmetro é um parâmetro de saída.<br /><br /> **0x80** = coluna é uma coluna de identidade.|  
|**tipo**|**int**|O tipo de armazenamento físico de [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**usertype**|**tinyint**|A ID de tipo de dados definido pelo usuário [sys. systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|O nível de precisão para essa coluna.|  
|**escala**|**int**|A escala para essa coluna.|  
|**iscomputed**|**int**|O sinalizador que indica se a coluna é computada:<br /><br /> **0** = não computada.<br /><br /> **1** = computada.|  
|**isoutparam**|**int**|Indica se o parâmetro de procedimento é de saída:<br /><br /> **1** = true.<br /><br /> **0** = false.|  
|**IsNullable**|**int**|Indica se a coluna permite valores nulos:<br /><br /> **1** = true.<br /><br /> **0** = false.|  
|**agrupamento**|**int**|O nome de agrupamento da coluna. NULL para colunas que não são baseadas em caracteres.|  
|**tdscollation**|**int**|O nome do agrupamento da coluna quando retornado em um protocolo TDS (Tabular Data Stream).|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
