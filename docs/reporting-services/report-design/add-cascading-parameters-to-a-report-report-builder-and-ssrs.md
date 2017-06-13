---
title: "Adicionar parâmetros em cascata a um relatório (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a22eec3-57a7-478e-b6fc-102a9dbe0591
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8efc7a0b7120faa53a63bd07c51029a1b379f9e
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="add-cascading-parameters-to-a-report-report-builder-and-ssrs"></a>Adicionar parâmetros em cascata a um relatório (Construtor de Relatórios e SSRS)
  Os parâmetros em cascata fornecem um modo de gerenciar grandes volumes de dados de relatório. É possível definir um conjunto de parâmetros relacionados de forma que a lista de valores de um parâmetro dependa do valor escolhido em outro parâmetro. Por exemplo, o primeiro parâmetro é independente e pode apresentar uma lista de categorias de produtos. Quando o usuário seleciona uma categoria, o segundo parâmetro é dependente do valor do primeiro parâmetro. Seus valores são atualizados com uma lista de subcategorias dentro da categoria escolhida. Quando o usuário exibe o relatório, os valores dos dois parâmetros de categoria e subcategoria são usados para filtrar dados do relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Para criar parâmetros em cascata, primeiro você define a consulta de conjunto de dados e inclui um parâmetro de consulta para cada parâmetro em cascata necessário. Você também deve criar um conjunto de dados separado para cada parâmetro em cascata para fornecer valores disponíveis. Para obter mais informações, consulte [Adicionar, alterar ou excluir valores disponíveis de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md).  
  
 A ordem é importante para parâmetros em cascata porque a consulta do conjunto de dados para um parâmetro posterior na lista inclui uma referência a cada parâmetro anterior na lista. Em tempo de execução, a ordem dos parâmetros no painel de dados do relatório determina a ordem na qual as consultas de parâmetro aparecem no relatório e, portanto, a ordem na qual um usuário escolhe cada valor de parâmetro sucessivo.  
  
 Para obter informações sobre como criar parâmetros em cascata com diversos valores e o recurso Selecionar Tudo, consulte [Como ter um parâmetro em cascata de diversos valores com Selecionar Tudo](http://go.microsoft.com/fwlink/?LinkId=184757).  
  
## <a name="to-create-the-main-dataset-with-a-query-that-includes-multiple-related-parameters"></a>Para criar o conjunto de dados principal com uma consulta que inclui múltiplos parâmetros relacionados  
  
1.  No painel Dados do Relatório, clique com o botão direito do mouse em uma fonte de dados e clique em **Adicionar Conjunto de Dados**.  
  
2.  Em **Nome**, digite o nome do conjunto de dados.  
  
3.  Em **Fonte de Dados**, escolha o nome da fonte de dados ou clique em **Nova** para criar uma.  
  
4.  Em **Tipo de consulta**, escolha o tipo de consulta para a fonte de dados selecionada. Neste tópico, o tipo de consulta **Text** é assumido.  
  
5.  Em **Consulta**, digite a consulta a ser usada para recuperar dados para este relatório. A consulta deve incluir as seguintes partes:  
  
    1.  Uma lista de campos de fonte de dados. Por exemplo, em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] , a instrução SELECT especifica uma lista de nomes de colunas do banco de dados de uma determinada tabela ou exibição.  
  
    2.  Um parâmetro de consulta para cada parâmetro em cascata. Um parâmetro de consulta limita os dados recuperados da fonte de dados especificando determinados valores a serem incluídos ou excluídos da consulta. Normalmente, parâmetros de consulta ocorrem em uma cláusula de restrição na consulta. Por exemplo, em uma instrução SELECT do [!INCLUDE[tsql](../../includes/tsql-md.md)] , os parâmetros de consulta ocorrem na cláusula WHERE. Para obter mais informações, consulte "Filtering Rows by Using WHERE and HAVING" na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online do SQL Server](http://go.microsoft.com/fwlink/?linkid=120955).  
  
6.  Clique em **Executar** (**!**). Depois que você incluir parâmetros de consulta e executar a consulta, os parâmetros do relatório que correspondem aos parâmetros da consulta serão criados automaticamente.  
  
    > [!NOTE]  
    >  A ordem dos parâmetros de consulta na primeira vez que você executa uma consulta determina a ordem como eles são criados no relatório. Para alterar a ordem, consulte [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Em seguida, você criará um conjunto de dados que fornece os valores para o parâmetro independente.  
  
## <a name="to-create-a-dataset-to-provide-values-for-an-independent-parameter"></a>Para criar um conjunto de dados para fornecer valores para um parâmetro independente  
  
1.  No painel Dados do Relatório, clique com o botão direito do mouse em uma fonte de dados e clique em **Adicionar Conjunto de Dados**.  
  
2.  Em **Nome**, digite o nome do conjunto de dados.  
  
3.  Em **Fonte de Dados**, verifique se o nome é o nome da fonte de dados escolhida na etapa 1.  
  
4.  Em **Tipo de consulta**, escolha o tipo de consulta para a fonte de dados selecionada. Neste tópico, o tipo de consulta **Text** é assumido.  
  
5.  Em **Consulta**, digite a consulta a ser usada para recuperar valores para este parâmetro. Normalmente, consultas de parâmetros independentes não contêm parâmetros de consulta. Por exemplo, para criar uma consulta para um parâmetro que fornece todos os valores de categoria, você pode usar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] semelhante à seguinte:  
  
    ```  
    SELECT DISTINCT <column name> FROM <table>  
    ```  
  
     O comando SELECT DISTINCT remove valores duplicados do conjunto de resultados para que você obtenha cada valor exclusivo da coluna especificada na tabela especificada.  
  
     Clique em **Executar** (**!**). O conjunto de resultados mostra os valores que estão disponíveis para esse primeiro parâmetro.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Em seguida, você definirá as propriedades do primeiro parâmetro para usar este conjunto de dados para popular seus valores disponíveis em tempo de execução.  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>Para definir os valores disponíveis para um parâmetro de relatório  
  
1.  No painel Dados do Relatório, na pasta Parâmetros, clique com o botão direito do mouse no primeiro parâmetro e clique em **Propriedades do Parâmetro**.  
  
2.  Em **Nome**, verifique se o nome do parâmetro está correto.  
  
3.  Clique em **Valores Disponíveis**.  
  
4.  Clique em **Obter valores de uma consulta**. Três campos são exibidos.  
  
5.  Em **Conjunto de Dados**, na lista suspensa, clique no nome do conjunto de dados criado no procedimento anterior.  
  
6.  No campo **Valor** , clique no nome do campo que fornece o valor do parâmetro.  
  
7.  No campo **Rótulo** , clique no nome do campo que fornece o rótulo do parâmetro.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Em seguida, você criará um conjunto de dados que fornece os valores para um parâmetro dependente.  
  
## <a name="to-create-a-dataset-to-provide-values-for-a-dependent-parameter"></a>Para criar um conjunto de dados para fornecer valores para um parâmetro dependente  
  
1.  No painel Dados do Relatório, clique com o botão direito do mouse em uma fonte de dados e clique em **Adicionar Conjunto de Dados**.  
  
2.  Em **Nome**, digite o nome do conjunto de dados.  
  
3.  Em **Fonte de Dados**, verifique se o nome é o nome da fonte de dados escolhida na etapa 1.  
  
4.  Em **Tipo de consulta**, escolha o tipo de consulta para a fonte de dados selecionada. Neste tópico, o tipo de consulta **Text** é assumido.  
  
5.  Em **Consulta**, digite a consulta a ser usada para recuperar valores para este parâmetro. Normalmente, consultas para parâmetros dependentes incluem parâmetros de consulta para cada parâmetro do qual este parâmetro é dependente. Por exemplo, para criar uma consulta para um parâmetro que fornece todos os valores de subcategoria (parâmetro dependente) para uma categoria (parâmetro independente), você pode usar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] semelhante à seguinte:  
  
    ```  
    SELECT DISTINCT Subcategory FROM <table>   
    WHERE (Category = @Category)  
    ```  
  
     Na cláusula WHERE, a categoria é o nome de um campo de \<tabela > e @Category é um parâmetro de consulta. Essa instrução gera uma lista de subcategorias para a categoria especificada em @Category. Em tempo de execução, esse valor será preenchido com o valor escolhido pelo usuário para o parâmetro de relatório que tem o mesmo nome.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Em seguida, você definirá as propriedades do segundo parâmetro para usar este conjunto de dados para popular seus valores disponíveis em tempo de execução.  
  
## <a name="to-set-available-values-for-a-report-parameter"></a>Para definir os valores disponíveis para um parâmetro de relatório  
  
1.  No painel Dados do Relatório, na pasta Parâmetros, clique com o botão direito do mouse no primeiro parâmetro e clique em **Propriedades do Parâmetro**.  
  
2.  Em **Nome**, verifique se o nome do parâmetro está correto.  
  
3.  Clique em **Valores Disponíveis**.  
  
4.  Clique em **Obter valores de uma consulta**.  
  
5.  Em **Conjunto de Dados**, na lista suspensa, clique no nome do conjunto de dados criado no procedimento anterior.  
  
6.  No campo **Valor** , clique no nome do campo que fornece o valor do parâmetro.  
  
7.  No campo **Rótulo** , clique no nome do campo que fornece o rótulo do parâmetro.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-test-the-cascading-parameters"></a>Para testar os parâmetros em cascata  
  
1.  Clique em **Executar**.  
  
2.  Na lista suspensa do primeiro parâmetro independente, escolha um valor.  
  
     O processador de relatório executa a consulta de conjunto de dados para o próximo parâmetro e passa para ele o valor que você escolheu para o primeiro parâmetro. A lista suspensa do segundo parâmetro é populada com os valores disponíveis com base no valor do primeiro parâmetro.  
  
3.  Na lista suspensa do segundo, parâmetro dependente, escolha um valor.  
  
     O relatório não é executado automaticamente depois que você escolhe o último parâmetro de forma que você pode alterar sua escolha.  
  
4.  Clique em **Exibir Relatório**. O relatório atualiza a exibição com base nos parâmetros escolhidos.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar, alterar ou excluir um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Tutorial: Adicionar um parâmetro ao relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Tutoriais do Construtor de Relatórios](../../reporting-services/report-builder-tutorials.md)   
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
