---
title: Monitorar e responder a eventos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- notifications [SQL Server], alert
- events [SQL Server], alerts
- alerts [SQL Server]
- notifications [SQL Server]
- events [SQL Server], automatically responding to
- administrator notifications [SQL Server Agent]
- automatic event responses
- SQL Server Agent alerts
- monitoring [SQL Server], events
- responding to events automatically
ms.assetid: f7fbe155-5b68-4777-bc71-a47637471f32
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9a159a48202f1c49e1ffccc5444eea1f21265f2d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="monitor-and-respond-to-events"></a>Monitorar e responder a eventos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent pode monitorar e responder automaticamente a *eventos*, como mensagens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], condições de desempenho específicas e eventos WMI (Instrumentação de Gerenciamento do Windows).  
  
## <a name="in-this-section"></a>Nesta seção  
[Alertas](../../ssms/agent/alerts.md)  
Contém informações sobre como nomear um alerta e selecionar os eventos ou as condições de desempenho às quais os alertas respondem.  
  
[Criar um evento definido pelo usuário](../../ssms/agent/create-a-user-defined-event.md)  
Contém informações sobre como criar eventos diferentes daqueles predefinidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
[Operadores](../../ssms/agent/operators.md)  
Contém informações sobre como criar aliases para administradores que podem ser utilizados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para enviar notificações sobre a falha ou o êxito de trabalhos.  
  
## <a name="about-monitoring-and-responding-to-events"></a>Sobre monitoramento e resposta a eventos  
As respostas automatizadas a eventos são chamadas de *alertas*. Você pode definir um alerta em um ou mais eventos, para especificar como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve responder mediante sua ocorrência. Um alerta pode responder a um evento notificando um administrador ou executando um trabalho, ou ambos. Um alerta também pode encaminhar um evento para o log de aplicativos do Microsoft Windows em um computador diferente. Por exemplo, é possível especificar que um operador seja notificado imediatamente caso ocorra um evento de severidade 19. Definindo alertas, os administradores de banco de dados podem monitorar e gerenciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]com mais eficácia.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent só responde a eventos para os quais está definido um alerta. O método utilizado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para monitorar eventos depende do tipo de evento.  
  
Quando um alerta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é definido para um contador de desempenho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent monitora diretamente esse contador de desempenho. No caso de um evento WMI, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent registra uma consulta de evento para o evento WMI.  
  
Para responder a mensagens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent monitora o log de aplicativos do Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent só pode responder a mensagens que aparecem nesse log. Por padrão, o SQL Server registra as seguintes mensagens no log de aplicativos do Windows:  
  
-   Erros de sysmessages com severidade 19 ou superior.  
  
    Caso deseje registrar também erros de sysmessages específicos de severidade menor que 19, use o procedimento armazenado sp_altermessage para designar tais erros como "always logged" (registrar sempre).  
  
-   Qualquer instrução RAISERROR é invocada usando a sintaxe WITH LOG.  
  
    Usar RAISERROR WITH LOG é a maneira recomendada de fazer registros no log de aplicativos do Windows a partir de uma instância do SQL Server.  
  
-   Qualquer evento de aplicativo que é registrado usando xp_logevent.  
  
    > [!NOTE]  
    > Registrar eventos de aplicativos consome espaço de log e pode fazer com que o log de aplicativos do Windows exceda seu tamanho máximo. Verifique que o tamanho máximo do log de aplicativos do Windows seja grande o suficiente para impedir perda de informações de eventos do SQL Server.  
  
Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] registra uma mensagem, o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent compara a mensagem com os alertas definidos pelo administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
Independentemente da origem do evento, o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent responde ao evento executando as tarefas especificadas no alerta correspondente.  
  
## <a name="see-also"></a>Consulte Também  
[sp_altermessage](http://msdn.microsoft.com/en-us/1b28f280-8ef9-48e9-bd99-ec14d79abaca)  
  
