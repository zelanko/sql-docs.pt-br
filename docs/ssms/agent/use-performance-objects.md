---
title: Usar objetos de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73e36b4d0ee10d42ec7774e20693d217ee274344
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260905"
---
# <a name="use-performance-objects"></a>Usar objetos de desempenho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent contém objetos de desempenho e contadores para monitorar o desempenho do serviço. Esses objetos de desempenho permitem-lhe usar o Monitor de Desempenho — uma ferramenta do Windows — para identificar o que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está fazendo em segundo plano. Por exemplo, é possível identificar quantos trabalhos ativos o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa atualmente, para determinar quais deles estão bloqueados.  
  
Existem objetos de desempenho e contadores do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada em um computador. Os objetos de desempenho são nomeados de acordo com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que representam.  
  
A tabela a seguir mostra como os objetos de desempenho do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent são nomeados:  
  
|Tipo de instância|Nome do objeto|  
|-----------------|---------------|  
|Padrão|**SQLAgent:** _objeto_:_contador_|  
|Nomeado|**SQLAgent$**<br /> **&#42;nome_da_instância&#42; :** _objeto_:_contador_|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém os objetos de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a seguir.  
  
|Nome do objeto|Descrição|  
|---------------|---------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|Informações sobre o desempenho de trabalhos que foram iniciados, taxas de êxito e status atual|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|Informações sobre o status de etapas de trabalho|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|Informações sobre o número de alertas e notificações|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|Informações gerais do desempenho|  
  
## <a name="see-also"></a>Consulte Também  
[Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
[Como: Iniciar o Monitor do Sistema (Windows)](https://msdn.microsoft.com/5e51bb79-5737-470b-9c47-fac330c001c5)  
  
