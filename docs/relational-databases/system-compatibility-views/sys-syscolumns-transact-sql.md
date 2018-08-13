---
title: sys.syscolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-enginel, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.syscolumns
- sys.syscolumns_TSQL
- syscolumns_TSQL
- syscolumns
dev_langs:
- TSQL
helpviewer_keywords:
- syscolumns system table
- sys.syscolumns compatibility view
ms.assetid: 863fd87b-ff33-4ac5-9aa9-df21140681da
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ed20abe081acad3ef1c653f3041006c6453e4607
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540636"
---
# <a name="syssyscolumns-transact-sql"></a>sys.syscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna uma linha para cada coluna em cada tabela e exibição, e uma linha para cada parâmetro em um procedimento armazenado no banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da coluna ou procedimento do parâmetro.|  
|**id**|**int**|A identificação do objeto da tabela à qual essa coluna pertence ou do procedimento armazenado ao qual esse parâmetro está associado.|  
|**tipoX**|**tinyint**|Tipo de armazenamento físico de **Types**.|  
|**typestat**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|ID de tipo de dados estendido definido pelo usuário. Estoura ou retorna NULL se o número de tipos de dados exceder 32.767.|  
|**Comprimento**|**smallint**|Comprimento máximo de armazenamento físico de **sys**. **tipos de**.|  
|**xprec**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**smallint**|ID de coluna ou de parâmetro.|  
|**xoffset**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|ID do padrão para essa coluna.|  
|**domain**|**int**|ID da regra ou restrição CHECK para essa coluna.|  
|**number**|**smallint**|Número de subprocedimentos quando o procedimento é agrupado.<br /><br /> 0 = Nenhuma entrada de procedimento|  
|**colorder**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**varbinary(8000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**smallint**|Deslocamento da linha na qual essa coluna aparece.|  
|**collationid**|**int**|ID do agrupamento da coluna. NULL para colunas não baseadas em caracteres.|  
|**status**|**tinyint**|Bitmap usado para descrever uma propriedade da coluna ou do parâmetro:<br /><br /> 0x08 = A coluna permite valores nulos.<br /><br /> 0x10 = o preenchimento ANSI estava em vigor quando **varchar** ou **varbinary** colunas foram adicionadas. Espaços em branco são preservados por **varchar** e zeros à direita são preservados por **varbinary** colunas.<br /><br /> 0x40 = O parâmetro é OUTPUT.<br /><br /> 0x80 = A coluna é de identidade.|  
|**type**|**tinyint**|Tipo de armazenamento físico de **sys**. **tipos de**.|  
|**usertype**|**smallint**|ID de tipo de dados definido pelo usuário **Types**. Estoura ou retorna NULL se o número de tipos de dados exceder 32.767.|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**smallint**|Nível de precisão para essa coluna.<br /><br /> -1 = **xml** ou tipo de valor grande.|  
|**scale**|**int**|Tamanho dessa coluna.<br /><br /> NULL = Tipo de dados é não numérico.|  
|**iscomputed**|**int**|Sinalizador que indica se a coluna é computada:<br /><br /> 0 = Não computada<br /><br /> 1 = Computada|  
|**isoutparam**|**int**|Indica se o parâmetro de procedimento é de saída:<br /><br /> 1 = True<br /><br /> 0 = False|  
|**isnullable**|**int**|Indica se a coluna permite valores nulos:<br /><br /> 1 = True<br /><br /> 0 = False|  
|**Agrupamento**|**sysname**|Nome do agrupamento da coluna. NULL se não for uma coluna baseada em caracteres.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
