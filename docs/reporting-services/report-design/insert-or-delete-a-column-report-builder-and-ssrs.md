---
title: "Inserir ou excluir uma coluna (construtor de relatórios e SSRS) | Microsoft Docs"
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
ms.assetid: e9db79e2-7e7d-4359-a706-cb746c94182a
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0dfa69257be349f7da24de5a1d6313cbd280105e
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="insert-or-delete-a-column-report-builder-and-ssrs"></a>Inserir ou excluir uma coluna (Construtor de Relatórios e SSRS)
  Você pode adicionar ou excluir colunas em uma região de dados tablix em um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Essa região pode ser uma tabela, uma matriz ou uma lista. Os procedimentos a seguir não se aplicam às regiões de dados de gráficos e medidores.  
  
 Em uma região de dados tablix, é possível adicionar colunas associadas a um grupo (dentro de um grupo) ou que não estejam associadas a um grupo (fora de um grupo). Uma coluna que está dentro de um grupo é repetida uma vez por valor de grupo único. Por exemplo, uma coluna dentro de um grupo com base em valor em uma coluna de dados que contém nomes de cores é repetida uma vez por nome de cor distinto. Para grupos aninhados, uma coluna pode estar fora do grupo filho, mas dentro do grupo pai. Nesse caso, a linha se repete uma vez para cada valor único no grupo pai.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-that-the-row-and-column-handles-appear"></a>Para selecionar uma região de dados para que os identificadores de linha e coluna sejam exibidos  
  
-   Na exibição de Design, clique no canto superior esquerdo da região de dados tablix para que os indicadores de coluna e linha sejam exibidos acima e ao lado dela.  
  
     Para obter mais informações sobre áreas de regiões de dados, consulte [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
## <a name="to-insert-a-column-in-a-selected-data-region"></a>Para inserir uma coluna em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse na alça da coluna na qual você deseja inserir uma coluna, clique em **Inserir Coluna**e depois em **Esquerda** ou **Direita**.  
  
     – ou –  
  
-   Clique com o botão direito do mouse em uma célula na região de dados na qual você deseja inserir uma linha, clique em **Inserir Coluna**e depois em **Esquerda** ou **Direita**.  
  
## <a name="to-delete-a-column-from-a-selected-data-region"></a>Para excluir uma coluna de uma região de dados selecionada  
  
-   Selecione uma ou mais colunas que deseja excluir, clique com o botão direito do mouse na alça de uma das colunas selecionadas e clique em **Excluir Colunas**.  
  
     – ou –  
  
-   Clique com o botão direito do mouse em uma célula na região de dados na qual você deseja excluir uma coluna e clique em **Excluir Colunas**.  
  
## <a name="to-insert-a-column-in-a-group-in-a-selected-data-region"></a>Para inserir uma coluna em um grupo em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse em uma célula do grupo de colunas, na área do grupo de colunas de uma região de dados tablix na qual você deseja inserir uma coluna, clique em **Inserir Coluna**e em **Esquerda – Fora do Grupo**, **Esquerda – Dentro do Grupo**, **Direita – Dentro do Grupo**ou **Direita – Fora do Grupo**.  
  
     Uma coluna é adicionada dentro ou fora do grupo representado pela célula do grupo de colunas na qual você clicou.  
  
## <a name="to-delete-a-column-from-a-group-in-a-selected-data-region"></a>Para excluir uma coluna de um grupo em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse em uma célula do grupo de colunas, na área do grupo de colunas de uma região de dados tablix na qual você deseja excluir uma coluna, e clique em **Excluir Colunas**.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
