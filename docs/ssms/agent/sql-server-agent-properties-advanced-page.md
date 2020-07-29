---
title: Propriedades do SQL Server Agent (página Avançado)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e92520ae859c128e07abb40336a45f1a306da34e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755169"
---
# <a name="sql-server-agent-properties-advanced-page"></a>Propriedades do SQL Server Agent (página Avançado)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página para ver e modificar propriedades avançadas de serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Encaminhamento de evento do SQL Server**  
As opções nesta categoria ativam e configuram o encaminhamento de evento.  
  
**Encaminhar eventos para um servidor diferente**  
Encaminha eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para um servidor diferente.  
  
**Servidor**  
Selecionar o nome do servidor ao qual os eventos serão encaminhados.  
  
**Eventos sem-tratamento**  
Encaminha apenas os eventos sem-tratamento para o servidor especificado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent só encaminha os eventos aos quais não haja respostas de nenhum alerta.  
  
**Todos os eventos**  
Encaminha todos os eventos. Quando um alerta na instância local responde ao evento, o agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encaminhará o evento e processará o alerta.  
  
**Se a gravidade do evento for esta ou acima**  
Encaminha apenas os eventos com nível de severidade igual ou maior que o nível especificado.  
  
**Condição de CPU ociosa**  
As opções nesta categoria definem as condições sobre as quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa trabalhos agendados para serem executados na agenda da CPU ociosa.  
  
**Definir condição de CPU ociosa**  
Define as condições sob as quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent considera que a CPU está ociosa.  
  
**Uso médio de CPU cai abaixo de**  
Porcentagem de uso de CPU abaixo do qual a CPU é considerada ociosa.  
  
**E permanece abaixo desse nível por**  
Quantidade de tempo em que o uso médio da CPU deve estar abaixo do nível especificado antes que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent execute trabalhos na agenda de CPU ociosa.  
  
## <a name="see-also"></a>Consulte Também  
[Criar e anexar agendas para trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Gerenciar eventos](../../ssms/agent/manage-events.md)  
  
