---
title: Destino do DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd361b6ca3f287c6874f734a1d3b6f4f3365b450
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="datareader-destination"></a>Destino DataReader
  O destino do DataReader expõe os dados em um fluxo de dados com o uso da interface **DataReader** do ADO.NET. Os dados podem ser consumidos por outros aplicativos. Por exemplo, você pode configurar a fonte de dados de um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para usar o resultado de execução de um pacote [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para fazer isso, crie um fluxo de dados que implementa o destino do DataReader.  
  
 Para obter informações sobre como acessar e ler valores no destino do DataReader programaticamente, consulte [Carregando a saída de um pacote local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md).  
  
## <a name="configuration-of-the-datareader-destination"></a>Configuração do destino do DataReader  
 Você pode especificar um valor de tempo limite para o destino do DataReader e indicar se o destino deveria falhar se ocorresse um tempo limite. Um tempo limite ocorre se o aplicativo não fizer uma solicitação de dados no tempo especificado.  
  
 O destino do DataReader tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do destino DataReader](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
