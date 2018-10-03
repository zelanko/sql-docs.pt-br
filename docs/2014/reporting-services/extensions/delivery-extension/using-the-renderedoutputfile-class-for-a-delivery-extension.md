---
title: Usando a classe RenderedOutputFile para uma extensão de entrega | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 37b6c2201326ede7c4dc42dffc4fa831136c50a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078516"
---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>Usando a classe RenderedOutputFile para uma extensão de entrega
  A classe de <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> representa um fluxo de dados e informações sobre as propriedades associadas ao fluxo de dados. A propriedade **Data** da classe <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> é usada para representar um relatório renderizado ou relatar um recurso como um objeto **Stream**.  
  
 O método <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> do objeto **Report** retorna uma matriz de um ou mais objetos <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> que juntos constituem um único relatório renderizado. O primeiro objeto de <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> é o relatório renderizado. Qualquer outro objeto de <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> será o recurso a ser entregue junto com os dados de relatório (por exemplo, um arquivo HTML e as imagens associadas). A renderização de extensões que são extensões de renderização de fluxo único (IMAGE, PDF, MHTML e EXCEL) retornará só um objeto de <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> na matriz.  
  
 Para obter um exemplo de como usar a classe <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>, consulte [Amostras de produto do SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
