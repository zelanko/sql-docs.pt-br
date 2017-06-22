---
title: "Implementando uma extensão de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 372d21a412efec6306912950e7f9f5a6f577ee3f
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="implementing-a-data-processing-extension"></a>Implementando uma extensão de processamento de dados
  As extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permitem que você se conecte a uma fonte de dados e recupere dados. Eles também servem como uma ponte entre uma fonte de dados e um conjunto de dados. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]extensões de processamento de dados são modeladas com um subconjunto do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] interfaces de provedor de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral de extensões de processamento de dados](../../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)  
 Apresenta como escrever uma extensão de processamento de dados personalizada para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparando para implementar uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/preparing-to-implement-a-data-processing-extension.md)  
 Descreve as interfaces disponíveis durante a implementação de uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], como também quando você precisa implementar uma interface específica.  
  
 [Criando uma biblioteca de extensões de processamento de dados](../../../reporting-services/extensions/data-processing/creating-a-data-processing-extension-library.md)  
 Descreve a atribuição de um namespace para a sua extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e a compilação da sua extensão de processamento de dados em uma DLL de biblioteca.  
  
 [Implementando uma classe de Conexão para uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-connection-class-for-a-data-processing-extension.md)  
 Descreve os atributos de uma conexão e como implementar sua própria **Conexão** classe para a sua extensão de processamento de dados.  
  
 [Implementando uma classe de comando para uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-command-class-for-a-data-processing-extension.md)  
 Descreve os atributos de um comando e como implementar sua própria **comando** classe para a sua extensão de processamento de dados.  
  
 [Implementando uma classe DataReader para uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-datareader-class-for-a-data-processing-extension.md)  
 Descreve os atributos de um leitor de dados e como implementar sua própria **DataReader** classe para a sua extensão de processamento de dados.  
  
 [Usando um conjunto de dados externo com o Reporting Services](../../../reporting-services/extensions/data-processing/using-an-external-dataset-with-reporting-services.md)  
 Descreve como expor personalizados **DataSet** objetos para o servidor de relatório para consumo.  
  
 [Implantando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
 Descreve como implantar a sua extensão de processamento de dados.  
  
 [Depurando código de extensão de processamento de dados](../../../reporting-services/extensions/data-processing/debugging-data-processing-extension-code.md)  
 Descreve como depurar código em suas extensões de processamento de dados.  
  
 [Removendo uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/removing-a-data-processing-extension.md)  
 Descreve como remover uma extensão de processamento de dados de um servidor de relatório ou do Designer de Relatórios.  
  
 Para obter um exemplo de uma extensão de processamento de dados totalmente implementada, consulte [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
