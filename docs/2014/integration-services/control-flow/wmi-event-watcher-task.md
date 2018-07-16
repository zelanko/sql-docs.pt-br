---
title: Tarefa Detector de Eventos do WMI | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmieventwatchertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6f4fa442175db0b00033e4c616f7572a3ad26da6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169228"
---
# <a name="wmi-event-watcher-task"></a>Tarefa Detector de Eventos do WMI
  A tarefa Detector de Eventos do WMI detecta um evento de Instrumentação de Gerenciamento do Windows (WMI) por meio de uma consulta de evento WQL (Management Instrumentation Query Language, Linguagem de Consulta de Instrumentação de Gerenciamento) para especificar eventos de interesse. É possível utilizar a tarefa Detector de Eventos do WMI para as seguintes finalidades:  
  
-   Aguardar notificação de que foram adicionados arquivos a uma pasta e depois iniciar o processamento do arquivo.  
  
-   Executar um pacote que exclui arquivos quando a memória disponível em um servidor elimina o que for inferior a um percentual especificado.  
  
-   Detectar a instalação de um aplicativo e então executar um pacote que usa o aplicativo.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui uma tarefa que lê informações WMI.  
  
 Para obter mais informações sobre essa tarefa, clique no tópico a seguir:  
  
-   [Tarefa Leitor de Dados do WMI](wmi-data-reader-task.md)  
  
## <a name="wql-queries"></a>Consultas WQL  
 WQL é um dialeto do SQL com extensões para dar suporte à notificação de eventos de WMI e outros recursos específicos ao WMI. Para obter mais informações sobre WQL, consulte a documentação da Instrumentação de Gerenciamento do Windows na [Biblioteca do MSDN](http://go.microsoft.com/fwlink/?linkid=62553).  
  
> [!NOTE]  
>  As classes WMI variam entre versões de Windows.  
  
 A consulta seguinte detecta notificação de que o uso da CPU é superior a 40 por cento.  
  
```  
SELECT * from __InstanceModificationEvent WITHIN 2 WHERE TargetInstance ISA 'Win32_Processor' and TargetInstance.LoadPercentage > 40  
```  
  
 A consulta seguinte detecta notificação de que um arquivo foi adicionado a uma pasta.  
  
```  
SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "CIM_DirectoryContainsFile" and TargetInstance.GroupComponent= "Win32_Directory.Name=\"c:\\\\WMIFileWatcher\""   
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-event-watcher-task"></a>Mensagens de registro personalizadas disponíveis na tarefa Detector de Eventos do WMI  
 A tabela a seguir relaciona as entradas de registro personalizadas da tarefa Detector de Eventos do WMI. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../custom-messages-for-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|Indica que ocorreu um evento que a tarefa estava monitorando.|  
|`WMIEventWatcherTimedout`|Indica que o tempo limite da tarefa foi esgotado.|  
|`WMIEventWatcherWatchingForWMIEvents`|Indica que a tarefa começou a executar a consulta WQL. A entrada inclui a consulta.|  
  
## <a name="configuration-of-the-wmi-event-watcher-task"></a>Configuração da tarefa Detector de Eventos do WMI  
 Você pode configurar a tarefa Leitura de Dados do WMI das seguintes formas:  
  
-   Especifique o gerenciador de conexões WMI a ser usado.  
  
-   Especifique a fonte da consulta WQL. A fonte pode ser armazenada fora da tarefa, em uma variável ou um arquivo, ou a consulta pode ser armazenada em uma propriedade de tarefa.  
  
-   Especificar a ação que a tarefa adotará quando o evento WMI ocorrer. Você pode registrar a notificação de eventos e o status após o evento ou levantar eventos personalizados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que fornecem informações associadas ao evento WMI, à notificação e ao status após o evento.  
  
-   Definir como a tarefa responde ao evento. A tarefa pode ser configurada para ter êxito ou falhar, dependendo do evento, ou a tarefa pode apenas detectar o evento novamente.  
  
-   Especificar a ação que a tarefa adotará quando a consulta WMI expirar. Você pode registrar a expiração e o status após a expiração ou levantar um evento personalizado do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , indicando que o evento WMI expirou e registrando a expiração e o status da expiração.  
  
-   Definir como a tarefa responde à expiração. A tarefa pode ser configurada para ter êxito ou falhar, ou a tarefa pode apenas detectar o evento novamente.  
  
-   Especificar o número de vezes que a tarefa detecta o evento.  
  
-   Especificar o limite de tempo.  
  
 Se a origem for um arquivo, a tarefa Detector de Eventos do WMI usará um gerenciador de conexões de Arquivo para se conectar ao arquivo. Para obter mais informações, consulte [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 A tarefa Detector de Eventos do WMI usa um gerenciador de conexões WMI para se conectar ao servidor do qual lê informações de WMI. Para obter mais informações, consulte [WMI Connection Manager](../connection-manager/wmi-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor de tarefa do detector de eventos do WMI &#40;página geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de tarefa do detector de eventos do WMI &#40;página de opções do WMI&#41;](../wmi-event-watcher-task-editor-wmi-options-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>Configuração programática da tarefa Detector de Eventos do WMI  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
  
