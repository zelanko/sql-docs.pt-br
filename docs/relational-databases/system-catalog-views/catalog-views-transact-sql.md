---
title: Exibições de catálogo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql13.SysViewExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- catalog metadata [SQL Server]
- system views [SQL Server], catalog
- metadata [SQL Server], views
- catalogs [SQL Server], metadata
- catalog views [SQL Server]
- Database Engine [SQL Server], metadata
- catalog views [SQL Server], about catalog views
ms.assetid: 13bccc2f-ed3c-4b58-abd0-ca8bf34a66b8
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9532ee19ec8489caa51d090feaff464e030a0da0
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670552"
---
# <a name="system-catalog-views-transact-sql"></a>Exibições do catálogo do sistema (Transact-SQL)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

As exibições do catálogo retornam informações usadas pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Recomendamos usar exibições do catálogo por serem a interface mais geral para metadados de catálogo e proporcionarem a maneira mais eficaz de obter, transformar e apresentar formas personalizadas dessas informações. Todos os metadados de catálogos disponíveis para o usuário são expostos por meio de exibições do catálogo.

> [!NOTE]
> As exibições do catálogo não contêm informações sobre replicação, backup, plano de manutenção de banco de dados ou dados de catálogo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.

 Algumas exibições do catálogo herdam linhas de outras. Por exemplo, a exibição do catálogo [Sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) herda da exibição do catálogo [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) . A exibição do catálogo sys.objects é conhecida como exibição básica, e a exibição sys.tables é chamada de derivada. A exibição do catálogo sys.tables retorna as colunas específicas de tabelas e também todas as colunas retornadas pela exibição do catálogo sys.objects. A exibição do catálogo sys.objects retorna linhas de objetos que não sejam de tabelas, como procedimentos armazenados e exibições. Depois que uma tabela é criada, o metadados da tabela são retornados em ambas as exibições. Embora as duas exibições do catálogo retornem níveis diferentes de informações sobre a tabela, há apenas uma entrada nos metadados para essa tabela com um nome e um object_id. Isso pode ser resumido como segue:

- A exibição básica contém um subconjunto de colunas e um superconjunto de linhas.
- A exibição derivada contém um superconjunto de colunas e um subconjunto de linhas.

> [!IMPORTANT]
> Em versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[msCoName](../../includes/msconame-md.md)] poderá aumentar a definição de qualquer exibição do catálogo de sistema adicionando colunas ao final da lista de colunas. É recomendável usar a sintaxe SELECT \* de *Sys. catalog_view_name* no código de produção porque o número de colunas retornado pode mudar e interromper seu aplicativo.

As exibições do catálogo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foram organizadas nas categorias seguintes:

|||
|-|-|
|[Exibições &#40;de catálogo de grupos de disponibilidade Always on TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[Mensagens &#40;para erros&#41; exibições &#40;de catálogo Transact&#41;-SQL](../system-catalog-views/messages-for-errors-catalog-views-sys-messages.md))|
|[Exibições do catálogo do banco de dados SQL do Azure](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[Exibições &#40;do catálogo de objetos TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|
|[Exibições &#40;de catálogo controle de alterações TRANSACT-SQL&#41;](../system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)|[Exibições &#40;de catálogo de funções de partição TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|
|[Exibições &#40;do catálogo do assembly CLR TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|
|[Exibições &#40;do coletor de dados TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[Exibições &#40;de catálogo resource governor TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|
|[Espaços &#40;de dados TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|
|[Database Mail exibições &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[Visualizações &#40;de catálogo de tipos escalares TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|
|[Exibições &#40;do catálogo de testemunha de espelhamento de banco de dados TRANSACT-SQL&#41;](../system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)|[Exibições &#40;de catálogo de esquemas TRANSACT-SQL&#41;](../system-catalog-views/schemas-catalog-views-sys-schemas.md)|
|[Exibições &#40;de catálogo de bancos de dados e arquivos TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|
|[Exibições &#40;de catálogo de pontos de extremidade TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Exibições de catálogo do Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|
|[Exibições de catálogo de eventos estendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[Exibições &#40;do catálogo de configuração de todo o servidor TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|
|[Exibições de catálogo de propriedades estendidas &#40;Transact-SQL&#41;](../system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)|[Exibições do catálogo de dados espaciais](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|
|[Exibições &#40;de catálogo de operações externas TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[Exibições do catálogo de data warehouse SQL Data Warehouse e paralelas](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|
|[Exibições &#40;de catálogo FileStream e filetable TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[Exibições &#40;de catálogo Stretch Database TRANSACT-SQL&#41;](../system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md)|
|[Pesquisa de texto completo e exibições &#40;de catálogo de pesquisa semântica TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[Tipo &#40;XML de esquemas XML exibições&#41; &#40;do catálogo do sistema Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|
|[Exibições &#40;de catálogo de servidores vinculados TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||

## <a name="see-also"></a>Consulte também

- [Exibições &#40;do esquema de informações TRANSACT-SQL&#41;](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
- [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)
