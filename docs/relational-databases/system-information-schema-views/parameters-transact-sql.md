---
title: PARÂMETROS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9b73215f275f2171f72a70a71f1855d88d60c034
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="parameters-transact-sql"></a>PARAMETERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada parâmetro de uma função definida pelo usuário ou procedimento armazenado que podem ser acessados pelo usuário atual no banco de dados atual. Para funções, esta exibição retorna também uma linha com informações de valor de retorno.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA. * * * view_name*.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar(** 128 **)**|Nome do catálogo da rotina para a qual este é um parâmetro.|  
|**SPECIFIC_SCHEMA**|**nvarchar(** 128 **)**|Nome do esquema da rotina para a qual este é um parâmetro.<br /><br /> **\*\* Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**SPECIFIC_NAME**|**nvarchar(** 128 **)**|Nome da rotina para a qual este é um parâmetro.|  
|**ORDINAL_POSITION**|**Int**|A posição ordinal do parâmetro começando em 1. Para o valor de retorno de uma função, este é um 0.|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|Retorna IN no caso de um parâmetro de entrada, OUT no caso de um parâmetro de saída e INOUT no caso de um parâmetro de entrada/saída.|  
|**IS_RESULT**|**nvarchar (** 10 **)**|Retorna YES se indica o resultado da rotina que é uma função. Caso contrário, retorna NO.|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|Retorna YES se declarado como localizador. Caso contrário, retorna NO.|  
|**PARAMETER_NAME**|**nvarchar(** 128 **)**|Nome do parâmetro. NULL se isto corresponder ao valor de retorno de uma função.|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|Tipo de dados fornecido pelo sistema.|  
|**CHARACTER_MAXIMUM_LENGTH**|**Int**|Comprimento máximo em caracteres para tipos de dados binários ou de caractere.<br /><br /> -1 para **xml** e dados de tipo de valor grande. Caso contrário, retorna NULL.|  
|**CHARACTER_OCTET_LENGTH**|**Int**|Comprimento máximo em bytes para tipos de dados binários ou de caractere.<br /><br /> -1 para **xml** e dados de tipo de valor grande. Caso contrário, retorna NULL.|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|Sempre retorna NULL.|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|Sempre retorna NULL.|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|Nome do agrupamento do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|O nome de catálogo do conjunto de caracteres do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|Sempre retorna NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|O nome do conjunto de caracteres do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|**NUMERIC_PRECISION**|**tinyint**|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**DATETIME_PRECISION**|**smallint**|Precisão em segundos fracionários se o tipo de parâmetro for **datetime** ou **smalldatetime**. Caso contrário, retorna NULL.|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL. Reservado para uso futuro.|  
|**INTERVAL_PRECISION**|**smallint**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar(** 128 **)**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar(** 128 **)**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar(** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_CATALOG**|**nvarchar(** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_SCHEMA**|**nvarchar(** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_NAME**|**nvarchar(** 128 **)**|NULL. Reservado para uso futuro.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. Parameters & #40; Transact-SQL & #41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
