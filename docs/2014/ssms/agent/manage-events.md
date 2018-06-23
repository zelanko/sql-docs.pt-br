---
title: Gerenciar Eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- event-triggered jobs [SQL Server]
- forwarding events [SQL Server]
- alerts [SQL Server], forwarded events
- alerts [SQL Server], management servers
- SQL Server Agent alerts, management servers
ms.assetid: 8f4ee7f5-80df-49fd-b2b8-d020e04b6e1b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 67dd730cfa06cff637e1ae58d89b18fc8b13bef5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117570"
---
# <a name="manage-events"></a>Gerenciar eventos
  É possível encaminhar a um instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todas as mensagens de evento que atendam ou excedam um nível de severidade de erro específico. A isso chamamos *encaminhamento de evento*. O servidor de encaminhamento é um servidor dedicado que também pode ser um servidor mestre. Você pode usar o encaminhamento de eventos para centralizar o gerenciamento de alertas para um grupo de servidores, reduzindo, assim, a carga de trabalho em servidores de intensa utilização.  
  
 Quando um servidor recebe eventos para um grupo de outros servidores, esse servidor é chamado de *servidor de gerenciamento de alertas*. Em um ambiente multisservidor, o servidor mestre é designado como servidor de gerenciamento de alertas.  
  
## <a name="advantages-of-using-an-alerts-management-server"></a>Vantagens de usar um servidor de gerenciamento de alertas  
 São vantagens de se configurar um servidor de gerenciamento de alertas:  
  
-   **Centralização**. Controle centralizado e exibição consolidada dos eventos de várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são possíveis a partir de um único servidor.  
  
-   **Escalabilidade**. Vários servidores físicos podem ser administrados como um mesmo servidor lógico. É possível adicionar ou remover servidores desse grupo de servidores físicos, conforme a necessidade.  
  
-   **Eficiência**. O tempo de configuração é reduzido, porque alertas e operadores precisam ser definidos apenas uma vez.  
  
## <a name="disadvantages-of-using-an-alerts-management-server"></a>Desvantagens de usar um servidor de gerenciamento de alertas  
 São desvantagens de se configurar um servidor de gerenciamento de alertas:  
  
-   **Aumento do tráfego**. Encaminhar eventos a um servidor de gerenciamento de alertas pode aumentar o tráfego da rede. Esse aumento pode ser moderado pela restrição do encaminhamento a eventos que estejam acima de um nível de severidade designado.  
  
-   **Ponto de falha único**. Se o servidor de gerenciamento de alertas ficar offline, nenhum alerta será emitido para qualquer evento no grupo gerenciado de servidores.  
  
-   **Carga de servidor**. A manipulação de alertas para os eventos encaminhados provocam um aumento na carga de processamento no servidor de gerenciamento de alertas.  
  
## <a name="guidelines-for-using-an-alerts-management-server"></a>Diretrizes para usar um servidor de gerenciamento de alertas  
 Ao configurar um servidor de gerenciamento de alertas, siga estas diretrizes:  
  
-   Para receber eventos encaminhados, o servidor de gerenciamento de alertas deve ser uma instância padrão do SQL Server.  
  
-   Evite executar aplicativos críticos ou intensamente utilizados no servidor de gerenciamento de alertas.  
  
-   Planeje cuidadosamente o tráfego de rede envolvido na configuração de muitos servidores compartilhando o mesmo servidor de gerenciamento de alertas. Se houver congestionamento, reduza o número de servidores que usam o servidor de gerenciamento de alertas em questão.  
  
     Os servidores registrados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] constituem a lista de servidores disponíveis para eleição como servidor de encaminhamento de alerta.  
  
-   Defina alertas na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que requeira uma resposta específica a servidor, em vez de encaminhar os alertas ao servidor de gerenciamento de alertas.  
  
     O servidor de gerenciamento de alertas exibe todos os servidores do quais recebe encaminhamentos como um todo lógico. Por exemplo, um servidor de gerenciamento de alertas responde do mesmo modo a um evento 605 tanto de um servidor A, quanto de um servidor B.  
  
-   Configurado o seu sistema de alertas, verifique periodicamente o log de aplicativos do Microsoft Windows quanto a eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
     As condições de falha encontradas pelo mecanismo de alerta são gravadas no log de aplicativos do Windows local, com nome de origem "SQL Server Agent." Por exemplo, se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não puder enviar uma notificação por email, conforme está definido, será registrado um evento no log de aplicativos.  
  
 Se um alerta definido localmente estiver inativo e ocorrer um evento que o dispararia, este será encaminhado ao servidor de gerenciamento de alertas (caso satisfaça a condição de encaminhamento de alerta). Esse encaminhamento permite a desativação e a ativação de substituições locais (alertas definidos localmente que também estão definidos no servidor de gerenciamento de alertas), conforme a necessidade, pelo usuário no site local. Você também pode solicitar que os eventos sempre sejam encaminhados, mesmo quando eles também são manipulados por alertas locais.  
  
 A seguir, encontram-se tarefas comuns do gerenciamento de eventos em um ambiente multisservidor:  
  
 **Para designar um servidor de gerenciamento de alertas**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
 **Para definir uma resposta a um alerta**  
  
-   [SQL Server Management Studio](define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
## <a name="running-event-triggered-jobs"></a>Executando trabalhos acionados por eventos  
 Você pode definir que um trabalho seja executado em resposta a um alerta. Por exemplo, é possível executar um trabalho que corrija ou aprofunde o diagnóstico de um problema detectado pelo alerta.  
  
> [!NOTE]  
>  Uma vez que um trabalho pode emitir um evento, tenha cuidado para não criar um loop recursivo alerta-trabalho.  
  
## <a name="see-also"></a>Consulte também  
 [sys. sysmessages &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysmessages-transact-sql)  
  
  
