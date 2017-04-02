---
title: "Limitar o hist&#243;rico de relat&#243;rio (Gerenciador de Relat&#243;rios) | Microsoft Docs"
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
  - "exibindo histórico de relatórios"
  - "histórico de relatório [Reporting Services], exibindo o histórico"
  - "histórico de relatórios [Reporting Services], configurando o histórico"
  - "dados do histórico [Reporting Services]"
  - "exibindo histórico de relatório"
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
caps.latest.revision: 36
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 36
---
# Limitar o hist&#243;rico de relat&#243;rio (Gerenciador de Relat&#243;rios)
  O histórico de relatórios é uma coleção de instantâneos de relatórios que você cria. Você pode criar um histórico de relatórios sob demanda ou agendar com que frequência um instantâneo é criado e adicionado ao histórico de relatórios.  
  
 O histórico de relatórios é armazenado no banco de dados do servidor de relatórios. Se os instantâneos de relatório contiverem uma grande quantidade de dados, limite o histórico de relatórios para minimizar o efeito da retenção de instantâneos no tamanho do banco de dados.  
  
### Para configurar o histórico de relatórios para um servidor de relatório  
  
1.  No Gerenciador de Relatórios, clique em **Configurações de Site** na barra de ferramentas global.  
  
2.  Selecione **Manter um número ilimitado de instantâneos no histórico de relatório** se desejar manter todo o histórico de relatórios indefinidamente. Caso contrário, selecione **Limitar as cópias do histórico de relatório** para especificar o número máximo de instantâneos que podem ser mantidos em um relatório específico.  
  
3.  Clique em **Aplicar**.  
  
### Para configurar o histórico de relatórios para um relatório específico  
  
1.  No Gerenciador de Relatórios, navegue até o relatório para o qual deseja configurar o histórico e, em seguida, clique no relatório para abri-lo.  
  
2.  Clique na guia **Propriedades** .  
  
3.  Clique na guia **Histórico**.  
  
4.  Selecione as opções para seu relatório e clique em **Aplicar**. Para obter detalhes sobre cada opção, consulte [Página de propriedades Opções de Instantâneo &#40;Gerenciador de Relatórios&#41;](../Topic/Snapshot%20Options%20Properties%20Page%20\(Report%20Manager\).md).  
  
## Consulte também  
 [Adicionar um instantâneo ao histórico de relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)  
  
  