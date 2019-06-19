---
title: Pesquisar um relatório usando o acesso à URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b45f3fabf58a0980d41ee7b4b89a771655477d02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102229"
---
# <a name="search-a-report-using-url-access"></a>Pesquisar um relatório com acesso à URL
  Você pode pesquisar um relatório para obter um conjunto específico de texto usando o acesso de URL. Para pesquisar um relatório, defina o valor do parâmetro *rc:FindString* na URL igual ao texto para o qual você deseja pesquisar. Além disso, use os parâmetros *rc:StartFind* e *rc:EndFind* para estreitar sua pesquisa a páginas específicas dentro do relatório.  
  
## <a name="example"></a>Exemplo  
 Este exemplo de acesso de URL procura a primeira ocorrência do texto "Mountain-400" no relatório de exemplo Catálogo de Produtos começando pela primeira página e terminando na página cinco:  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>Consulte também  
 [Acesso à URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](url-access-parameter-reference.md)  
  
  
