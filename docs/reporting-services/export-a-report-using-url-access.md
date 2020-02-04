---
title: Exportar um relatório usando o acesso à URL | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 24cc4fbe1a1cadeeb9c2e94fe0da85fce24db8a6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65571498"
---
# <a name="export-a-report-using-url-access"></a>Exportar um relatório com acesso à URL
  Opcionalmente, você pode especificar o formato no qual renderizará um relatório com o parâmetro de URL *rs:Format* .  Os formatos HTML 4.0 e HTM5 (extensão de renderização) realizarão a renderização no navegador e, para outros formatos, o navegador solicitará a gravação da saída de relatório em um arquivo local.  
  
 Por exemplo, para obter uma cópia em PDF de um relatório diretamente de um servidor de relatório de modo nativo:  
  
```  
https://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
 E, em um servidor de relatório no modo integrado do SharePoint:  
  
```  
https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
 
::: moniker-end
 
 Por exemplo, o seguinte comando de URL no seu navegador exporta um relatório PPTX de uma instância nomeada do servidor de relatório:  
  
```  
https://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Os valores válidos desse parâmetro se baseiam nas extensões de renderização de relatório que estão instaladas no servidor de relatório que está sendo acessado. Extensões comuns são HTML4.0, MHTML, IMAGE, EXCELOPENXML (xlsx), WORDOPENXML (docx), CSV, PDF, XML e NULL. Se uma extensão de renderização especificada não estiver instalada no servidor de relatórios, o relatório não será renderizado, e um erro será gerado e exibido no pesquisador.  
  
 Se você não incluir o parâmetro *Format* como parte da URL, o servidor de relatórios detectará o pesquisador e renderizará o relatório no formato HTML apropriado.  
  
## <a name="see-also"></a>Consulte Também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  
