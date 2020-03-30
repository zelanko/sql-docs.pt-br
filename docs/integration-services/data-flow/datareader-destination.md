---
title: Destino do DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 484464550b08f209bb271a806c496e87417c0d99
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71293062"
---
# <a name="datareader-destination"></a>Destino DataReader

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O destino do DataReader expõe os dados em um fluxo de dados com o uso da interface **DataReader** do ADO.NET. Os dados podem ser consumidos por outros aplicativos. Por exemplo, você pode configurar a fonte de dados de um relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para usar o resultado de execução de um pacote do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para fazer isso, crie um fluxo de dados que implementa o destino do DataReader.  
  
 Para obter informações sobre como acessar e ler valores no destino do DataReader programaticamente, consulte [Carregando a saída de um pacote local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md).  
  
## <a name="configuration-of-the-datareader-destination"></a>Configuração do destino do DataReader  
 Você pode especificar um valor de tempo limite para o destino do DataReader e indicar se o destino deveria falhar se ocorresse um tempo limite. Um tempo limite ocorre se o aplicativo não fizer uma solicitação de dados no tempo especificado.  
  
 O destino do DataReader tem uma entrada. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do destino DataReader](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
