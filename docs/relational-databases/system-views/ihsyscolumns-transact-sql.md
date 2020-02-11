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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029633"
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A exibição **IHsyscolumns** expõe informações de coluna para artigos publicados de um Publicador não SQL Server. Essa exibição é armazenada no DistributionDatabase.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome da coluna ou do parâmetro do procedimento.|  
|**sessão**|**int**|A ID de objeto da tabela à qual essa coluna pertence ou a ID do procedimento armazenado com a qual esse parâmetro está associado.|  
|**xtype**|**tinyint**|O tipo de armazenamento físico de [Sys. systypes &#40;&#41;Transact-SQL ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|A ID do tipo de dados estendido definido pelo usuário.|  
|**muito**|**bigint**|O comprimento máximo do armazenamento físico de [Sys. systypes &#40;&#41;Transact-SQL ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|A ID da coluna ou do parâmetro.|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reservado**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|A ID do padrão para essa coluna.|  
|**controlador**|**int**|A ID da regra ou restrição CHECK para essa coluna.|  
|**number**|**int**|O número do Subprocedimento quando o procedimento é agrupado (**0** para entradas não de procedimento).|  
|**cosenhor**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**desvio**|**int**|O deslocamento para a linha na qual essa coluna aparece.|  
|**CollationID**|**int**|A ID de ordenação da coluna. NULL para colunas que não são baseadas em caracteres.|  
|**linguagem**|**int**|O identificador de idioma para a coluna.|  
|**Estado**|**int**|O bitmap usado para descrever uma propriedade da coluna ou do parâmetro:<br /><br /> **0x08** = Column permite valores nulos.<br /><br /> **0x10** = o preenchimento ANSI estava em vigor quando colunas **varchar** ou **varbinary** foram adicionadas. Os espaços em branco à direita são preservados para os zeros **varchar** e à direita são preservados para colunas **varbinary** .<br /><br /> **0x40** = Parameter é um parâmetro de saída.<br /><br /> **0x80** = Column é uma coluna de identidade.|  
|**tipo**|**int**|O tipo de armazenamento físico de [Sys. systypes &#40;&#41;Transact-SQL ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**usertype**|**tinyint**|A ID do tipo de dados definido pelo usuário de [Sys. systypes &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|O nível de precisão para essa coluna.|  
|**scale**|**int**|A escala para essa coluna.|  
|**iscomputad**|**int**|O sinalizador que indica se a coluna é computada:<br /><br /> **0** = não computado.<br /><br /> **1** = computado.|  
|**isoutparam**|**int**|Indica se o parâmetro de procedimento é de saída:<br /><br /> **1** = true.<br /><br /> **0** = falso.|  
|**IsNullable**|**int**|Indica se a coluna permite valores nulos:<br /><br /> **1** = true.<br /><br /> **0** = falso.|  
|**Agrupamento**|**int**|O nome de ordenação da coluna. NULL para colunas que não são baseadas em caracteres.|  
|**tdscollation**|**int**|O nome da ordenação da coluna quando retornado em um protocolo TDS (Tabular Data Stream).|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
