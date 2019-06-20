---
title: Mesclar células em uma região de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 97e9280512b75aebfccb93c0e11e5402136fa6f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105573"
---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>Mesclar células em uma região de dados (Construtor de Relatórios e SSRS)
  Você pode mesclar células em uma região de dados para combinar células, melhorar a aparência da região de dados ou fornecer rótulos que abrangem grupos de colunas e de linhas.  
  
> [!NOTE]  
>  As células só podem ser mescladas dentro de cada área de uma região de dados: canto, cabeçalho de coluna, definição de grupo (ou cabeçalhos de linha) e corpo. Não é possível mesclar células que cruzam os limites da área. Por exemplo, você não pode mesclar uma célula na área do canto da região de dados com uma célula na área do grupo de linhas. Para obter mais informações sobre áreas tablix, consulte [lista &#40;construtor de relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-merge-cells-in-a-data-region"></a>Para mesclar células em uma região de dados  
  
1.  Na região de dados na superfície de design de relatório, clique na primeira célula a ser mesclada. Mantendo o botão esquerdo do mouse pressionado, arraste verticalmente ou horizontalmente para selecionar células adjacentes. As células selecionadas são realçadas.  
  
2.  Clique com o botão direito do mouse nas células selecionadas e selecione **Mesclar Células**. As células selecionadas são combinadas em uma única célula.  
  
3.  Repita as etapas 1 e 2 para mesclar outras células adjacentes em uma região de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
