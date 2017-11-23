---
title: "Exibições de esquema de informações do sistema (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- information schema views
- schemas [SQL Server], information schema views
- metadata [SQL Server], views
- views [SQL Server], information schema
- system views [SQL Server], information schema
ms.assetid: 7e9f1dfe-27e9-40e7-8fc7-bfc5cae6be10
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 361e6385eb14d6ea3ae2826c1b8aa184c167e50a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="system-information-schema-views-transact-sql"></a>Exibições de esquema de informações do sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Uma exibição de esquema de informações é um dos vários métodos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecidos para obtenção de metadados. As exibições de esquema de informações fornecem uma exibição interna independente da tabela do sistema dos metadados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Exibições de esquema de informações permitem que os aplicativos trabalhem corretamente embora alterações significativas tenham sido feitas nas tabelas do sistema subjacentes. As exibições de esquema de informações incluídas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão em conformidade com a definição padrão ISO para o INFORMATION_SCHEMA.  
  
> [!IMPORTANT]  
>  Algumas alterações feitas nas exibições do esquema de informações quebram a compatibilidade com versões anteriores. Essas alterações são descritas nos tópicos das exibições específicas.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a uma convenção de nomenclatura de três partes quando você faz uma referência ao servidor atual. O padrão ISO também oferece suporte a uma convenção de nomenclatura de três partes. Entretanto, os nomes usados em ambas as convenções de nomenclatura são diferentes. As exibições de esquema de informações são definidas em um esquema especial chamado INFORMATION_SCHEMA. Esse esquema está contido em cada banco de dados. Cada exibição de esquema de informações contém metadados para todos os objetos de dados armazenados naquele banco de dados específico. A tabela a seguir mostra as relações entre os nomes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os nomes SQL padrão.  
  
|Nome do SQL Server|Mapeia para seu nome SQL padrão equivalente|  
|---------------------|-----------------------------------------------|  
|Banco de Dados|Catálogo|  
|esquema|esquema|  
|Objeto|Objeto|  
|tipo de dados definido pelo usuário|Domínio|  
  
 Esta convenção de mapeamento de nome se aplica às seguintes exibições compatíveis com ISO [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|||  
|-|-|  
|[CHECK_CONSTRAINTS](../../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)|[REFERENTIAL_CONSTRAINTS](../../relational-databases/system-information-schema-views/referential-constraints-transact-sql.md)|  
|[COLUMN_DOMAIN_USAGE](../../relational-databases/system-information-schema-views/column-domain-usage-transact-sql.md)|[ROUTINES](../../relational-databases/system-information-schema-views/routines-transact-sql.md)|  
|[COLUMN_PRIVILEGES](../../relational-databases/system-information-schema-views/column-privileges-transact-sql.md)|[ROUTINE_COLUMNS](../../relational-databases/system-information-schema-views/routine-columns-transact-sql.md)|  
|[COLUMNS](../../relational-databases/system-information-schema-views/columns-transact-sql.md)|[SCHEMATA](../../relational-databases/system-information-schema-views/schemata-transact-sql.md)|  
|[CONSTRAINT_COLUMN_USAGE](../../relational-databases/system-information-schema-views/constraint-column-usage-transact-sql.md)|[TABLE_CONSTRAINTS](../../relational-databases/system-information-schema-views/table-constraints-transact-sql.md)|  
|[CONSTRAINT_TABLE_USAGE](../../relational-databases/system-information-schema-views/constraint-table-usage-transact-sql.md)|[TABLE_PRIVILEGES](../../relational-databases/system-information-schema-views/table-privileges-transact-sql.md)|  
|[DOMAIN_CONSTRAINTS](../../relational-databases/system-information-schema-views/domain-constraints-transact-sql.md)|[TABLES](../../relational-databases/system-information-schema-views/tables-transact-sql.md)|  
|[DOMAINS](../../relational-databases/system-information-schema-views/domains-transact-sql.md)|[VIEW_COLUMN_USAGE](../../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)|  
|[KEY_COLUMN_USAGE](../../relational-databases/system-information-schema-views/key-column-usage-transact-sql.md)|[VIEW_TABLE_USAGE](../../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)|  
|[PARAMETERS](../../relational-databases/system-information-schema-views/parameters-transact-sql.md)|[VIEWS](../../relational-databases/system-information-schema-views/views-transact-sql.md)|  
  
 Além disso, algumas exibições contêm referências a classes diferentes de dados como dados de caractere ou dados binários.  
  
 Ao fazer referência às exibições de esquema de informações, você deve usar um nome qualificado que inclui o nome do esquema `INFORMATION_SCHEMA`. Por exemplo:  
  
```  
SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = N'Product';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
