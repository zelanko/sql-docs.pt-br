---
title: Provedor WMI para eventos de servidor Classes e propriedades | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4145bfb3dac5043556d18fb794504effd12eeb4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>Provedor WMI para classes e propriedades de eventos de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Os eventos de servidor a seguir constituem o modelo de programação do Provedor WMI para eventos do servidor. Há duas categorias principais de eventos que podem ser consultadas pela emissão de consultas de WQL no provedor. São os eventos DDL (linguagem de definição de dados) e eventos de rastreamento. Os eventos QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED do agente de serviço também podem ser consultados. Observe a natureza inclusiva dos diagramas de árvore a seguir. Por exemplo, o evento DDL_ASSEMBLY_EVENTS inclui qualquer evento ALTER_ASSEMBLY, CREATE_ASSEMBLY e DROP_ASSEMBLY. Da mesma forma, o evento TRC_FULL_TEXT inclui qualquer evento FT_CRAWL_ABORTED, FT_CRAWL_STARTED e FT_CRAWL_STOPPED. ALL_EVENTS cobre todos os eventos de DDL, eventos de rastreamento, QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED.  
  
 Para saber quais propriedades podem ser examinadas de um evento ou grupo de eventos, consulte o esquema de evento. Por padrão, o esquema do evento é instalado no seguinte diretório: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events .xsd.  
  
 Como alternativa, você pode consultar o esquema do evento publicado em [ http://schemas.microsoft.com/sqlserver ](http://go.microsoft.com/fwlink/?linkid=43100).  
  
 Por exemplo, referindo-se ao evento ALTER_DATABASE, você vai aprender que seu evento pai é DDL_SERVER_LEVEL_EVENTS e suas propriedades são **TSQLCommand** e **DatabaseName**. O evento também herda as propriedades **SQLInstance**, **PostTime**, **ComputerName**, **SPID**, e **LoginName** . O evento não tem nenhum evento filho.  
  
> [!NOTE]  
>  Os procedimentos armazenados do sistema que executam operações similares a DDL também podem acionar notificações de eventos. Teste as notificações de eventos para determinar suas respostas aos procedimentos armazenados que são executados. Por exemplo, a instrução CREATE TYPE e **sp_addtype** procedimento armazenado dispararão uma notificação de evento que é criada em um evento CREATE_TYPE. Para obter mais informações, consulte[eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
 **Eventos de linguagem de definição de dados e grupos de eventos**  
  
 ![Provedor WMI de árvore de servidor eventos](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "provedor WMI para a árvore de eventos de eventos do servidor")  
  
 **Eventos de rastreamento e grupos de eventos**  
  
 ![Grupos de eventos e eventos de rastreamento](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "grupos de eventos e eventos de rastreamento")  
  
## <a name="see-also"></a>Consulte também  
 [Provedor WMI para conceitos de eventos do servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [Usando o WQL com o Provedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
