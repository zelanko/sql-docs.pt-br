---
description: VIEWS (Transact-SQL)
title: EXIBIções (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEWS_TSQL
- VIEWS
dev_langs:
- TSQL
helpviewer_keywords:
- VIEWS view
- INFORMATION_SCHEMA.VIEWS view
ms.assetid: 6119bc94-0b22-45d4-a34b-967afd810a9d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c2e09f62858865c9ae1420efff17b0a3a0de9736
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482433"
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para exibições que podem ser acessadas pelo usuário atual no banco de dados atual.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Qualificador de exibição.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém a exibição.<br /><br /> **&#42;&#42; importante &#42;&#42;**  apenas uma maneira confiável de localizar o esquema de um objeto é consultar a exibição do catálogo sys. Objects.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|Nome da exibição.|  
|**VIEW_DEFINITION**|**nvarchar (** 4000 **)**|Se o comprimento da definição for maior que **nvarchar (** 4000 **)**, essa coluna será nula. Caso contrário, essa coluna será o texto de definição da exibição.|  
|**CHECK_OPTION**|**varchar (** 7 **)**|Tipo de WITH CHECK OPTION. Será CASCADE se a exibição original tiver sido criada usando WITH CHECK OPTION. Caso contrário, será retornado NONE.|  
|**IS_UPDATABLE**|**varchar (** 2 **)**|Especifica se a exibição é atualizável. Sempre retorna NO.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL ](../../t-sql/language-reference.md)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
