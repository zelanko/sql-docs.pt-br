---
title: "Mesclar células em uma região de dados (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c643b94c86109a99e1448093b4b9744924fcd7f7
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>Mesclar células em uma região de dados (Construtor de Relatórios e SSRS)
Em um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você pode mesclar células em uma região de dados para combinar células, melhorar a aparência da região de dados ou fornecer rótulos que abrangem grupos de colunas e de linhas.  
  
Só é possível mesclar células em cada área de uma região de dados: canto, cabeçalhos de coluna, definição de grupo (ou cabeçalhos de linha) e corpo. Não é possível mesclar células que cruzam os limites da área. Por exemplo, você não pode mesclar uma célula na área do canto da região de dados com uma célula na área do grupo de linhas. Leia mais sobre [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-merge-cells-in-a-data-region"></a>Para mesclar células em uma região de dados  
  
1.  Na região de dados na superfície de design de relatório, clique na primeira célula a ser mesclada. Mantendo o botão esquerdo do mouse pressionado, arraste verticalmente ou horizontalmente para selecionar células adjacentes. As células selecionadas são realçadas.  
  
2.  Clique com o botão direito do mouse nas células selecionadas e selecione **Mesclar Células**. As células selecionadas são combinadas em uma única célula.  
  
3.  Repita as etapas 1 e 2 para mesclar outras células adjacentes em uma região de dados.  
  
## <a name="see-also"></a>Consulte também  
[Região de dados Tablix](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)  
 [Tabelas &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Criar uma matriz](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Criar faturas e formulários com listas](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
[Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  

