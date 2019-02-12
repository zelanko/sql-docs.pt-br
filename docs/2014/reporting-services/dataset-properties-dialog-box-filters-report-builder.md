---
title: Caixa de diálogo de propriedades do conjunto de dados, filtros (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10025"
ms.assetid: 933a6f44-4eb7-4e73-9c40-ac0fd17b23d3
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 58abc975b461c6d12778c95620eadedd4e6caf8a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030217"
---
# <a name="dataset-properties-dialog-box-filters-report-builder"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Filtros (Construtor de Relatórios)
  Selecione **Filtros** na caixa de diálogo **Propriedades do Conjunto de Dados** para criar filtros para o conjunto de dados.  
  
 Filtros que fazem parte de uma definição de conjunto de dados compartilhado no servidor de relatório afetam todos os relatórios que usam o conjunto de dados compartilhado. Filtros adicionais para o conjunto de dados compartilhado podem ser especificados depois de adicionados em um relatório. Esses filtros afetam somente o relatório no qual são definidos.  
  
 Filtros de um conjunto de dados inserido afetam apenas o relatório no qual são definidos.  
  
 Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opções  
 **Adicionar**  
 Adicione uma nova cláusula de filtro à lista.  
  
 **Delete (excluir)**  
 Exclua a cláusula de filtro selecionada da lista.  
  
 **Seta para cima**  
 Mova o filtro selecionado para cima na lista.  
  
 **Seta para baixo**  
 Mova o filtro selecionado para baixo na lista.  
  
 **Expression**  
 Digite ou escolha a expressão à qual deseja aplicar um filtro. Clique no botão Expressão (**fx**) para editar a expressão.  
  
 **Data type**  
 Escolha o tipo de dados para **Valor**. Sempre que possível, escolha um tipo de dados correspondente ao tipo de dados de **Expressão**.  
  
 Os valores em **Expressão** e **Valor** devem ser avaliados como o mesmo tipo de dados. Por exemplo, se a opção **Expressão** for definida como um campo que tem o tipo de dados System.Int32 e **Valor** como 7, na lista suspensa, escolha **Inteiro**.  
  
 Se a opção de tipo de dados necessária não estiver na lista suspensa, escreva uma expressão para converter o valor no tipo de dados correto. Para obter mais informações, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
 **Operador**  
 Selecione o operador que será usado para comparar a expressão e o valor.  
  
 **Value**  
 Digite a expressão ou o valor a ser usado quando for avaliar a expressão especificada na caixa **Expressão** . Clique no botão Expressão (**fx**) para editar a expressão.  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Adicionar um filtro a um conjunto de dados &#40;relatórios e SSRS&#41;](report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)   
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
