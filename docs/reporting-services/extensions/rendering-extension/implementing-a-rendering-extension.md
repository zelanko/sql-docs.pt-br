---
title: "Implementando uma extensão de renderização | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 68e74b4a67a1edc6517c9e6b2b0160ce2db258b9
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-a-rendering-extension"></a>Implementando uma extensão de renderização
  Uma extensão de renderização é um componente ou um módulo de um servidor de relatório que transforma dados de relatório e informações de layout para um formato específico do dispositivo. O SQL Server Reporting Services inclui seis extensões de renderização: HTML, Excel, Word, CSV ou Texto, XML, Imagem e PDF. Você pode criar extensões de renderização adicionais para gerar relatórios em outros formatos.  
  
> [!NOTE]  
>  Para determinar quais extensões de renderização estão disponíveis, exiba a lista das extensões instaladas no arquivo RSReportServer.config.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral de extensões de renderização](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
 Introduz como escrever uma extensão de renderização personalizada para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Implementando a Interface IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)  
 Descreve os atributos de uma extensão de renderização.  
  
 [Implantando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
 Descreve como implantar uma extensão de renderização em um servidor de relatório.  
  
 [Removendo uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/removing-a-rendering-extension.md)  
 Descreve como remover uma extensão de renderização de um servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
