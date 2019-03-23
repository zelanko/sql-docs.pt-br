---
title: Transformação de Reversão da Dinamização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottrans.f1
helpviewer_keywords:
- Unpivot transformation
- more normalized data set [Integration Services]
- normalized data [Integration Services]
- datasets [Integration Services], normalized data
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 98a8476ef317a0ddfa6f7fc27c0c9572ed12817a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385473"
---
# <a name="unpivot-transformation"></a>Transformação Não Dinâmica
  A transformação não dinâmica transforma um conjunto de dados não normalizado em uma versão mais normalizada, expandindo valores de várias colunas de um único registro em vários registros, com os mesmos valores em uma única coluna. Por exemplo, um conjunto de dados que lista nomes de clientes tem uma linha para cada cliente, com os produtos e a quantidade comprada mostrados em colunas da linha. Depois que a transformação não dinâmica normaliza o conjunto de dados, este contém uma linha diferente para cada produto que o cliente comprou.  
  
 O diagrama a seguir mostra um conjunto de dados antes da transformação não dinâmica na coluna Produto.  
  
 ![Conjunto de dados após sua dinamização ser revertida](../../media/mw-dts-18.gif "Conjunto de dados após sua dinamização ser revertida")  
  
 O diagrama a seguir mostra um conjunto de dados depois da transformação não dinâmica na coluna Produto.  
  
 ![Conjunto de dados antes da sua dinamização ser revertida](../../media/mw-dts-17.gif "Conjunto de dados antes da sua dinamização ser revertida")  
  
 Em algumas circunstâncias, os resultados da transformação não dinâmica podem conter linhas com valores inesperados. Por exemplo, se os dados de exemplo a serem transformados mostrados no diagrama tivessem valores nulos em todas as colunas Qtd para Fred, a saída incluiria somente uma linha para Fred, e não cinco. A coluna Qtd conteria valor nulo ou zero, dependendo do tipo de dados da coluna.  
  
## <a name="configuration-of-the-unpivot-transformation"></a>Configuração da transformação Não Dinâmica  
 A transformação Não Dinâmica inclui a propriedade personalizada `PivotKeyValue`. Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada e uma saída. Não tem nenhuma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Não Dinâmica** , clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Não Dinâmica](../../unpivot-transformation-editor.md)  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas de Transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
  
