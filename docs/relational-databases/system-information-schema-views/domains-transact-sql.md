---
title: DOMÍNIOS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAINS_TSQL
- DOMAINS
dev_langs:
- TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1c47c9e1f03436923332a6f3beee49a0b4a6ef43
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85647475"
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada tipo de dados de alias que pode ser acessado pelo usuário atual no banco de dados atual.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|Banco de dados no qual o tipo de dados de alias existe.|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém o tipo de dados do alias.<br /><br /> **&#42;&#42; importantes &#42;&#42;** Não use INFORMATION_SCHEMA exibições para determinar o esquema de um tipo de dados. O único modo seguro para localizar o esquema de um tipo é usar a função TYPEPROPERTY.|  
|**DOMAIN_NAME**|**sysname**|Tipo de dados de alias.|  
|**DATA_TYPE**|**sysname**|Tipo de dados fornecido pelo sistema.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Comprimento máximo, em caracteres, de dados binários, dados de caracteres e dados de texto e imagem.<br /><br /> -1 para **XML** e dados de tipo de valor grande. Caso contrário, será retornado NULL. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Comprimento máximo, em bytes, de dados binários, dados de caracteres e dados de texto e imagem.<br /><br /> -1 para **XML** e dados de tipo de valor grande. Caso contrário, será retornado NULL.|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|Sempre retorna NULL.|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|Sempre retorna NULL.|  
|**COLLATION_NAME**|**nvarchar (** 128 **)**|Retorna o nome exclusivo da ordem de classificação se a coluna for de dados de caracteres ou tipo de dados de **texto** . Caso contrário, será retornado NULL.|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|Retorna o **mestre**. Isso indica o banco de dados no qual o conjunto de caracteres está localizado, se a coluna for um tipo de dados de caractere ou de **texto** . Caso contrário, será retornado NULL.|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|Sempre retorna NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar (** 128 **)**|Retorna o nome exclusivo para o conjunto de caracteres se esta coluna for de dados de caracteres ou tipo de dados de **texto** . Caso contrário, será retornado NULL.|  
|**NUMERIC_PRECISION**|**tinyint**|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|**DATETIME_PRECISION**|**smallint**|Código de subtipo para tipo de dados **DateTime** e **intervalo** ISO. Para outros tipos de dados, essa coluna retorna um valor nulo.|  
|**DOMAIN_DEFAULT**|**nvarchar (** 4000 **)**|Texto real da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] de definição.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
