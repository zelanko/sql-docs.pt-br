---
title: Tarefa Leitor de Dados do WMI | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fa94e484ea82f0ca5421ada5a6e8779e02dfd461
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438023"
---
# <a name="wmi-data-reader-task"></a>Tarefa Leitor de Dados do WMI
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
  
 Se a origem ou o destino for um arquivo, a tarefa Leitor de Dados do WMI usará um gerenciador de conexões de Arquivo para se conectar ao arquivo. Para obter mais informações, consulte [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 A tarefa Leitor de Dados do WMI usa um gerenciador de conexões WMI para se conectar ao servidor do qual lê informações de WMI. Para obter mais informações, consulte [WMI Connection Manager](../connection-manager/wmi-connection-manager.md).  
  
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
 A tabela a seguir relaciona as entradas de log personalizadas para a tarefa Leitor de Dados do WMI. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../custom-messages-for-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|Indica que a tarefa começou a ser ler os dados do WMI.|  
|`WMIDataReaderOperation`|Informa a consulta WQL executada pela tarefa.|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>Configuração da tarefa Leitor de Dados do WMI  
 Você pode definir propriedades programaticamente ou por meio do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos tópicos a seguir:  
  
-   [Editor da Tarefa Leitor de Dados do WMI &#40;Página Opções do WMI&#41;](../wmi-data-reader-task-editor-wmi-options-page.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou de um contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas de Integration Services](integration-services-tasks.md)   
 [Fluxo de controle](control-flow.md)  
  
  
