---
title: Tarefa Detector de Eventos do WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmieventwatchertask.f1
- sql13.dts.designer.wmieventwatcher.general.f1
- sql13.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d31b2d7515eaebc7d0c2e5fb5861d8b6b51ad6f7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293713"
---
# <a name="wmi-event-watcher-task"></a>Tarefa Detector de Eventos do WMI

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa Detector de Eventos do WMI detecta um evento de Instrumentação de Gerenciamento do Windows (WMI) por meio de uma consulta de evento WQL (Management Instrumentation Query Language, Linguagem de Consulta de Instrumentação de Gerenciamento) para especificar eventos de interesse. É possível utilizar a tarefa Detector de Eventos do WMI para as seguintes finalidades:  
  
-   Aguardar notificação de que foram adicionados arquivos a uma pasta e depois iniciar o processamento do arquivo.  
  
-   Executar um pacote que exclui arquivos quando a memória disponível em um servidor elimina o que for inferior a um percentual especificado.  
  
-   Detectar a instalação de um aplicativo e então executar um pacote que usa o aplicativo.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui uma tarefa que lê informações WMI.  
  
 Para obter mais informações sobre essa tarefa, clique no tópico a seguir:  
  
-   [Tarefa Leitor de Dados do WMI](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
## <a name="wql-queries"></a>Consultas WQL  
 WQL é um dialeto do SQL com extensões para dar suporte à notificação de eventos de WMI e outros recursos específicos ao WMI. Para obter mais informações sobre WQL, consulte a documentação da Instrumentação de Gerenciamento do Windows na [Biblioteca do MSDN](https://go.microsoft.com/fwlink/?linkid=62553).  
  
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
 A tabela a seguir relaciona as entradas de registro personalizadas da tarefa Detector de Eventos do WMI. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|Indica que ocorreu um evento que a tarefa estava monitorando.|  
|**WMIEventWatcherTimedout**|Indica que o tempo limite da tarefa foi esgotado.|  
|**WMIEventWatcherWatchingForWMIEvents**|Indica que a tarefa começou a executar a consulta WQL. A entrada inclui a consulta.|  
  
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
  
 Se a origem for um arquivo, a tarefa Detector de Eventos do WMI usará um gerenciador de conexões de Arquivo para se conectar ao arquivo. Para obter mais informações, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 A tarefa Detector de Eventos do WMI usa um gerenciador de conexões WMI para se conectar ao servidor do qual lê informações de WMI. Para obter mais informações, consulte [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>Configuração programática da tarefa Detector de Eventos do WMI  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
## <a name="wmi-event-watcher-task-editor-general-page"></a>Editor da Tarefa Detector de Eventos do WMI (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Detector de Eventos do WMI** para nomear e descrever a tarefa Detector de Eventos do WMI.  
  
 Para obter mais informações sobre a linguagem WQL, consulte o tópico Instrumentação de Gerenciamento do Windows, [Querying with WQL](/windows/win32/wmisdk/querying-with-wql)(Consultando com WQL), na Biblioteca MSDN.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Detector de Eventos do WMI. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Detector de Eventos do WMI.  
  
## <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>Editor do Detector de Eventos do WMI (página Opções do WMI)
  Use a página **Opções do WMI** da caixa de diálogo **Editor do Detector de Eventos do WMI** para especificar a origem da consulta WQL (Instrumentação de Gerenciamento do Windows Query Language) e como a tarefa do Detector de Eventos do WMI responde aos eventos do WMI (Microsoft Windows Instrumentation).  
  
 Para obter mais informações sobre a linguagem WQL, consulte o tópico Instrumentação de Gerenciamento do Windows, [Querying with WQL](/windows/win32/wmisdk/querying-with-wql)(Consultando com WQL), na Biblioteca MSDN.  
  
### <a name="static-options"></a>Opções estáticas  
 **WMIConnectionName**  
 Selecione um gerenciador de conexões WMI na lista ou clique em \<**Nova Conexão WMI...** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor do Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Selecione o tipo de origem da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de consultas WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém a consulta WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
|**Variável**|Define a origem de uma variável que define a consulta WQL. Selecionar este valor faz com que seja exibida a opção dinâmica **WQLQuerySource**.|  
  
 **ActionAtEvent**  
 Especifique se o evento WMI efetua logon do evento e inicia uma ação do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou só efetua logon do evento.  
  
 **AfterEvent**  
 Especifique se a tarefa é bem-sucedida ou falha depois que recebe o evento WMI ou se a tarefa continua observando se o evento ocorre novamente.  
  
 **ActionAtTimeout**  
 Especifique se a tarefa registra o tempo limite excedido da consulta WMI e inicia um evento [!INCLUDE[ssIS](../../includes/ssis-md.md)] em resposta ou só registra o tempo limite excedido.  
  
 **AfterTimeout**  
 Especifique se a tarefa é bem-sucedida ou falha em resposta ao tempo limite excedido ou se a tarefa continua observando se o tempo limite é excedido novamente.  
  
 **NumberOfEvents**  
 Especifique o número de eventos a serem observados.  
  
 **Tempo Limite**  
 Especifique o número de segundos a esperar para que o evento ocorra. Um valor de 0 significa que nenhum tempo limite está em efeito.  
  
### <a name="wqlquerysource-dynamic-options"></a>Opções dinâmicas do WQLQuerySource  
  
#### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = Entrada direta  
 **WQLQuerySource**  
 Forneça uma consulta ou clique no botão de reticências (...) e digite uma consulta usando a caixa de diálogo **Consulta WQL**.  
  
#### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = Conexão do arquivo  
 **WQLQuerySource**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor do Gerenciador de conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysource--variable"></a>WQLQuerySource = Variável  
 **WQLQuerySource**  
 Selecione uma variável na lista ou clique em \<**Nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
