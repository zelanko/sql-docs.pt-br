---
title: "Transformação não dinâmica | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d491bb19b4eb86bd0fe75a7b8ca8e7b6e5d226b5
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="unpivot-transformation"></a>Transformação Não Dinâmica
  A transformação não dinâmica transforma um conjunto de dados não normalizado em uma versão mais normalizada, expandindo valores de várias colunas de um único registro em vários registros, com os mesmos valores em uma única coluna. Por exemplo, um conjunto de dados que lista nomes de clientes tem uma linha para cada cliente, com os produtos e a quantidade comprada mostrados em colunas da linha. Depois que a transformação não dinâmica normaliza o conjunto de dados, este contém uma linha diferente para cada produto que o cliente comprou.  
  
 O diagrama a seguir mostra um conjunto de dados antes da transformação não dinâmica na coluna Produto.  
  
 ![Conjunto de dados após reverter a dinamização](../../../integration-services/data-flow/transformations/media/mw-dts-18.gif "conjunto de dados após reverter a dinamização")  
  
 O diagrama a seguir mostra um conjunto de dados depois da transformação não dinâmica na coluna Produto.  
  
 ![Conjunto de dados antes de reverter a dinamização](../../../integration-services/data-flow/transformations/media/mw-dts-17.gif "conjunto de dados antes de reverter a dinamização")  
  
 Em algumas circunstâncias, os resultados da transformação não dinâmica podem conter linhas com valores inesperados. Por exemplo, se os dados de exemplo a serem transformados mostrados no diagrama tivessem valores nulos em todas as colunas Qtd para Fred, a saída incluiria somente uma linha para Fred, e não cinco. A coluna Qtd conteria valor nulo ou zero, dependendo do tipo de dados da coluna.  
  
## <a name="configuration-of-the-unpivot-transformation"></a>Configuração da transformação Não Dinâmica  
 A transformação Não Dinâmica inclui a propriedade personalizada **PivotKeyValue** . Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada e uma saída. Não tem nenhuma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Não Dinâmica** , clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Não Dinâmica](../../../integration-services/data-flow/transformations/unpivot-transformation-editor.md)  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
