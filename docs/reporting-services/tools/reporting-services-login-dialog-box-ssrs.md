---
title: "Caixa de di&#225;logo Logon do Reporting Services (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "sql13.rtp.rptdesigner.reportservicelogin.f1"
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
caps.latest.revision: 31
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 31
---
# Caixa de di&#225;logo Logon do Reporting Services (SSRS)
  Use a caixa de diálogo **Logon do Reporting Services** para fornecer credenciais para publicar relatórios no servidor de relatório.  
  
-   **Observação** Se esta for a primeira vez que você publica um relatório no servidor de relatório desde que você definiu a propriedade de implantação **TargetServerURL** para um projeto, verifique se o nome do servidor especificado é semelhante a **server** e não a **reports**. Por exemplo, `http://localhost/reportserver`e não a `http://localhost/reports`. Especificar o diretório `reports` no servidor local em vez do diretório `reportserver` indiretamente faz com que essa caixa de diálogo seja aberta. Para obter mais informações sobre a configuração de **TargetServerURL**, consulte [Definir as propriedades da implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
## Opções  
 **Servidor**  
 Exibe o nome do servidor de relatório. Por exemplo, `http://localhost/reportserver`. Para servidores de relatório que usam uma porta diferente da porta 80 padrão, inclua o número da porta. Por exemplo, `http://localhost:81/reportserver`.  
  
 **Nome de usuário**  
 Digite o nome de usuário para fazer logon no serviço Web.  
  
 **Senha**  
 Digite a senha para fazer logon no serviço Web.  
  
## Consulte também  
 [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Ajuda F1 do Designer de Relatórios](../../reporting-services/tools/report-designer-f1-help.md)  
  
  