---
title: Exportar um relatório usando o acesso à URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b90f1ad3e67aafa2ee8b967f8a04ddb16daf4e53
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132897"
---
# <a name="export-a-report-using-url-access"></a>Exportar um relatório com acesso à URL
  Opcionalmente, você pode especificar o formato no qual renderizar um relatório usando o *rs: Format* parâmetro. Por exemplo, para obter uma cópia em PDF de um relatório diretamente de um servidor de relatório de modo nativo:  
  
```  
http://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  
  
 E, em um servidor de relatório no modo integrado do SharePoint:  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
  
 Os valores válidos desse parâmetro se baseiam nas extensões de renderização de relatório que estão instaladas no servidor de relatório que está sendo acessado. Extensões comuns são HTML4.0, MHTML, IMAGE, EXCEL, WORD, CSV, PDF, XML e NULL. Se uma extensão de renderização especificada não estiver instalada no servidor de relatórios, o relatório não será renderizado, e um erro será gerado e exibido no pesquisador.  
  
 Se você não incluir o parâmetro *Format* como parte da URL, o servidor de relatórios detectará o pesquisador e renderizará o relatório no formato HTML apropriado.  
  
## <a name="see-also"></a>Consulte também  
 [Acesso à URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](url-access-parameter-reference.md)  
  
  
