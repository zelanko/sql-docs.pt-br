---
title: Editor de transformação mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- Merge Join Transformation Editor
ms.assetid: ac06f419-30b3-42aa-8b34-42000bec4285
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1f548972d99242a4bc3d3423eeed748de2c31704
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116922"
---
# <a name="merge-join-transformation-editor"></a>Editor de Transformação Mesclagem
  Use a caixa de diálogo **Editor de Transformação Mesclar Junção** para especificar o tipo de junção, as colunas de junção e as colunas de saída para mesclar duas entradas combinadas por uma junção.  
  
> [!IMPORTANT]  
>  A Transformação Junção de Mesclagem requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Para saber mais sobre transformação Mesclagem de Junção, consulte [Merge Join Transformation](data-flow/transformations/merge-join-transformation.md).  
  
## <a name="options"></a>Opções  
 **Tipo de junção**  
 Especifique se você quer usar uma junção interna, externa esquerda ou completa.  
  
 **Trocar Entradas**  
 Troque a ordem entre entradas usando o botão **Trocar Entradas** . Essa seleção pode ser útil com a opção de Junção externa esquerda.  
  
 **Entrada**  
 Para cada coluna que você desejar na saída mesclada, selecione primeiro na lista de entradas disponíveis.  
  
 São exibidas entradas em duas tabelas separadas. Selecione colunas a serem incluídas na saída. Arraste colunas para criar uma junção entre as tabelas. Para excluir uma junção, selecione-a e pressione a tecla DELETE.  
  
 **Coluna de Entrada**  
 Selecione uma coluna a incluir na saída mesclada da lista de colunas disponíveis na entrada selecionada.  
  
 **Alias de Saída**  
 Digite um alias para cada coluna de saída. O padrão é o nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Classificar dados para transformações de junção de mesclagem e de mesclagem](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)   
 [Estender um conjunto de dados usando a transformação mesclar junção](data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)   
 [Transformação de mesclagem](data-flow/transformations/merge-transformation.md)   
 [Transformação Unir Tudo](data-flow/transformations/union-all-transformation.md)  
  
  