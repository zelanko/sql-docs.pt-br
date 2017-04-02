---
title: "Propriedades do Servidor (p&#225;gina Log) | Microsoft Docs"
ms.custom: ""
ms.date: "06/10/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.reportserver.serverproperties.logging.f1"
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
caps.latest.revision: 17
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 17
---
# Propriedades do Servidor (p&#225;gina Log)
  Use essa página [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] no [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] para definir limites nos dados de execução de relatório que são coletados por um servidor de relatório. Dados de execução são armazenados internamente no banco de dados do servidor de relatório. Você pode controlar atividade de relatório para servidor de relatório que executa em modo nativo ou em modo integrado de SharePoint. Se o servidor de relatório for parte de uma implantação em expansão, o log de execução do relatório manterá um registro de todas as atividades do relatório para toda a implantação, em um único arquivo de log.  
  
 Para abrir esta página:
 1) Iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) Conecte-se a um servidor de relatório.
 3) Clique com o botão direito do mouse no nome do servidor de relatório e selecione **Propriedades**. 
 4) Clique em **Log** para abrir esta página.  
  
## Opções  
 **Habilitar log de execução de relatório**  
 Clique para criar e armazenar informações sobre atividade de relatório no servidor. Se essa opção estiver habilitada, o servidor de relatório controlará quais relatórios serão usados, a frequência de processamento do relatório, o tipo de operação executado, o formato de saída e quem executou o relatório. Para obter mais informações sobre pontos de dados adicionais capturados no log, consulte [ExecutionLog do servidor de relatório e exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 **Remova entradas de log mais antigas que este número de dias**  
 Especifique o número de dias depois dos quais as entradas de log serão apagadas do log de execução de relatório. O valor padrão é 60 dias.  
  
## Consulte também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio ](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [ExecutionLog do servidor de relatório e exibição do ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  