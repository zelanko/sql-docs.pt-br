---
title: Adicionar ou excluir um grupo em uma região de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4de53c3c-c6fc-49ce-b692-3609fc0b3ec5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 7bb8794920bc4e6eec0db9917c6c6f656b8333ce
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159766"
---
# <a name="add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs"></a>Adicionar ou excluir um grupo em uma região de dados (Construtor de Relatórios e SSRS)
  Adicione um grupo a uma região de dados quando quiser organizar os dados por um valor ou conjunto de expressões específico para exibição e cálculos. Um grupo tem um nome e uma expressão que identificam quais dados de um conjunto de dados pertencem ao grupo. Para obter mais informações sobre grupos, consulte [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](understanding-groups-report-builder-and-ssrs.md).  
  
 Em uma região de dados tablix, clique na tabela, matriz ou lista para exibir o painel Agrupamento. Arraste campos do conjunto de dados para os painéis Grupo de Linhas e Grupo de Colunas para criar grupos pai ou filho. Clique com o botão direito do mouse em um grupo existente para adicionar um grupo adjacente. Por definição, o grupo de detalhes é o grupo interno e pode ser adicionado somente como um grupo filho. Clique com o botão direito do mouse em um grupo existente para excluí-lo. Linhas e colunas nas quais exibir valores de grupos são adicionadas automaticamente para você. Para obter mais informações, consulte [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
 Em uma região de dados do Gráfico, clique no gráfico para exibir as áreas para arrastar e soltar. Crie grupos arrastando campos do conjunto de dados para as áreas para arrastar e soltar categorias e séries. Para adicionar grupos aninhados, adicione vários campos à área para arrastar e soltar.  
  
 Por padrão, os grupos não são definidos em um medidor. O comportamento padrão do medidor é agregar todos os valores no campo especificado em um valor que é exibido no medidor. Para obter mais informações, consulte [Medidores &#40;Construtor de Relatórios e SSRS&#41;](gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-parent-or-child-row-or-column-group-to-a-tablix-data-region"></a>Para adicionar uma linha pai ou filho ou grupo de colunas a uma região de dados tablix  
  
1.  Arraste um campo do painel **Dados do Relatório** para o painel **Grupos de Linhas** ou para o painel **Grupos de Colunas** .  
  
    > [!NOTE]  
    >  Se o painel Agrupamento não estiver visível, na guia Exibir, clique em **Agrupamento**.  
  
2.  Solte o campo acima ou abaixo da hierarquia do grupo usando a barra de guias para colocar o grupo como um grupo pai ou filho em um grupo existente.  
  
     O grupo é adicionado com um nome padrão, expressão de grupo e expressão de classificação que é baseada no nome do campo.  
  
### <a name="to-add-an-adjacent-row-or-column-group-to-a-tablix-data-region"></a>Para adicionar uma linha adjacente ou grupo de colunas a uma região de dados tablix  
  
1.  No painel Agrupamento, clique com o botão direito do mouse em um grupo que seja do mesmo nível que o grupo que você deseja adicionar. Clique em **Adicionar Grupo**e em **Adjacente Antes** ou **Adjacente Após** para especificar onde adicionar o grupo. A caixa de diálogo **Grupo Tablix** é aberta.  
  
2.  Em **Nome**, digite um nome para o grupo.  
  
3.  Em **Expressão de grupo**, digite uma expressão ou clique no botão de expressão (**fx**) para criar uma expressão.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Um novo grupo é adicionado ao painel Agrupamento e uma linha ou coluna na qual exibir valores de grupo é adicionada à região de dados tablix na superfície de design.  
  
### <a name="to-add-a-details-group-to-a-tablix-data-region"></a>Para adicionar um grupo de detalhes a uma região de dados tablix  
  
1.  No painel Agrupamento, clique com o botão direito do mouse no grupo filho mais interno, mas não no grupo **Detalhes** . Clique em **Adicionar Grupo**e em **Grupo Filho**. A caixa de diálogo **Grupo Tablix** é aberta.  
  
2.  Em **Expressão de Grupo**, deixe a expressão em branco. Um grupo de detalhes não tem nenhuma expressão.  
  
3.  Selecione **Mostrar dados de detalhes**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Um novo grupo de detalhes é adicionado como um grupo filho ao painel Agrupamento e o identificador da linha do grupo selecionado na etapa 1 exibe o ícone do grupo de detalhes. Para obter mais informações sobre identificadores, consulte [Células, linhas e colunas da região de dados Tablix &#40;Construtor de Relatórios&#41; e SSRS](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
### <a name="to-edit-a-row-or-column-group-in-a-tablix-data-region"></a>Para editar uma linha ou um grupo de colunas em uma região de dados tablix  
  
1.  Na superfície de design de relatório, clique em qualquer lugar na região de dados tablix para selecioná-la. O painel Agrupamento exibe os grupos de linhas e colunas.  
  
2.  Clique com o botão direito do mouse no grupo e clique em **Propriedades do Grupo**.  
  
3.  Em **Nome**, digite o nome do grupo.  
  
4.  Em **Expressões de grupo**, digite ou selecione uma expressão simples ou clique no botão Expressão (**fx**) para criar uma expressão de grupo.  
  
5.  Clique em **Adicionar** para criar expressões adicionais. Todas as expressões especificadas são combinadas usando um AND lógico para especificar dados para esse grupo.  
  
6.  (Opcional) Clique em **Quebras de Página** para definir opções de quebra de página.  
  
7.  (Opcional) Clique em **Classificação** para selecionar ou digitar expressões que especificam a ordem de classificação dos valores no grupo.  
  
8.  (Opcional) Clique em **Visibilidade** para selecionar as opções de visibilidade do item.  
  
9. (Opcional) Clique em **Filtros** para definir filtros para esse grupo.  
  
10. (Opcional) Clique em **Variáveis** para definir variáveis com escopo para esse grupo e acessíveis de qualquer grupo filho.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-group-from-a-tablix-data-region"></a>Para excluir um grupo de uma região de dados tablix  
  
1.  No painel Agrupamento, clique com o botão direito do mouse no grupo e clique em **Excluir Grupo**.  
  
2.  Na caixa de diálogo **Excluir Grupo** , selecione uma das seguintes opções:  
  
    -   **Excluir grupo e linhas e colunas relacionadas** Escolha esta opção para excluir a definição do grupo e todas as linhas relacionadas que exibem dados do grupo. Para obter o grupo de detalhes, se a mesma linha pertencer a detalhes e a dados do grupo, só as linhas de dados de detalhes serão excluídas.  
  
    -   **Excluir grupo somente** Escolha esta opção para manter a mesma estrutura da região de dados tablix e excluir só a definição do grupo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-details-group-from-a-tablix-data-region"></a>Para excluir um grupo de detalhes de uma região de dados tablix  
  
1.  No painel Agrupamento, clique com o botão direito do mouse no grupo de detalhes e clique em **Excluir Grupo**.  
  
2.  Na caixa de diálogo **Excluir Grupo** , selecione uma das seguintes opções:  
  
    -   **Excluir grupo e linhas e colunas relacionadas** Escolha esta opção para excluir a definição do grupo e todas as linhas relacionadas que exibem dados do grupo. Para obter o grupo de detalhes, se a mesma linha pertencer a detalhes e a dados do grupo, só as linhas de dados de detalhes serão excluídas.  
  
    -   **Excluir grupo somente** Escolha esta opção para manter a mesma estrutura da região de dados tablix e excluir só a definição do grupo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     O grupo de detalhes é excluído.  
  
    > [!NOTE]  
    >  Depois da remoção de uma linha de detalhes, verifique se a expressão em cada célula especifica uma expressão de agregação quando apropriado. Se necessário, edite a expressão para especificar funções de agregação.  
  
## <a name="see-also"></a>Consulte também  
 [Referências de coleções de variáveis de grupo e de relatório &#40;Construtor de Relatórios e SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)   
 [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
