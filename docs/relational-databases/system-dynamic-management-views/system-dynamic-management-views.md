---
title: Exibições de gerenciamento dinâmico (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], about dynamic management objects
- server state information [SQL Server]
- dynamic management functions [SQL Server]
- metadata [SQL Server], dynamic management objects
- dynamic management views [SQL Server]
- DMVs [SQL Server]
- functions [SQL Server], dynamic management
- server scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server]
ms.assetid: cf893ecb-0bf6-4cbf-ac00-8a1099e405b1
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ab6b2c35bb3507dbf7debc4b2e0d5f3a27df937
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043134"
---
# <a name="system-dynamic-management-views"></a>Exibições de gerenciamento dinâmico do sistema
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  As exibições e funções de gerenciamento dinâmico retornam informações do estado do servidor que podem ser usadas para monitorar a saúde da instância do servidor, diagnosticar problemas e ajustar o desempenho.  
  
> [!IMPORTANT]  
>  Elas retornam dados de estado internos específicos de implementação. Os esquemas e os dados retornados podem mudar em versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por isso, as exibições e funções de gerenciamento dinâmico, em versões futuras, podem não ser compatíveis com as exibições e funções de gerenciamento dinâmico nessa versão. Por exemplo, em versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a Microsoft poderá aumentar a definição de qualquer exibição do gerenciamento dinâmico adicionando colunas ao final da lista de colunas. Não é recomendável o uso da sintaxe `SELECT * FROM dynamic_management_view_name` no código de produção, pois o número de colunas retornado pode mudar e quebrar seu aplicativo.  
  
 Há dois tipos de exibições e funções de gerenciamento dinâmico:  
  
-   Exibições e funções de gerenciamento dinâmico de escopo de servidor. Requerem a permissão VIEW SERVER STATE no servidor.  
  
-   Exibições e funções de gerenciamento dinâmico de escopo de banco de dados. Requerem permissão VIEW DATABASE STATE no banco de dados.  
  
## <a name="querying-dynamic-management-views"></a>Consultando exibições de gerenciamento dinâmico  
 As exibições de gerenciamento dinâmico podem ser mencionadas em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] usando nomes de duas, três ou quatro partes. Por sua vez, as funções de gerenciamento dinâmico podem ser mencionadas em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] usando nomes de duas ou três partes. As exibições e funções de gerenciamento dinâmico não podem ser referenciadas em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] usando nomes de uma parte.  
  
 Todas as exibições e funções de gerenciamento dinâmico estão no esquema sys e seguem a convenção de nomenclatura dm_*. Quando você usa uma exibição ou função de gerenciamento dinâmico, é preciso prefixar o nome da exibição ou função usando o esquema sys. Por exemplo, para consultar a exibição de gerenciamento dinâmico dm_os_wait_stats, execute a seguinte consulta:  
  
 ```sql
SELECT wait_type, wait_time_ms  
FROM sys.dm_os_wait_stats;  
```  
  
### <a name="required-permissions"></a>Permissões necessárias  
 A consulta de uma exibição ou função de gerenciamento dinâmico requer a permissão SELECT no objeto e a permissão VIEW SERVER STATE ou VIEW DATABASE STATE. Isso permite restringir seletivamente o acesso de um usuário ou logon a exibições e funções de gerenciamento dinâmico. Para fazer isso, primeiro crie o usuário em mestre e negue a permissão SELECT aos usuários nas exibições e funções de gerenciamento dinâmico a que os usuários não devem ter acesso. Depois disso, o usuário não poderá selecionar essas exibições ou funções de gerenciamento dinâmico, independentemente do contexto de banco de dados do usuário.  
  
> [!NOTE]  
>  Como DENY prevalece, se um usuário tiver recebido permissões VIEW SERVER STATE, mas não a permissão VIEW DATABASE STATE, ele poderá verificar as informações de servidor, mas não as de banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
 As exibições e as funções de gerenciamento dinâmico foram organizadas nas seguintes categorias.  
  
|||  
|-|-|  
|[Grupos de disponibilidade Always On, exibições de gerenciamento dinâmico e funções (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)|[Exibições de gerenciamento dinâmico de tabela otimizada em memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)|  
|[Exibições de gerenciamento dinâmico relacionadas à captura de dados de alterações &#40;Transact-SQL&#41;](change-data-capture-sys-dm-cdc-errors.md)|[Funções e exibições de gerenciamento dinâmico relacionadas ao objeto &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Controle de alterações relacionadas a exibições de gerenciamento dinâmico](change-tracking-sys-dm-tran-commit-table.md)|[Exibições de gerenciamento dinâmico relacionadas às notificações de consulta &#40;Transact-SQL&#41;](query-notifications-sys-dm-qn-subscriptions.md)|  
|[Common Language Runtime relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)|[Exibições de gerenciamento dinâmico relacionadas à replicação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)|  
|[Exibições de gerenciamento dinâmico relacionadas ao espelhamento de banco de dados &#40;Transact-SQL&#41;](database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)|[Administrador de recursos relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)|  
|[Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)|[Funções e exibições de gerenciamento dinâmico relacionadas à segurança &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)|[Exibições e funções de gerenciamento dinâmico relacionadas ao servidor &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Exibições de gerenciamento dinâmico de eventos estendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)|[Exibições de gerenciamento dinâmico relacionadas ao Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)|  
|[FileStream e exibições de gerenciamento dinâmico de FileTable &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)|[Exibições de gerenciamento dinâmico e funções relacionam a dados espaciais &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/c542ac38-451f-43a5-bf8c-4edd38bb738e)|  
|[Pesquisa de texto completo e funções e exibições de gerenciamento dinâmico de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)|[SQL Data Warehouse e Parallel Data Warehouse exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)|  
|[Funções e exibições de gerenciamento dinâmico de replicação geográfica &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)|[Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)|  
|[Índice de funções e exibições de gerenciamento dinâmico relacionadas ao &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)|[Stretch Database exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/1193efce-a105-49a9-a8b8-26b063485567)|  
|[Eu O relacionadas a funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)|[Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)|  

  
## <a name="see-also"></a>Consulte também  
 [Permissões GRANT do servidor &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)   
 [Permissões GRANT de banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)   
 [Exibições do sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
