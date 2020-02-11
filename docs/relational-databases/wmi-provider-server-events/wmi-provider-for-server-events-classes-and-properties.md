---
title: Provedor WMI para classes e propriedades de eventos de servidor
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 08b18a3a5805b37a371d6fa17850584d6f4953fd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74164915"
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>Provedor WMI para classes e propriedades de eventos de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Os eventos de servidor a seguir constituem o modelo de programação do Provedor WMI para eventos do servidor. Há duas categorias principais de eventos que podem ser consultadas pela emissão de consultas de WQL no provedor. São os eventos DDL (linguagem de definição de dados) e eventos de rastreamento. Os eventos QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED do agente de serviço também podem ser consultados. Observe a natureza inclusiva dos diagramas de árvore a seguir. Por exemplo, o evento DDL_ASSEMBLY_EVENTS inclui qualquer evento ALTER_ASSEMBLY, CREATE_ASSEMBLY e DROP_ASSEMBLY. Da mesma forma, o evento TRC_FULL_TEXT inclui qualquer evento FT_CRAWL_ABORTED, FT_CRAWL_STARTED e FT_CRAWL_STOPPED. ALL_EVENTS cobre todos os eventos de DDL, eventos de rastreamento, QUEUE_ACTIVATION e BROKER_QUEUE_DISABLED.  
  
 Para saber quais propriedades podem ser examinadas de um evento ou grupo de eventos, consulte o esquema de evento. Por padrão, o esquema do evento é instalado no seguinte diretório: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events .xsd.  
  
 Como alternativa, você pode consultar o esquema de evento publicado em [https://schemas.microsoft.com/sqlserver](https://go.microsoft.com/fwlink/?linkid=43100).  
  
 Por exemplo, fazendo referência ao evento ALTER_DATABASE, você aprenderá que seu evento pai é DDL_SERVER_LEVEL_EVENTS e suas propriedades são **TSQLCommand** e **DatabaseName**. O evento também herda as propriedades **SQLInstance**, **TimeTime**, **ComputerName**, **SPID**e **LoginName**. O evento não tem nenhum evento filho.  
  
> [!NOTE]  
>  Os procedimentos armazenados do sistema que executam operações similares a DDL também podem acionar notificações de eventos. Teste as notificações de eventos para determinar suas respostas aos procedimentos armazenados que são executados. Por exemplo, a instrução CREATE TYPE e **sp_addtype** procedimento armazenado acionarão uma notificação de evento que é criada em um evento CREATE_TYPE. Para obter mais informações, consulte [eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
 **Eventos de linguagem de definição de dados e grupos de eventos**  
  
 ![Provedor WMI de Árvore de Eventos de Servidor.](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "Provedor WMI de Árvore de Eventos de Servidor.")  
  
 **Eventos de rastreamento e grupos de eventos**  
  
 ![Eventos de rastreamento e grupos de evento](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "Eventos de rastreamento e grupos de evento")  
  
## <a name="see-also"></a>Consulte Também  
 [Provedor WMI para conceitos de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [Usando o WQL com o Provedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
