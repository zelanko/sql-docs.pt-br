---
title: Conectar componentes com caminhos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], connections
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 05633e4c-1370-4b05-802b-f36b07dd71c8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1a75a9717345d1d0dc4c2fe30bf7fc441cb91ddc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060393"
---
# <a name="connect-components-with-paths"></a>Conectar componentes com caminhos
  Você constrói o fluxo de dados em um pacote na superfície de design da guia **Fluxo de Dados** no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] . Se o fluxo de dados contiver dois componentes de fluxo de dados, você poderá conectá-los vinculando a saída de uma fonte ou transformação à entrada de uma transformação ou destino. O conector entre dois componentes de fluxo de dados é chamado de caminho.  
  
 O diagrama a seguir mostra um simples fluxo de dados com um componente de fonte, duas transformações, um componente de destino e os caminhos que os conecta.  
  
 ![Fluxo de dados](media/mw-dts-08.gif "Fluxo de dados")  
  
 Depois de dois componentes terem sido conectados, você pode visualizar os metadados dos dados que se movimentam através do caminho e as propriedades do caminho em **Editor de Caminho de Fluxo de Dados**. Para obter mais informações, consulte [Integration Services Paths](data-flow/integration-services-paths.md).  
  
 Você também pode adicionar os visualizadores de dados aos caminhos. Um visualizador de dados torna possível visualizar os dados que se movem entre os componentes de fluxo de dados quando o pacote é executado.  
  
### <a name="to-connect-components-in-a-data-flow"></a>Para conectar os componentes em um fluxo de dados  
  
-   [Conectar componentes em um fluxo de dados](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-set-path-properties"></a>Para definir as propriedades do caminho  
  
-   [Definir as propriedades de um caminho por meio do Editor de Caminho do Fluxo de Dados](../../2014/integration-services/set-the-properties-of-a-path-by-using-the-data-flow-path-editor.md)  
  
### <a name="to-view-path-metadata"></a>Para exibir os metadados do caminho  
  
-   [Exibir metadados do caminho no Editor de Caminho do Fluxo de Dados](../../2014/integration-services/view-path-metadata-in-the-data-flow-path-editor.md)  
  
### <a name="to-view-path-metadata"></a>Para exibir os metadados do caminho  
  
-   [Adicionar um visualizador de dados a um fluxo de dados](../../2014/integration-services/add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefa de Fluxo de Dados](control-flow/data-flow-task.md)   
 [Fluxo de Dados](data-flow/data-flow.md)   
 [Transformar dados com transformações](data-flow/transformations/transform-data-with-transformations.md)   
 [Tratamento de erros em dados](data-flow/error-handling-in-data.md)  
  
  
