---
title: "Exportar um relatório usando o acesso à URL | Microsoft Docs"
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
caps.latest.revision: "42"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 8087e6e9c1ca644a1e1b302bebfbdae1598622b6
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="export-a-report-using-url-access"></a>Exportar um relatório com acesso à URL
  Opcionalmente, você pode especificar o formato no qual renderizará um relatório com o parâmetro de URL *rs:Format* .  Os formatos HTML 4.0 e HTM5 (extensão de renderização) realizarão a renderização no navegador e, para outros formatos, o navegador solicitará a gravação da saída de relatório em um arquivo local.  
  
 Por exemplo, para obter uma cópia em PDF de um relatório diretamente de um servidor de relatório de modo nativo:  
  
```  
http://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  
  
 E, em um servidor de relatório no modo integrado do SharePoint:  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
  
 Por exemplo, o seguinte comando de URL no seu navegador exporta um relatório PPTX de uma instância nomeada do servidor de relatório:  
  
```  
http://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Os valores válidos desse parâmetro se baseiam nas extensões de renderização de relatório que estão instaladas no servidor de relatório que está sendo acessado. Extensões comuns são HTML4.0, MHTML, IMAGE, EXCELOPENXML (xlsx), WORDOPENXML (docx), CSV, PDF, XML e NULL. Se uma extensão de renderização especificada não estiver instalada no servidor de relatórios, o relatório não será renderizado, e um erro será gerado e exibido no pesquisador.  
  
 Se você não incluir o parâmetro *Format* como parte da URL, o servidor de relatórios detectará o pesquisador e renderizará o relatório no formato HTML apropriado.  
  
## <a name="see-also"></a>Consulte Também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  
