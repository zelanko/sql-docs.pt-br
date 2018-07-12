---
title: Implementando uma extensão de processamento de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7d247becb7a50aa11ba1f42574938d441a627502
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230766"
---
# <a name="implementing-a-data-processing-extension"></a>Implementando uma extensão de processamento de dados
  As extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permitem que você se conecte a uma fonte de dados e recupere dados. Eles também servem como uma ponte entre uma fonte de dados e um conjunto de dados. As extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] são modeladas de acordo com um subconjunto das interfaces do provedor de dados do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral das extensões de processamento de dados](data-processing-extensions-overview.md)  
 Apresenta como escrever uma extensão de processamento de dados personalizada para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparar a implementação de uma extensão de processamento de dados](preparing-to-implement-a-data-processing-extension.md)  
 Descreve as interfaces disponíveis durante a implementação de uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], como também quando você precisa implementar uma interface específica.  
  
 [Criar uma biblioteca de extensões de processamento de dados](creating-a-data-processing-extension-library.md)  
 Descreve a atribuição de um namespace para a sua extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e a compilação da sua extensão de processamento de dados em uma DLL de biblioteca.  
  
 [Implementar uma classe Connection para uma extensão de processamento de dados](implementing-a-connection-class-for-a-data-processing-extension.md)  
 Descreve os atributos de uma conexão e como implementar sua própria classe **Connection** para a extensão de processamento de dados.  
  
 [Implementar uma classe Command para uma extensão de processamento de dados](implementing-a-command-class-for-a-data-processing-extension.md)  
 Descreve os atributos de um comando e como implementar sua própria classe **Command** para a extensão de processamento de dados.  
  
 [Implementar uma classe DataReader para uma extensão de processamento de dados](implementing-a-datareader-class-for-a-data-processing-extension.md)  
 Descreve os atributos de um leitor de dados e como implementar sua própria classe **DataReader** para a extensão de processamento de dados.  
  
 [Usar um conjunto de dados externo com o Reporting Services](using-an-external-dataset-with-reporting-services.md)  
 Descreve como expor os objetos **DataSet** personalizados para o servidor de relatório para consumo.  
  
 [Implantando uma extensão de processamento de dados](deploying-a-data-processing-extension.md)  
 Descreve como implantar a sua extensão de processamento de dados.  
  
 [Depurar o código de extensão de processamento de dados](debugging-data-processing-extension-code.md)  
 Descreve como depurar código em suas extensões de processamento de dados.  
  
 [Remover uma extensão de processamento de dados](removing-a-data-processing-extension.md)  
 Descreve como remover uma extensão de processamento de dados de um servidor de relatório ou do Designer de Relatórios.  
  
 Para obter uma amostra de uma extensão de processamento de dados totalmente implementada, consulte [Amostras de produto do SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
