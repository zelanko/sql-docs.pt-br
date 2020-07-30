---
title: sys.syscolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-enginel, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8dcf0f88fed4ef48cc90a6057a757a205d9e56b
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396053"
---
# <a name="syssyscolumns-transact-sql"></a>sys.syscolumns (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada coluna em cada tabela e exibição, e uma linha para cada parâmetro em um procedimento armazenado no banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do parâmetro de coluna ou procedimento.|  
|**id**|**int**|A identificação do objeto da tabela à qual essa coluna pertence ou do procedimento armazenado ao qual esse parâmetro está associado.|  
|**xtype**|**tinyint**|Tipo de armazenamento físico de **Sys. Types**.|  
|**typestat**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|ID de tipo de dados estendido definido pelo usuário. Estoura ou retorna NULL se o número de tipos de dados exceder 32.767.|  
|**length**|**smallint**|Comprimento máximo do armazenamento físico de **Sys**. **tipos**.|  
|**xprec**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**smallint**|ID de coluna ou de parâmetro.|  
|**xoffset**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reservado**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|ID do padrão para essa coluna.|  
|**controlador**|**int**|ID da regra ou restrição CHECK para essa coluna.|  
|**number**|**smallint**|Número de subprocedimentos quando o procedimento é agrupado.<br /><br /> 0 = Nenhuma entrada de procedimento|  
|**colorder**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**varbinary(8000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**smallint**|Deslocamento da linha na qual essa coluna aparece.|  
|**CollationID**|**int**|ID da ordenação da coluna. NULL para colunas não baseadas em caracteres.|  
|**status**|**tinyint**|Bitmap usado para descrever uma propriedade da coluna ou do parâmetro:<br /><br /> 0x08 = A coluna permite valores nulos.<br /><br /> 0x10 = o preenchimento ANSI estava em vigor quando colunas **varchar** ou **varbinary** foram adicionadas. Os espaços em branco à direita são preservados para os zeros **varchar** e à direita são preservados para colunas **varbinary** .<br /><br /> 0x40 = O parâmetro é OUTPUT.<br /><br /> 0x80 = A coluna é de identidade.|  
|**tipo**|**tinyint**|Tipo de armazenamento físico de **Sys**. **tipos**.|  
|**UserType**|**smallint**|ID do tipo de dados definido pelo usuário de **Sys. Types**. Estoura ou retorna NULL se o número de tipos de dados exceder 32.767.|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**smallint**|Nível de precisão para essa coluna.<br /><br /> -1 = **XML** ou tipo de valor grande.|  
|**scale**|**int**|Tamanho dessa coluna.<br /><br /> NULL = Tipo de dados é não numérico.|  
|**iscomputad**|**int**|Sinalizador que indica se a coluna é computada:<br /><br /> 0 = Não computada<br /><br /> 1 = Computada|  
|**isoutparam**|**int**|Indica se o parâmetro de procedimento é de saída:<br /><br /> 1 = True<br /><br /> 0 = False|  
|**IsNullable**|**int**|Indica se a coluna permite valores nulos:<br /><br /> 1 = True<br /><br /> 0 = False|  
|**Agrupamento**|**sysname**|Nome da ordenação da coluna. NULL se não for uma coluna baseada em caracteres.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
