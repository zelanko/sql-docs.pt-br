---
title: Alterar um item em uma célula (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 91a54778-8929-41f9-bb4c-826cec636be4
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 9461a5cdfaf6b10d229380681b626ff2a6172bf1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115637"
---
# <a name="change-an-item-within-a-cell-report-builder-and-ssrs"></a>Alterar um item de uma célula (Construtor de Relatórios e SSRS)
  Somente um item não contêiner, como uma caixa de texto, linha ou imagem, pode ser substituído por um novo item de relatório. Por exemplo, é possível arrastar uma tabela para uma caixa de texto a fim de substituí-la pela tabela.  
  
 Se a célula contiver um item de contêiner, como um retângulo, lista, tabela ou matriz, o novo item será adicionado a ele em vez de substituí-lo. Para substituir um item por um novo item, exclua o contêiner. A exclusão do contêiner substitui o mesmo por uma caixa de texto, que você pode então substituir por outro item.  
  
 Por padrão, todas as células de uma tabela, matriz ou região de dados da lista contêm uma caixa de texto.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-an-item-within-a-cell"></a>Para alterar um item de uma célula  
  
-   Na guia **Inserir** , no grupo **Regiões de Dados** ou **Itens de Relatório** , clique no item que você deseja adicionar ao relatório e, em seguida, clique no relatório. O item será adicionado ao relatório.  
  
> [!NOTE]  
>  A caixa de diálogo **Propriedades da Imagem** é aberta quando você arrasta um item de relatório de imagem para uma célula, na qual é possível definir propriedades, como a origem da imagem, antes de adicionar a imagem à célula.  
  
## <a name="see-also"></a>Consulte também  
 [Imagens, caixas de texto, retângulos e linhas &#40;SSRS e construtor de relatórios&#41;](rectangles-and-lines-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  