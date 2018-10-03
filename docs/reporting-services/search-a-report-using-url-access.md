---
title: Pesquisar um relatório usando o acesso à URL | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b5714f7d224410ce5eac704e11a9ef2dc3e49a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47759414"
---
# <a name="search-a-report-using-url-access"></a>Pesquisar um relatório com acesso à URL
  Você pode pesquisar um relatório para obter um conjunto específico de texto usando o acesso de URL. Para pesquisar um relatório, defina o valor do parâmetro *rc:FindString* na URL igual ao texto para o qual você deseja pesquisar. Além disso, use os parâmetros *rc:StartFind* e *rc:EndFind* para estreitar sua pesquisa a páginas específicas dentro do relatório.  
  
## <a name="example"></a>Exemplo  
 Este exemplo de acesso de URL procura a primeira ocorrência do texto "Mountain-400" no relatório de exemplo Catálogo de Produtos começando pela primeira página e terminando na página cinco:  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  
