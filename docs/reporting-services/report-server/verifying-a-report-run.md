---
title: "Verificando uma execu&#231;&#227;o de relat&#243;rio | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "auditoria[Reporting Services]"
  - "verificando execução de relatório"
  - "logs [Reporting Services], verificando a execução de relatório"
  - "dados da execução de relatório [Reporting Services]"
  - "informações de status [Reporting Services]"
  - "processamento do relatório [Reporting Services], verificando a execução"
  - "verificando execução de relatório "
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
caps.latest.revision: 37
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 37
---
# Verificando uma execu&#231;&#227;o de relat&#243;rio
  Para visualizar informações sobre o status de processamento do relatório, você pode usar os arquivos de log ou consultar as informações sobre status exibidas com o relatório no Gerenciador de Relatórios.  
  
## Fontes de dados de execução de relatórios  
 Os logs de execução de relatório fornecem informações abrangentes sobre a execução do relatório, incluindo o nome dele, o nome do usuário que o executou, o horário da execução do relatório e a extensão de entrega usada para distribuí-lo. Para visualizar e analisar esses dados, você pode copiar o log de execução do relatório nas tabelas do banco de dados que são fáceis de consultar e relatar.  
  
 Os arquivos de log contêm muitas entradas sobre a execução de relatório e outra atividade de servidor. Uma vez que os arquivos de log contêm tantos dados, talvez você queira usar o Gerenciador de Relatórios apenas se quiser verificar quando foi a última execução do relatório. Se quiser informações adicionais, exiba os arquivos de log.  
  
> [!NOTE]  
>  O Gerenciador de Relatórios não mostra os horários de processamento dos relatórios executados sob demanda.  
  
 A tabela a seguir descreve como exibir a data e hora do processamento para vários tipos de relatórios.  
  
|Para este tipo de relatório|As informações sobre data e hora estão localizadas aqui|Para exibir as informações, faça o seguinte|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|Um relatório que é executado como um instantâneo de relatório.|Na página Conteúdo. Para obter mais informações, consulte [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md).|1) Localize a pasta que contém o relatório.<br /><br /> 2) Defina a pasta na exibição Detalhes.<br /><br /> 3) Observe a data e hora na coluna **Quando Executado**.|  
|Um instantâneo no histórico de relatórios.|Na página Propriedades do Histórico. Para obter mais informações, consulte [Página de propriedades Opções de Instantâneo &#40;Gerenciador de Relatórios&#41;](../Topic/Snapshot%20Options%20Properties%20Page%20\(Report%20Manager\).md).|1) Abra o relatório.<br /><br /> 2) Clique na página **Propriedades**.<br /><br /> 3) Clique na guia **Histórico**.<br /><br /> 4) Observe a data e hora na coluna **Quando Executado**.|  
|Um relatório armazenado em cache.|Na agenda usada para criar e atualizar o relatório armazenado em cache.|1) Abra o relatório.<br /><br /> 2) Clique na página **Propriedades**.<br /><br /> 3) Clique na guia **Execução**.<br /><br /> 4) Abra a agenda.|  
  
## Consulte também  
 [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  