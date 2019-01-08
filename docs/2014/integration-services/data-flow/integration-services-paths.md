---
title: Caminhos do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aea7a95787d38ea81e584ea822dd7b521e44c7c2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790648"
---
# <a name="integration-services-paths"></a>Caminhos do Integration Services
  Um caminho conecta dois componentes em um fluxo de dados conectando a saída de um componente de fluxo de dados à entrada de outro componente. Um caminho tem uma origem e um destino. Por exemplo, se um caminho conectar uma origem OLE DB e uma transformação Classificação, a origem OLE DB será a origem do caminho e a transformação Classificação será o destino do caminho. A origem é o componente onde o caminho inicia, e o destino é o componente onde o caminho termina.  
  
 Se você executar um pacote no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , será possível exibir os dados em um fluxo de dados anexando visualizadores de dados a um caminho. Um visualizador de dados pode ser configurado para exibir dados em uma grade. Um visualizador de dados é uma ferramenta útil de depuração. Para obter mais informações, consulte [Debugging Data Flow](../troubleshooting/debugging-data-flow.md).  
  
## <a name="configuration-of-the-path"></a>Configuração do caminho  
 O Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece a caixa de diálogo **Editor de Caminho do Fluxo de Dados** para definir propriedades de caminho, exibindo os metadados das colunas de dados que passam pelo caminho e configurando visualizadores de dados.  
  
 As propriedades de caminho configurável incluem o nome, a descrição e a anotação do caminho. Você também pode configurar caminhos de forma programática. Para obter mais informações, consulte [Conectando componentes do fluxo de dados programaticamente](../building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
 Uma anotação de caminho exibe o nome da origem do caminho ou o nome do caminho na superfície de design da guia **Fluxo de Dados** no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] . As anotações de caminho são semelhantes às anotações que você pode adicionar a fluxos de dados, fluxos de controle e manipuladores de eventos. A única diferença é que uma anotação de caminho é anexada a um caminho, ao passo que outras anotações aparecem nas guias **Fluxo de Dados**, **Fluxo de Controle**e **Controle de Eventos**do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Os metadados exibem nome, tipo de dados, precisão, escala, comprimento, página de código e componente de origem de cada coluna na saída do componente anterior. O componente de origem é o componente de fluxo de dados que criou a coluna. Isso pode ou não ser o primeiro componente no fluxo de dados. Por exemplo, as transformações Union All e Classificação criam as próprias colunas e são as origens de suas colunas de saída. Em contrapartida, uma transformação Copiar Coluna pode passar por colunas sem as alterá-las ou pode criar colunas novas copiando as colunas de entrada. A transformação Copiar Coluna é o componente de origem somente das novas colunas.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Caminho do Fluxo de Dados** , clique em um dos seguintes tópicos:  
  
-   [Editor de caminho de fluxo de dados &#40;página geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de caminho de fluxo de dados &#40;página de metadados&#41;](../data-flow-path-editor-metadata-page.md)  
  
-   [Editor de caminho de fluxo de dados &#40;página visualizadores de dados&#41;](../data-flow-path-editor-data-viewers-page.md)  
  
 Para obter mais informações sobre as propriedades que podem ser definidas programaticamente, consulte [Path Properties](../path-properties.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Exibir metadados do caminho no Editor de Caminho do Fluxo de Dados](../view-path-metadata-in-the-data-flow-path-editor.md)  
  
-   [Conectar componentes em um fluxo de dados](connect-components-in-a-data-flow.md)  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](data-flow.md)  
  
  
