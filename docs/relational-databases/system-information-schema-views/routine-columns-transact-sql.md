---
title: ROUTINE_COLUMNS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROUTINE_COLUMNS_TSQL
- ROUTINE_COLUMNS
dev_langs: TSQL
helpviewer_keywords:
- ROUTINE_COLUMNS view
- INFORMATION_SCHEMA.ROUTINE_COLUMNS view
ms.assetid: 91dbc61b-e4c0-4826-976c-b2fce88b7793
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3815c6db044ec66bae8eddd7bceb6ad69f29db61
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="routinecolumns-transact-sql"></a>ROUTINE_COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada coluna retornada pelas funções com valor de tabela que podem ser acessadas pelo usuário atual no banco de dados atual.  
  
 Para recuperar informações dessa exibição, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA.** *view_name*.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (**128**)**|Catálogo ou nome de banco de dados da função com valor de tabela.|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|Nome do esquema que contém a função com valor de tabela.<br /><br /> **\*\*Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**TABLE_NAME**|**nvarchar (**128**)**|Nome da função com valor de tabela.|  
|**NOME DA COLUNA**|**nvarchar (**128**)**|Nome da coluna.|  
|**ORDINAL_POSITION**|**int**|Número de identificação da coluna.|  
|**COLUMN_DEFAULT**|**nvarchar (**4000**)**|Valor padrão da coluna.|  
|**IS_NULLABLE**|**varchar (**3**)**|Se essa coluna permitir NULL, ela retornará YES. Caso contrário, retorna NO.|  
|**DATA_TYPE**|**nvarchar (**128**)**|Tipo de dados fornecido pelo sistema.|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|Comprimento máximo, em caracteres, de dados binários, dados de caracteres e dados de texto e imagem.<br /><br /> -1 para **xml** e dados de tipo de valor grande. Caso contrário, retorna NULL. Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).|  
|**CHARACTER_OCTET_LENGTH**|**int**|Comprimento máximo, em bytes, de dados binários, dados de caracteres e dados de texto e imagem.<br /><br /> -1 para **xml** e dados de tipo de valor grande. Caso contrário, retorna NULL.|  
|**NUMERIC_PRECISION**|**tinyint**|Precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**NUMERIC_SCALE**|**tinyint**|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, retorna NULL.|  
|**DATETIME_PRECISION**|**smallint**|Código de subtipo para **datetime** e ISO**inteiro** tipos de dados. Para outros tipos de dados, retorna NULL.|  
|**CHARACTER_SET_CATALOG**|**varchar (**6**)**|Retorna **mestre**. Isso indica que o banco de dados no qual o conjunto de caracteres se a coluna de dados de caractere ou **texto** tipo de dados. Caso contrário, retorna NULL.|  
|**CHARACTER_SET_SCHEMA**|**varchar (**3**)**|Sempre retorna NULL.|  
|**CHARACTER_SET_NAME**|**nvarchar (**128**)**|Retorna o nome exclusivo para o conjunto de caracteres se essa coluna é dados de caractere ou **texto** tipo de dados. Caso contrário, retorna NULL.|  
|**COLLATION_CATALOG**|**varchar (**6**)**|Sempre retorna NULL.|  
|**COLLATION_SCHEMA**|**varchar (**3**)**|Sempre retorna NULL.|  
|**COLLATION_NAME**|**nvarchar (**128**)**|Retorna o nome exclusivo para a ordem de classificação, se a coluna de dados de caractere ou **texto** tipo de dados. Caso contrário, retorna NULL.|  
|**DOMAIN_CATALOG**|**nvarchar (**128**)**|Se a coluna for do tipo de dados de alias, essa coluna será o nome do banco de dados no qual foi criado o tipo de dados definido pelo usuário. Caso contrário, retorna NULL.|  
|**DOMAIN_SCHEMA**|**nvarchar (**128**)**|Se a coluna for do tipo definido pelo usuário, essa coluna será o nome do esquema que contém o tipo de dados definido pelo usuário. Caso contrário, retorna NULL.<br /><br /> **\*\*Importante \* \***  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**NOME_DO_DOMÍNIO**|**nvarchar (**128**)**|Se a coluna for do tipo de dados definido pelo usuário, essa coluna será o nome do tipo de dados definido pelo usuário. Caso contrário, retorna NULL.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40; Transact-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
