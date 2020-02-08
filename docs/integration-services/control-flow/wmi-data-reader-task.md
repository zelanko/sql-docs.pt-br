---
title: Tarefa Leitor de Dados do WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmidatareadertask.f1
- sql13.dts.designer.wmidatareadertask.general.f1
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e0c1b30985bf93ff1b04af85e45bf64e53c75853
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71293725"
---
# <a name="wmi-data-reader-task"></a>Tarefa Leitor de Dados do WMI

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa Leitor de Dados do WMI executa consultas por meio da linguagem de consulta WMI (Instrumentação de Gerenciamento do Windows) que retorna informações de WMI sobre um sistema de computador. Pode-se utilizar o Leitor de Dados WMI para as seguintes finalidades:  
  
-   Consultar os logs de eventos do Windows em um computador local ou remoto e gravar as informações em um arquivo ou variável.  
  
-   Obter informações sobre a presença, o estado ou as propriedades de componentes de hardware e, depois, usar essas informações para determinar se outras tarefas no fluxo de controle devem ser executadas.  
  
-   Obter uma lista de aplicativos e determinar qual versão de cada aplicativo está instalada.  
  
 Você pode configurar a tarefa Leitura de Dados do WMI das seguintes formas:  
  
-   Especifique o gerenciador de conexões WMI a ser usado.  
  
-   Especifique a fonte da consulta WQL. A consulta pode ser armazenada em uma propriedade de tarefa, ou pode ser armazenada fora da tarefa, em uma variável ou um arquivo.  
  
-   Defina o formato dos resultados da consulta WQL. A tarefa oferece suporte a uma tabela, par de nome/valor de propriedade ou formato de valor de propriedade.  
  
-   Espefique o destino da consulta. O destino pode ser um variável ou um arquivo.  
  
-   Indique se o destino de consulta é substituído, mantido ou acrescentado.  
  
 Se a origem ou o destino for um arquivo, a tarefa Leitor de Dados do WMI usará um gerenciador de conexões de Arquivo para se conectar ao arquivo. Para obter mais informações, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 A tarefa Leitor de Dados do WMI usa um gerenciador de conexões WMI para se conectar ao servidor do qual lê informações de WMI. Para obter mais informações, consulte [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
## <a name="wql-query"></a>Consulta WQL  
 WQL é um dialeto do SQL com extensões para dar suporte à notificação de eventos de WMI e outros recursos específicos ao WMI. Para obter mais informações sobre WQL, consulte a documentação da Instrumentação de Gerenciamento do Windows na [Biblioteca do MSDN](https://go.microsoft.com/fwlink/?linkid=7022).  
  
> [!NOTE]  
>  As classes WMI variam entre versões de Windows.  
  
 A consulta WQL a seguir retorna entradas no evento de logs do aplicativo.  
  
```  
SELECT * FROM Win32_NTLogEvent WHERE LogFile = 'Application' AND (SourceName='SQLISService' OR SourceName='SQLISPackage') AND TimeGenerated > '20050117'  
```  
  
 A consulta WQL a seguir retorna informações lógicas de disco.  
  
```  
SELECT FreeSpace, DeviceId, Size, SystemName, Description FROM Win32_LlogicalDisk  
```  
  
 A consulta WQL a seguir retorna uma lista das atualizações QFE (Quick Fix Engineering) ao sistema operacional.  
  
```  
Select * FROM Win32_QuickFixEngineering  
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-data-reader-task"></a>Mensagens de log personalizadas disponíveis na tarefa Leitor de Dados do WMI  
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Leitor de Dados do WMI. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|Indica que a tarefa começou a ser ler os dados do WMI.|  
|**WMIDataReaderOperation**|Informa a consulta WQL executada pela tarefa.|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>Configuração da tarefa Leitor de Dados do WMI  
 Você pode definir propriedades programaticamente ou por meio do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="wmi-data-reader-task-editor-general-page"></a>Editor da Tarefa Leitor de Dados do WMI (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Leitor de Dados WMI** para nomear e descrever a tarefa Leitor de Dados WMI.  
  
  Para obter mais informações sobre a linguagem WQL, consulte o tópico Instrumentação de Gerenciamento do Windows, [Querying with WQL](/windows/win32/wmisdk/querying-with-wql)(Consultando com WQL), na Biblioteca MSDN.  
  
### <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Leitor de Dados WMI. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Leitor de Dados WMI.  
  
## <a name="wmi-data-reader-task-editor-wmi-options-page"></a>Editor da Tarefa Leitor de Dados do WMI (página Opções do WMI)
  Use a página **Opções do WMI** da caixa de diálogo **Editor da Tarefa Leitor de Dados do WMI** para especificar a origem da consulta da linguagem WQL e o destino do resultado da consulta.  
  
 Para obter mais informações sobre a linguagem WQL, consulte o tópico Instrumentação de Gerenciamento do Windows, [Querying with WQL](/windows/win32/wmisdk/querying-with-wql)(Consultando com WQL), na Biblioteca MSDN.  
  
### <a name="static-options"></a>Opções estáticas  
 **WMIConnectionName**  
 Selecione um gerenciador de conexões WMI na lista ou clique em \<**Nova Conexão WMI...** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor do Gerenciador de Conexões WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Selecione o tipo de origem da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a origem de consultas WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém a consulta WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
|**Variável**|Defina a origem de uma variável que defina a consulta WQL. Ao selecionar esse valor, a opção dinâmica **WQLQuerySourceType**será exibida.|  
  
 **OutputType**  
 Especifique se a saída deve ser uma tabela de dados, valor de propriedade ou nome e valor de propriedade.  
  
 **OverwriteDestination**  
 Especifique se é necessário manter, substituir ou adicionar aos dados originais no arquivo ou variável de destino.  
  
 **DestinationType**  
 Selecione o tipo de destino da consulta WQL que a tarefa executa. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão do Arquivo**|Selecione um arquivo no qual salvar os resultados da consulta WQL. A seleção desse valor exibe a opção dinâmica **DestinationType**.|  
|**Variável**|Defina a variável na qual armazenar os resultados da consulta WQL. A seleção desse valor exibe a opção dinâmica **DestinationType**.|  
  
### <a name="wqlquerysourcetype-dynamic-options"></a>Opções dinâmicas de WQLQuerySourceType  
  
#### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = Entrada direta  
 **WQLQuerySource**  
 Forneça uma consulta ou clique nas reticências (...) e digite uma consulta, usando a caixa de diálogo **Consulta WQL**.  
  
#### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = Conexão do arquivo  
 **WQLQuerySource**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor do Gerenciador de conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = Variável  
 **WQLQuerySource**  
 Selecione uma variável na lista ou clique em \<**Nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="destinationtype-dynamic-options"></a>Opções dinâmicas de DestinationType  
  
#### <a name="destinationtype--file-connection"></a>DestinationType = Conexão do arquivo  
 **Destino**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor do Gerenciador de conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="destinationtype--variable"></a>DestinationType = Variável  
 **Destino**  
 Selecione uma variável na lista ou clique em \<**Nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
