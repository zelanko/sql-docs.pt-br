---
description: Exibições do esquema de informações do sistema (Transact-SQL)
title: Exibições do esquema de informações do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- information schema views
- schemas [SQL Server], information schema views
- metadata [SQL Server], views
- views [SQL Server], information schema
- system views [SQL Server], information schema
ms.assetid: 7e9f1dfe-27e9-40e7-8fc7-bfc5cae6be10
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8c283777fea2999d7948a3282b623cd92f0baf54
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907375"
---
# <a name="system-information-schema-views-transact-sql"></a>Exibições do esquema de informações do sistema (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Uma exibição de esquema de informações é um dos vários métodos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecidos para obtenção de metadados. As exibições de esquema de informações fornecem uma exibição interna independente da tabela do sistema dos metadados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Exibições de esquema de informações permitem que os aplicativos trabalhem corretamente embora alterações significativas tenham sido feitas nas tabelas do sistema subjacentes. As exibições de esquema de informações incluídas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão em conformidade com a definição padrão ISO para o INFORMATION_SCHEMA.

> [!IMPORTANT]
> Algumas alterações feitas nas exibições do esquema de informações quebram a compatibilidade com versões anteriores. Essas alterações são descritas nos tópicos das exibições específicas.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a uma convenção de nomenclatura de três partes quando você faz uma referência ao servidor atual. O padrão ISO também oferece suporte a uma convenção de nomenclatura de três partes. Entretanto, os nomes usados em ambas as convenções de nomenclatura são diferentes. As exibições de esquema de informações são definidas em um esquema especial chamado INFORMATION_SCHEMA. Esse esquema está contido em cada banco de dados. Cada exibição de esquema de informações contém metadados para todos os objetos de dados armazenados naquele banco de dados específico. A tabela a seguir mostra as relações entre os nomes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os nomes SQL padrão.

|Nome do SQL Server|Mapeia para seu nome SQL padrão equivalente|
|---------------------|-----------------------------------------------|
|Banco de dados|Catálogo|
|Esquema|Esquema|
|Objeto|Objeto|
|tipo de dados definido pelo usuário|Domínio|

Esta convenção de mapeamento de nome se aplica às seguintes exibições compatíveis com ISO [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

:::row:::
    :::column:::
        [CHECK_CONSTRAINTS](../../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)

        [COLUMN_DOMAIN_USAGE](../../relational-databases/system-information-schema-views/column-domain-usage-transact-sql.md)

        [COLUMN_PRIVILEGES](../../relational-databases/system-information-schema-views/column-privileges-transact-sql.md)

        [COLUMNS](../../relational-databases/system-information-schema-views/columns-transact-sql.md)

        [CONSTRAINT_COLUMN_USAGE](../../relational-databases/system-information-schema-views/constraint-column-usage-transact-sql.md)

        [CONSTRAINT_TABLE_USAGE](../../relational-databases/system-information-schema-views/constraint-table-usage-transact-sql.md)

        [DOMAIN_CONSTRAINTS](../../relational-databases/system-information-schema-views/domain-constraints-transact-sql.md)

        [DOMÍNIOS](../../relational-databases/system-information-schema-views/domains-transact-sql.md)

        [KEY_COLUMN_USAGE](../../relational-databases/system-information-schema-views/key-column-usage-transact-sql.md)

        [PARAMETERS](../../relational-databases/system-information-schema-views/parameters-transact-sql.md)
    :::column-end:::
    :::column:::
        [REFERENTIAL_CONSTRAINTS](../../relational-databases/system-information-schema-views/referential-constraints-transact-sql.md)

        [ROUTINES](../../relational-databases/system-information-schema-views/routines-transact-sql.md)

        [ROUTINE_COLUMNS](../../relational-databases/system-information-schema-views/routine-columns-transact-sql.md)

        [SCHEMATA](../../relational-databases/system-information-schema-views/schemata-transact-sql.md)

        [TABLE_CONSTRAINTS](../../relational-databases/system-information-schema-views/table-constraints-transact-sql.md)

        [TABLE_PRIVILEGES](../../relational-databases/system-information-schema-views/table-privileges-transact-sql.md)

        [TABLES](../../relational-databases/system-information-schema-views/tables-transact-sql.md)

        [VIEW_COLUMN_USAGE](../../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)

        [VIEW_TABLE_USAGE](../../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)

        [VIEWS](../../relational-databases/system-information-schema-views/views-transact-sql.md)
    :::column-end:::
:::row-end:::

Além disso, algumas exibições contêm referências a classes diferentes de dados como dados de caractere ou dados binários.

Ao fazer referência às exibições de esquema de informações, você deve usar um nome qualificado que inclui o nome do esquema `INFORMATION_SCHEMA`. Por exemplo:

```sql
SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME = N'Product';
```

## <a name="permissions"></a>Permissões  
A visibilidade dos metadados nas exibições do esquema de informações é limitada aos protegíveis que um usuário possui ou aos quais o usuário recebeu alguma permissão. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).

> [!NOTE]  
> As exibições do esquema de informações são definidas para todo o servidor e, portanto, não podem ser negadas no contexto de um banco de dados de usuário. Para REVOGAr ou negar acesso (SELECT), o banco de dados mestre deve ser usado. Por padrão, a função pública tem a permissão SELECT-Permission para todas as exibições de esquema de informações, mas o conteúdo é limitado com regras de visibilidade de metadados.

## <a name="see-also"></a>Consulte Também

- [Exibições do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-views/replication-views-transact-sql.md)
- [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
- [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) 
