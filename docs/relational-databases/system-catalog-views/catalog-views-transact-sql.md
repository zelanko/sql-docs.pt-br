---
title: "(Transact-SQL) de exibições do catálogo | Microsoft Docs"
ms.custom: 
ms.date: 05/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: sql13.SysViewExpandPortal.f1
dev_langs: TSQL
helpviewer_keywords:
- catalog metadata [SQL Server]
- system views [SQL Server], catalog
- metadata [SQL Server], views
- catalogs [SQL Server], metadata
- catalog views [SQL Server]
- Database Engine [SQL Server], metadata
- catalog views [SQL Server], about catalog views
ms.assetid: 13bccc2f-ed3c-4b58-abd0-ca8bf34a66b8
caps.latest.revision: "45"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 40d26c8b87daec4f7cea3b1ac5e6a3390d50b193
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="system-catalog-views-transact-sql"></a>Exibições de catálogo do sistema (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  As exibições do catálogo retornam informações usadas pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Recomendamos usar exibições do catálogo por serem a interface mais geral para metadados de catálogo e proporcionarem a maneira mais eficaz de obter, transformar e apresentar formas personalizadas dessas informações. Todos os metadados de catálogos disponíveis para o usuário são expostos por meio de exibições do catálogo.  
  
> [!NOTE]  
>  As exibições do catálogo não contêm informações sobre replicação, backup, plano de manutenção de banco de dados ou dados de catálogo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 Algumas exibições do catálogo herdam linhas de outras. Por exemplo, o [sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) herda de exibição do catálogo a [sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) exibição do catálogo. A exibição do catálogo sys.objects é conhecida como exibição básica, e a exibição sys.tables é chamada de derivada. A exibição do catálogo sys.tables retorna as colunas específicas de tabelas e também todas as colunas retornadas pela exibição do catálogo sys.objects. A exibição do catálogo sys.objects retorna linhas de objetos que não sejam de tabelas, como procedimentos armazenados e exibições. Depois que uma tabela é criada, o metadados da tabela são retornados em ambas as exibições. Embora as duas exibições do catálogo retornem níveis diferentes de informações sobre a tabela, há apenas uma entrada nos metadados para essa tabela com um nome e um object_id. Isso pode ser resumido como segue:  
  
-   A exibição básica contém um subconjunto de colunas e um superconjunto de linhas.  
  
-   A exibição derivada contém um superconjunto de colunas e um subconjunto de linhas.  
  
> [!IMPORTANT]  
>  Em versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[msCoName](../../includes/msconame-md.md)] poderá aumentar a definição de qualquer exibição do catálogo de sistema adicionando colunas ao final da lista de colunas. Não é recomendável o uso da sintaxe SELECT \* FROM *sys.catalog_view_name* em produção código porque o número de colunas retornado pode alterar e quebrar seu aplicativo.  
  
 As exibições do catálogo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foram organizadas nas categorias seguintes:  
  
|||  
|-|-|  
|[Sempre em exibições do catálogo de grupos de disponibilidade &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[Mensagens &#40; para erros &#41; Exibições de catálogo &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)|  
|[Exibições do catálogo de banco de dados SQL do Azure](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|  
|[Alterar modos de exibição de catálogo de rastreamento &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)|[Exibições do catálogo de função de partição &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|  
|[Exibições do catálogo Assembly CLR &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|  
|[Exibições do coletor de dados &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[Exibições de catálogo do administrador de recursos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|  
|[Espaços de dados &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|  
|[Exibições do Database Mail &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[Escalar tipos de exibições de catálogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|  
|[Modos de exibição de catálogo de testemunha de espelhamento &#40; do banco de dados Transact-SQL &#41;](http://msdn.microsoft.com/library/8a0c9053-5d76-4aa9-a18d-0ea1c514034d)|[Exibições do catálogo de esquemas &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)|  
|[Bancos de dados e exibições do catálogo de arquivos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|  
|[Exibições do catálogo de pontos de extremidade &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Exibições de catálogo do Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|  
|[Exibições de catálogo de eventos estendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[Exibições de catálogo de configuração do servidor &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|  
|[Exibições de catálogo de propriedades estendidas &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/f39fd324-efd4-4468-884c-bf77ed1a026f)|[Exibições do catálogo de dados espaciais](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|  
|[Exibições do catálogo operações externas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[SQL Data Warehouse e exibições de catálogo do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|  
|[FileStream e exibições do catálogo FileTable &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[Exibições de catálogo de ampliação do banco de dados &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/bee78e39-e07d-4b0f-b8ad-09a01a5eb795)|  
|[Pesquisa de texto completo e exibições do catálogo de pesquisa semântica &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[Esquemas XML &#40; Sistema de tipo XML &#41; Exibições de catálogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|  
|[Exibições de catálogo de servidores vinculados &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do esquema de informações &#40; Transact-SQL &#41;](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Tabelas do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
