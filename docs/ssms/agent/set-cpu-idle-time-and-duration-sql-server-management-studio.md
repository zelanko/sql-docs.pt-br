---
title: Definir o momento e a duração de ociosidade da CPU (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CPU [SQL Server], idle conditions
- time [SQL Server], CPU idle and duration
- duration of CPU idle [SQL Server]
- SQL Server Agent, CPU idle conditions
- idle time [SQL Server]
ms.assetid: 8647b465-d899-4cc7-9640-134a506d0a2e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c8cbc7954b67fd9adaf3859ed9fc5027b0f65ff3
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42775920"
---
# <a name="set-cpu-idle-time-and-duration-sql-server-management-studio"></a>Definir o momento e a duração de ociosidade da CPU (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico explica como definir a condição de ociosidade de CPU para seu servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. A definição de ociosidade de CPU influencia o modo de resposta do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a eventos. Por exemplo, suponhamos que você defina a condição de ociosidade de CPU como o uso médio de CPU abaixo de 10 por cento, com permanência de 10 minutos nesse nível. Assim, se você tiver definido trabalhos para execução sempre que a CPU do servidor estiver em condição de ociosidade, o trabalho será iniciado quando o uso de CPU cair abaixo de 10 por cento e permanecer por 10 minutos nesse nível. Caso se trate de um trabalho com impacto significativo sobre o desempenho do servidor, é muito importante a definição da condição de ociosidade de CPU.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-set-cpu-idle-time-and-duration"></a>Para definir o momento e a duração da ociosidade de CPU  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, clique em **Propriedades**e selecione a página **Avançado** .  
  
3.  Em **Condição de CPU ociosa**, siga um destes procedimentos:  
  
    -   Marque **Definir condição de CPU ociosa**.  
  
    -   Especifique um percentual na caixa **O uso médio de CPU cai abaixo de** (em todas as CPUs). Isso define o nível de uso abaixo do qual a CPU deve cair para ser considerada ociosa.  
  
    -   Especifique um número de segundos na caixa **E permanece abaixo desse nível por** . Isto define a duração da permanência sob o uso mínimo de CPU para que ela seja considerada ociosa.  
  
