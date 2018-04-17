---
title: Usar objetos de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73a727c385ce24f9d1490de52e1e563510d3dfa5
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2018
---
# <a name="use-performance-objects"></a>Usar objetos de desempenho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent contém objetos de desempenho e contadores para monitorar o desempenho do serviço. Esses objetos de desempenho permitem-lhe usar o Monitor de Desempenho — uma ferramenta do Windows — para identificar o que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent está fazendo em segundo plano. Por exemplo, é possível identificar quantos trabalhos ativos o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent executa atualmente, para determinar quais deles estão bloqueados.  
  
Existem objetos de desempenho e contadores do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instalada em um computador. Os objetos de desempenho são nomeados de acordo com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que representam.  
  
A tabela a seguir mostra como os objetos de desempenho do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent são nomeados:  
  
|Tipo de instância|Nome do objeto|  
|-----------------|---------------|  
|Padrão|**SQLAgent:***object*:*counter*|  
|Nomeado|**SQLAgent$**<br /> **&#42;instance_name&#42; :***object*:*counter*|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] contém os objetos de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent a seguir.  
  
|Nome do objeto|Description|  
|---------------|---------------|  
|[SQLAgent:Jobs](http://msdn.microsoft.com/en-us/225b5e2d-4a78-4178-b2b6-b419df83c4aa)|Informações sobre o desempenho de trabalhos que foram iniciados, taxas de êxito e status atual|  
|[SQLAgent:JobSteps](http://msdn.microsoft.com/en-us/44f9983c-1753-4fe0-8475-973aa2460b3a)|Informações sobre o status de etapas de trabalho|  
|[SQLAgent:Alerts](http://msdn.microsoft.com/en-us/e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a)|Informações sobre o número de alertas e notificações|  
|[SQLAgent:Statistics](http://msdn.microsoft.com/en-us/ebe92bfa-0721-48aa-9ba6-e7904ad265a1)|Informações gerais do desempenho|  
  
## <a name="see-also"></a>Consulte também  
[Monitorar e ajustar o desempenho](http://msdn.microsoft.com/en-us/87f23f03-0f19-4b2e-bfae-efa378f7a0d4)  
[Como iniciar o Monitor do Sistema (Windows)](http://msdn.microsoft.com/en-us/5e51bb79-5737-470b-9c47-fac330c001c5)  
  
