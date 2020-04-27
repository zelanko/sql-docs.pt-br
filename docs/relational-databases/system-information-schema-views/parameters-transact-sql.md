---
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e6d3880c4be8925e6b85a20af1324537e3977ecc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68103280"
---
# <a name="parameters-transact-sql"></a>PARAMETERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada parâmetro de uma função definida pelo usuário ou procedimento armazenado que podem ser acessados pelo usuário atual no banco de dados atual. Para funções, esta exibição retorna também uma linha com informações de valor de retorno.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar (** 128 **)**|Nome do catálogo da rotina para a qual este é um parâmetro.|  
|**SPECIFIC_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema da rotina para a qual este é um parâmetro.<br /><br /> <strong> \* Importante \* \* </strong> Não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
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
 [Exibições do sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [&#41;sys. Columns &#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
