---
title: "Pesquisar um relat&#243;rio com acesso &#224; URL | Microsoft Docs"
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
  - "pesquisando relatórios"
  - "pesquisas de texto [Reporting Services]"
  - "Acesso à URL [Reporting Services], pesquisas de relatório"
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
caps.latest.revision: 34
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 34
---
# Pesquisar um relat&#243;rio com acesso &#224; URL
  Você pode pesquisar um relatório para obter um conjunto específico de texto usando o acesso de URL. Para pesquisar um relatório, defina o valor do parâmetro *rc:FindString* na URL igual ao texto para o qual você deseja pesquisar. Além disso, use os parâmetros *rc:StartFind* e *rc:EndFind* para estreitar sua pesquisa a páginas específicas dentro do relatório.  
  
## Exemplo  
 Este exemplo de acesso de URL procura a primeira ocorrência do texto "Mountain-400" no relatório de exemplo Catálogo de Produtos começando pela primeira página e terminando na página cinco:  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## Consulte também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  