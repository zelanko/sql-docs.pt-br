---
title: Inserir ou excluir uma linha (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bd9f92b0128bd6280654885f79f8231570f721de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105630"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>Inserir ou excluir uma linha (Construtor de Relatórios e SSRS)
  Você pode adicionar ou excluir linhas em uma região de dados tablix. Essa região pode ser uma tabela, uma matriz ou uma lista. Os procedimentos a seguir não se aplicam às regiões de dados de gráficos e medidores.  
  
 Na região de dados Tablix, você pode adicionar linhas associadas a um grupo (dentro de um grupo) ou que não estão associadas a um grupo (fora de um grupo). Uma linha que está dentro de um grupo é repetida uma vez por valor de grupo único. Por exemplo, uma linha dentro de um grupo com base em valor em uma coluna de dados que contém nomes de cores é repetida uma vez por nome de cor distinto. Para grupos aninhados, uma linha pode estar fora do grupo filho, mas dentro do grupo pai. Nesse caso, a linha se repete uma vez para cada valor único no grupo pai.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>Para selecionar uma região de dados para que os identificadores de linha e coluna sejam exibidos  
  
-   No modo Design, clique no canto superior esquerdo da região de dados Tablix para que os indicadores de linha e coluna sejam exibidos acima ou próximo dele.  
  
     Para obter mais informações sobre áreas da região de dados, consulte [lista &#40;construtor de relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
### <a name="to-insert-a-row-in-a-selected-data-region"></a>Para inserir uma linha em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse no identificador de linha no qual você deseja inserir uma linha, clique em **Inserir Linha**e depois em **Acima** ou **Abaixo**.  
  
     \- ou –  
  
-   Clique com o botão direito do mouse em uma célula na região de dados na qual você deseja inserir uma linha, clique em **Inserir Linha**e depois em **Acima** ou **Abaixo**.  
  
### <a name="to-delete-a-row-from-a-selected-data-region"></a>Para excluir uma linha de uma região de dados selecionada  
  
-   Selecione uma ou mais linhas a serem excluídas, clique com o botão direito do mouse no identificador de uma das linhas selecionadas e clique em **Excluir Linhas**.  
  
     \- ou –  
  
-   Clique com o botão direito do mouse em uma célula na região de dados na qual você deseja excluir uma linha e clique em **Excluir Linhas**.  
  
### <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>Para inserir uma linha em um grupo em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse em uma célula de grupo de linhas na área de grupo de linhas de uma região de dados Tablix na qual deseja inserir uma linha, clique em **Inserir Linha**e depois em **Acima – Fora do Grupo**, **Acima – Dentro do Grupo**, **Abaixo – Dentro do Grupo**ou **Abaixo – Fora do Grupo**.  
  
     Uma linha é adicionada dentro ou fora do grupo representado pela célula do grupo de linhas na qual você clicou.  
  
### <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>Para excluir uma linha de um grupo em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse em uma célula do grupo de linhas na área do grupo de colunas de uma região de dados Tablix na qual você deseja excluir uma linha e clique em **Excluir Linhas**.  
  
## <a name="see-also"></a>Consulte também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
