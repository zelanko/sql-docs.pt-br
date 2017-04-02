---
title: "Formato de arquivo de sa&#237;da XML (ssbdiagnose) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Formato de arquivo de saída XML [ssbdiagnose]"
  - "ssbdiagnose"
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Formato de arquivo de sa&#237;da XML (ssbdiagnose)
  O utilitário **ssbdiagnose** entrega sua saída como um arquivo XML quando você o executa com a opção **-XML**. O arquivo de saída XML lista informações de cabeçalho e erros encontrados na configuração ou conversa do [!INCLUDE[ssSB](../../includes/sssb-md.md)] analisadas. Você pode escrever um aplicativo para analisar ou reportar os erros listados no arquivo. Ou pode exibir o arquivo de XML em um editor de XML geral, como o Bloco de Notas XML.  
  
 Um arquivo de saída do **ssbdiangose** contém um elemento raiz DiagnosticInformation com dois tipos de filho:  
  
-   Um elemento Banner com informações de cabeçalho.  
  
-   Um elemento Issue para cada problema reportado por **ssbdiagnose**.  
  
## Elemento raiz DiagnosticInformation  
  
-   [Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)  
  
## Elemento Banner  
  
-   [Elemento Banner &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)  
  
## Elemento Issue  
  
-   [Elemento Issue &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)  
  
## Consulte também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  