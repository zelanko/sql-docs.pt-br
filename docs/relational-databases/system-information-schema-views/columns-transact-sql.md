---
title: COLUNAS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMNS
- COLUMNS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS view
- INFORMATION_SCHEMA.COLUMNS view
ms.assetid: bbf7ac4a-7444-4351-a590-a9f71e0bc495
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5a5d8039b34401bbe8cd11e6b9fb79320a35360b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811374"
---
# <a name="columns-transact-sql"></a>COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada coluna que pode ser acessada pelo usuário atual no banco de dados atual.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA * * *.** view_name *.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|Qualificador da tabela.|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|Nome do esquema que contém a tabela.<br /><br /> **\*\* Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|Nome da tabela.|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|Nome da coluna.|  
|**ORDINAL_POSITION**|**int**|Número de identificação da coluna.|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|Valor padrão da coluna.|  
|**IS_NULLABLE**|**varchar (** 3 **)**|Possibilidade de nulidade da coluna. Se essa coluna permitir NULL, essa coluna retornará YES. Caso contrário, será retornado NO.|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|Tipo de dados fornecido pelo sistema.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Comprimento máximo, em caracteres, de dados binários, dados de caracteres e dados de texto e imagem.<br /><br /> -1 para **xml** e dados de tipo de valor grande. Caso contrário, será retornado NULL. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Comprimento máximo, em bytes, de dados binários, dados de caracteres e dados de texto e imagem.<br /><br /> -1 para **xml** e dados de tipo de valor grande. Caso contrário, será retornado NULL.|  
|**NUMERIC_PRECISION**|**tinyint**|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|**NUMERIC_SCALE**|**int**|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|  
|**DATETIME_PRECISION**|**smallint**|Código de subtipo para **datetime** e ISO **intervalo** tipos de dados. Para outros tipos de dados, é retornado NULL.|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|Retorna **mestre**. Isso indica que o banco de dados no qual o conjunto de caracteres está localizado, se a coluna de dados de caractere ou **texto** tipo de dados. Caso contrário, será retornado NULL.|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|Sempre retorna NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|Retorna o nome exclusivo para o conjunto de caracteres se essa coluna é dados de caractere ou **texto** tipo de dados. Caso contrário, será retornado NULL.|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|Sempre retorna NULL.|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|Sempre retorna NULL.|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|Retorna o nome exclusivo para o agrupamento, se a coluna de dados de caractere ou **texto** tipo de dados. Caso contrário, será retornado NULL.|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|Se a coluna for do tipo de dados de alias, essa coluna será o nome do banco de dados no qual foi criado o tipo de dados definido pelo usuário. Caso contrário, será retornado NULL.|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|Se a coluna for do tipo de dados definido pelo usuário, essa coluna retornará o nome do esquema do tipo de dados definido pelo usuário. Caso contrário, será retornado NULL.<br /><br /> **\*\* Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um tipo de dados. O único modo seguro para localizar o esquema de um tipo é usar a função TYPEPROPERTY.|  
|**NOME_DO_DOMÍNIO**|**nvarchar(** 128 **)**|Se a coluna for do tipo de dados definido pelo usuário, essa coluna será o nome do tipo de dados definido pelo usuário. Caso contrário, será retornado NULL.|  
  
## <a name="remarks"></a>Comentários  
 O **ORDINAL_POSITION** coluna o **INFORMATION_SCHEMA. COLUNAS** exibição não é compatível com o padrão de bit de colunas retornadas pela função COLUMNS_UPDATED. Para obter um padrão de bit que é compatível com COLUMNS_UPDATED, você deve fazer referência a **ColumnID** propriedade da função de sistema COLUMNPROPERTY ao consultar o **INFORMATION_SCHEMA. COLUNAS** modo de exibição. Por exemplo:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys. syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
  
