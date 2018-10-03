---
title: Destino do DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3bed24bd847c0b2c02fcfb2370c59c93f2524682
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215036"
---
# <a name="datareader-destination"></a>Destino DataReader
  O destino do DataReader expõe os dados em um fluxo de dados com o uso da interface `DataReader` do ADO.NET. Os dados podem ser consumidos por outros aplicativos. Por exemplo, você pode configurar a fonte de dados de um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para usar o resultado de execução de um pacote [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para fazer isso, crie um fluxo de dados que implementa o destino do DataReader.  
  
 Para obter informações sobre como acessar e ler valores no destino do DataReader programaticamente, consulte [Carregando a saída de um pacote local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md).  
  
## <a name="configuration-of-the-datareader-destination"></a>Configuração do destino do DataReader  
 Você pode especificar um valor de tempo limite para o destino do DataReader e indicar se o destino deveria falhar se ocorresse um tempo limite. Um tempo limite ocorre se o aplicativo não fizer uma solicitação de dados no tempo especificado.  
  
 O destino do DataReader tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas do destino DataReader](datareader-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
  
