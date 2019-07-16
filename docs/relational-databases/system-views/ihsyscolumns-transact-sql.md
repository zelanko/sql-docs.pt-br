---
title: IHsyscolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: a432685809676f997049940ea5aa1ce43dc38a60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029633"
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHsyscolumns** exibição expõe informações de coluna para artigos publicados a partir de um publicador não SQL Server. Essa exibição é armazenada no distributiondatabase.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome da coluna ou do parâmetro do procedimento.|  
|**id**|**int**|A ID de objeto da tabela à qual essa coluna pertence ou a ID do procedimento armazenado com a qual esse parâmetro está associado.|  
|**tipoX**|**tinyint**|O tipo de armazenamento físico de [sys. systypes &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|A ID do tipo de dados estendido definido pelo usuário.|  
|**length**|**bigint**|O comprimento máximo de armazenamento físico da [sys. systypes &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|A ID da coluna ou do parâmetro.|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|A ID do padrão para essa coluna.|  
|**domain**|**int**|A ID da regra ou restrição CHECK para essa coluna.|  
|**number**|**int**|O número de subprocedimentos quando o procedimento é agrupado (**0** para entradas de não procedimento).|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**int**|O deslocamento para a linha na qual essa coluna aparece.|  
|**collationid**|**int**|A ID de ordenação da coluna. NULL para colunas que não são baseadas em caracteres.|  
|**language**|**int**|O identificador de idioma para a coluna.|  
|**status**|**int**|O bitmap usado para descrever uma propriedade da coluna ou do parâmetro:<br /><br /> **0x08** = coluna permite valores nulos.<br /><br /> **0x10** = o preenchimento ANSI estava em vigor quando **varchar** ou **varbinary** colunas foram adicionadas. Espaços em branco são preservados por **varchar** e zeros à direita são preservados por **varbinary** colunas.<br /><br /> **0x40** = parâmetro é um parâmetro de saída.<br /><br /> **0x80** = coluna é uma coluna de identidade.|  
|**type**|**int**|O tipo de armazenamento físico de [sys. systypes &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**usertype**|**tinyint**|A ID de tipo de dados definido pelo usuário [sys. systypes &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|O nível de precisão para essa coluna.|  
|**scale**|**int**|A escala para essa coluna.|  
|**iscomputed**|**int**|O sinalizador que indica se a coluna é computada:<br /><br /> **0** = não computada.<br /><br /> **1** = computada.|  
|**isoutparam**|**int**|Indica se o parâmetro de procedimento é de saída:<br /><br /> **1** = true.<br /><br /> **0** = false.|  
|**isnullable**|**int**|Indica se a coluna permite valores nulos:<br /><br /> **1** = true.<br /><br /> **0** = false.|  
|**Agrupamento**|**int**|O nome de ordenação da coluna. NULL para colunas que não são baseadas em caracteres.|  
|**tdscollation**|**int**|O nome da ordenação da coluna quando retornado em um protocolo TDS (Tabular Data Stream).|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
