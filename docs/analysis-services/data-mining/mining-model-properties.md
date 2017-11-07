---
title: "Propriedades do modelo de mineração | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- Data Mining Designer
- properties [data mining]
ms.assetid: c5194619-8b31-42be-a95f-585711462945
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1fa45b604df0a118936f903491e707bd09d58295
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mining-model-properties"></a>Propriedades do modelo de mineração
  Os modelos de mineração têm os seguintes tipos de propriedades:  
  
-   As propriedades que são herdadas da estrutura de mineração que definem o tipo de dados e o tipo de conteúdo dos dados usados pelo modelo;  
  
-   As propriedades que são relacionadas ao algoritmo usadas para criar o modelo de mineração, inclusive os parâmetros de cliente;  
  
-   As propriedades que definem um filtro no modelo usado para treinar o modelo.  
  
 As propriedades de um modelo de mineração são inicialmente definidas quando você cria o modelo; porém, você pode alterar a maioria das propriedades posteriormente, inclusive os parâmetros de algoritmo, filtros e uso de coluna. Você pode alterar as propriedades usando a guia **Modelos de Mineração** do Designer de Data Mining ou usando AMO ou XMLA.  
  
 Sempre que você alterar uma propriedade de um modelo, deve processar novamente o modelo para que as alterações sejam refletidas no modelo. O reprocessamento é necessário mesmo se a alteração envolver apenas metadados, como a adição de um alias ou descrição de coluna.  
  
## <a name="properties-of-models"></a>Propriedades de modelos  
 A tabela a seguir descreve as propriedades que são específicas para modelos de mineração. Adicionalmente, há propriedades que você pode definir em colunas individuais na mineração  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**Algoritmo**|Define o tipo de algoritmo do modelo de mineração.|  
|**AlgorithmParameters**|Define valores para os parâmetros dos algoritmos disponíveis para cada tipo de algoritmo.|  
|**Filtro**|Define um filtro que é aplicado aos dados que são usados para treinar e testar o modelo de mineração. A definição do filtro é armazenada com o modelo e pode ser usada opcionalmente quando consultas de previsão são criadas ou quando você testar a exatidão do modelo.<br /><br /> O filtro de modelo não é opcional para o treinamento do modelo.|  
|**Nome**|Define o nome do modelo de mineração.|  
|**AllowDrillThrough**|Especifica se a análise está habilitada no modelo de mineração.|  
  
## <a name="properties-of-model-columns"></a>Propriedades das colunas de modelo  
 Você pode definir as seguintes propriedades específicas da mineração de dados para cada coluna em um modelo de mineração. Você pode definir essas propriedades com um valor diferente em cada modelo de mineração em uma estrutura de mineração.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**Description**|Descreve a finalidade da coluna de mineração.|  
|**Nome**|Define o nome da coluna do modelo de mineração. Você pode digitar um novo nome, para fornecer um alias à coluna do modelo de mineração.|  
|**ModelingFlags**|Define qualquer sinalizador específico de um algoritmo para a coluna.|  
|**SourceColumnID**|Indica o nome da coluna de estrutura de mineração na qual a coluna de modelo é baseada.<br /><br /> Esta propriedade é somente leitura.|  
|**Uso**|Define como a coluna será usada pelo modelo de mineração.|  
  
## <a name="see-also"></a>Consulte também  
 [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md)   
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Alterar as propriedades de um modelo de mineração](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [Ferramentas de mineração de dados](../../analysis-services/data-mining/data-mining-tools.md)   
 [Criar uma estrutura de mineração relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [Criar um alias para uma coluna de modelo](../../analysis-services/data-mining/create-an-alias-for-a-model-column.md)  
  
  

