---
title: O que&#39;novo no construtor de relatórios para SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8223c19b-4b0d-4b1d-a042-9a726c18e708
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 15e4e4a90232f4db1b83b3a09d45589e6fcdeb8d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48226876"
---
# <a name="what39s-new-in-report-builder-for-sql-server-2014"></a>O que&#39;novo no construtor de relatórios para SQL Server 2014
  O [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] apresenta vários recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Para obter informações sobre os recursos nesta versão para outros [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] produtos e tecnologias, consulte [o que há de novo no SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
> [!TIP]  
>  Para obter as informações e os recursos mais recentes relativos aos novos recursos desta versão, consulte [Informações adicionais sobre as novidades do SQL Server Reporting Services (SSRS)](http://go.microsoft.com/fwlink/?LinkId=207147).  
  
##  <a name="ExcelRenderer"></a> Renderizador do Excel para Microsoft Excel 2007-2010 e Microsoft Excel 2003  
 A extensão de renderização do Excel do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], nova no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] renderiza um relatório como um documento do Excel compatível com [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2007-2010, bem como com [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2003 com o Pacote de Compatibilidade do Microsoft Office para Word, Excel e PowerPoint instalado. O formato é o Office Open XML e a extensão de arquivo dos arquivos é .xlsx.  
  
 Esta extensão de renderização do Excel remove limitações da versão anterior, compatíveis com o Excel 2003. Veja uma lista do aperfeiçoamento na extensão de renderização:  
  
-   O máximo de linhas por planilha é 1.048.576.  
  
-   O máximo de colunas por planilha é 16.384.  
  
-   O número de cores permitidas em uma planilha é aproximadamente de 16 milhões (cor de 24 bits).  
  
-   A compactação em ZIP fornece tamanhos de arquivos menores.  
  
 Para obter mais informações, consulte [Exportar para Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
##  <a name="WordRenderer"></a> Renderizador do Word para Microsoft Word 2007-2010 e Microsoft Word 2003  
 A extensão de renderização do Word do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], nova no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] renderiza um relatório como um documento do Word compatível com [!INCLUDE[ofprword](../includes/ofprword-md.md)] 2007-2010, bem como com [!INCLUDE[ofprword](../includes/ofprword-md.md)] 2003 com o Pacote de Compatibilidade do [!INCLUDE[msCoName](../includes/msconame-md.md)] Office para Word, Excel e PowerPoint instalado. O formato é o Office Open XML e a extensão de arquivo dos arquivos é docx.  
  
 Além de disponibilizar os recursos que são novos no Word 2007-2010 para relatórios exportados, os arquivos *.docx de relatórios exportados tendem a ser menores. Os relatórios exportados usando o renderizador do Word são geralmente significativamente menores que os mesmos relatórios exportados usando o renderizador do Word 2003.  
  
 Para obter mais informações, consulte [Exportar para Microsoft Word &#40;Construtor de Relatórios e SSRS&#41;](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
