---
description: PARAMETERS (Transact-SQL)
title: PARÂMETROS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 46360eac7080f92f98ba3f081b7cd9ec505f12c9
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753554"
---
# <a name="parameters-transact-sql"></a>PARAMETERS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada parâmetro de uma função definida pelo usuário ou procedimento armazenado que podem ser acessados pelo usuário atual no banco de dados atual. Para funções, esta exibição retorna também uma linha com informações de valor de retorno.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar (** 128 **)**|Nome do catálogo da rotina para a qual este é um parâmetro.|  
|**SPECIFIC_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema da rotina para a qual este é um parâmetro.<br /><br /> Importante não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. <strong> \* \* \* \* </strong> INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**SPECIFIC_NAME**|**nvarchar (** 128 **)**|Nome da rotina para a qual este é um parâmetro.|  
|**ORDINAL_POSITION**|**int**|A posição ordinal do parâmetro começando em 1. Para o valor de retorno de uma função, este é um 0.|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|Retorna IN no caso de um parâmetro de entrada, OUT no caso de um parâmetro de saída e INOUT no caso de um parâmetro de entrada/saída.|  
|**IS_RESULT**|**nvarchar (** 10 **)**|Retorna YES se indica o resultado da rotina que é uma função. Caso contrário, retorna NO.|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|Retorna YES se declarado como localizador. Caso contrário, retorna NO.|  
|**PARAMETER_NAME**|**nvarchar (** 128 **)**|Nome do parâmetro. NULL se isto corresponder ao valor de retorno de uma função.|  
|**DATA_TYPE**|**nvarchar (** 128 **)**|Tipo de dados fornecido pelo sistema.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Comprimento máximo em caracteres para tipos de dados binários ou de caractere.<br /><br /> -1 para **XML** e dados de tipo de valor grande. Caso contrário, retorna NULL.|  
|**CHARACTER_OCTET_LENGTH**|**int**|Comprimento máximo em bytes para tipos de dados binários ou de caractere.<br /><br /> -1 para **XML** e dados de tipo de valor grande. Caso contrário, retorna NULL.|  
|**COLLATION_CATALOG**|**nvarchar (** 128 **)**|Sempre retorna NULL.|  
|**COLLATION_SCHEMA**|**nvarchar (** 128 **)**|Sempre retorna NULL.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|Nome da ordenação do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|**CHARACTER_SET_CATALOG**|**nvarchar (** 128 **)**|O nome de catálogo do conjunto de caracteres do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar (** 128 **)**|Sempre retorna NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|O nome do conjunto de caracteres do parâmetro. Se não for um dos tipos de caractere, retorna NULL.|  
|**NUMERIC_PRECISION**|**tinyint**|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**DATETIME_PRECISION**|**smallint**|Precisão em segundos fracionários se o tipo de parâmetro for **DateTime** ou **smalldatetime**. Caso contrário, retorna NULL.|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL. Reservado para uso futuro.|  
|**INTERVAL_PRECISION**|**smallint**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_CATALOG**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_SCHEMA**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|**SCOPE_NAME**|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL ](../../t-sql/language-reference.md)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
