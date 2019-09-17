---
title: Propriedades do alerta – Novo alerta (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.general.f1
ms.assetid: f5c11610-62e3-44df-9800-a5dc35be4a09
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4634821adee5021b986b3f9c87c0416bad33ec6a
ms.sourcegitcommit: 949e55b32eff6610087819a93160a35af0c5f1c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70383804"
---
# <a name="alert-properties---new-alert-general-page"></a>Propriedades do alerta – Novo alerta (página Geral)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página para exibir e modificar as propriedades gerais dos alertas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  

## <a name="options"></a>Opções  
**Nome**  
Altere o nome do alerta.  
  
**Habilitar**  
Habilite o alerta. Quando o alerta não está habilitado, as ações especificadas no alerta não acontecem.  
  
**Tipo**  
Selecione o tipo de alerta:  
  
-   O**Alerta de evento do SQL Server** responde às mensagens no log de eventos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows.  
  
-   O**Alerta de condição de desempenho do SQL Server** responde a uma condição específica em um contador de desempenho.  
  
-   O**Alerta de evento do WMI** responde a um evento WMI (Instrumentação de Gerenciamento do Windows).  
  
## <a name="sql-server-event-alert-options"></a>Opções de alerta de evento do SQL Server  
**Nome do banco de dados**  
Especifica um banco de dados para o evento ou **todos os bancos de dados** para responder a uma mensagem independentemente do banco de dados no qual o evento ocorrer.  
  
**Número do erro**  
Especifique que este evento responda a um erro e o número do erro.  
  
**Severity**  
Especifique que este evento responda a qualquer mensagem com um nível de severidade específico e o nível de severidade.  
  
**Gerar alertas quando a mensagem contiver**  
Filtre os eventos por uma cadeia de caracteres específica. Quando esta opção é selecionada, o alerta só responde a eventos que contenham uma cadeia de caracteres específica.  
  
**Texto da mensagem**  
Especifique a cadeia de caracteres usada para filtrar eventos.  
  
## <a name="sql-server-performance-condition-alerts"></a>Alertas de condição de desempenho do SQL Server  
**Objeto**  
Especifique o objeto de desempenho a ser monitorado.  
  
**Contador**  
Especifique o contador dentro do objeto de desempenho a ser monitorado.  
  
**Instância**  
Especifique a instância do contador a ser monitorado.  
  
**Alertar se o contador**  
Especifique o comportamento do contador ao qual o alerta responde. Por exemplo, o alerta pode responder a uma condição em que o valor do contador de **Espaço livre em tempdb (KB)** cai abaixo de um determinado valor ou responder a uma condição em que as **Compilações de SQL/s** subam acima de um determinado valor.  
  
**Value**  
Especifique um valor para o contador.  
  
## <a name="wmi-event-alert-options"></a>Opções de alerta de evento WMI  
**Namespace**  
Especifique o namespace a ser usado para a instrução WQL (WMI Query Language). Só têm suporte os namespaces em computadores que executam o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Consulta**  
Especifique a instrução WQL que identifica o evento ao qual o alerta responde.  
  
## <a name="see-also"></a>Consulte Também  
[Alertas](../../ssms/agent/alerts.md)  
[Usando o WQL com o Provedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
[Criar um alerta usando um número de erro](../../ssms/agent/create-an-alert-using-an-error-number.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
