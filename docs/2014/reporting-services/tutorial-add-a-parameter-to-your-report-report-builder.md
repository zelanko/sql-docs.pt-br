---
title: 'Tutorial: Adicionar um parâmetro ao relatório (construtor de relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eab34ec4-b3ad-4a76-95cc-07b2f75ee6d7
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 02d7879bab489d92f6c5897406d3dce12b279d96
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238229"
---
# <a name="tutorial-add-a-parameter-to-your-report-report-builder"></a>Tutorial: Adicionar um parâmetro ao relatório (Construtor de Relatórios)
  Adicione um parâmetro ao relatório para permitir que os usuários filtrem dados do relatório na fonte de dados ou no relatório. Os parâmetros de relatório são criados automaticamente para cada parâmetro de consulta incluído em uma consulta de conjunto de dados. O tipo de dados do parâmetro determina como ele aparece na barra de ferramentas de exibição de relatório.  
  
 ![rs_tut_Parameter](../../2014/tutorials/media/rs-tut-parameter.gif "rs_tut_Parameter")  
  
##  <a name="BackToTop"></a> O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
1.  [Criar um relatório de matriz e um conjunto de dados do Assistente de tabela ou matriz](#Setup)  
  
2.  [Organizar dados, escolher Layout e estilo de Assistente de tabela ou matriz](#CompleteWizard)  
  
3.  [Adicionar um parâmetro de consulta para criar um parâmetro de relatório](#Query)  
  
4.  [Alterar o tipo de dados padrão e outras propriedades de um parâmetro de relatório](#ChangeDefaultProperties)  
  
    1.  [Adicionar um conjunto de dados para fornecer valores disponíveis e nomes para exibição](#AddDataset)  
  
    2.  [Especificar os valores disponíveis para criar uma lista suspensa de valores](#AvailableValues)  
  
    3.  [Especificar valores padrão para que o relatório seja executado automaticamente](#DefaultValues)  
  
    4.  [Procurar um valor de um conjunto de dados com pares nome/valor](#NameValue)  
  
5.  [Exibir o valor do parâmetro selecionado no relatório](#Expression)  
  
6.  [Usar o parâmetro de relatório em um filtro](#Filter)  
  
7.  [Altere o parâmetro de relatório para aceitar vários valores](#Multivalued)  
  
8.  [Adicionar um parâmetro booliano para visibilidade condicional](#Boolean)  
  
9. [Adicionar um título de relatório](#Title)  
  
10. [Salvar o relatório](#Save)  
  
> [!NOTE]  
>  Neste tutorial, as etapas do assistente são consolidadas em um procedimento. Para obter instruções passo a passo sobre como procurar um servidor de relatório, escolher uma fonte de dados e criar um conjunto de dados, consulte o primeiro tutorial desta série: [Tutorial: Criação de um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo estimado para concluir este tutorial: 25 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Setup"></a> 1. Criar um relatório de matriz e um conjunto de dados no Assistente de Tabela ou Matriz  
 Criar um relatório de matriz, uma fonte de dados e um conjunto de dados.  
  
> [!NOTE]  
>  Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-create-a-new-matrix-report"></a>Para criar um novo relatório de matriz  
  
1.  Clique em **inicie**, aponte para **programas**, aponte para [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **construtor de relatórios**e, em seguida, clique em **construtor de relatórios**.  
  
     A caixa de diálogo **Guia de Introdução** é exibida.  
  
    > [!NOTE]  
    >  Se o **guia de Introdução** caixa de diálogo não aparece, da **construtor de relatórios** , clique em **New**.  
  
2.  No painel esquerdo, verifique se **Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Tabela ou Matriz**.  
  
4.  Clique em **Criar**.  
  
5.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados**.  
  
6.  Clique em **Avançar**.  
  
7.  Na página **Escolher uma conexão com uma fonte de dados**, selecione uma fonte de dados do tipo **SQL Server**. Selecione uma fonte de dados na lista ou navegue até o servidor de relatório para selecionar uma.  
  
8.  Clique em **Avançar**.  
  
9. Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
10. Cole a seguinte consulta no painel de consulta:  
  
    ```  
    ;WITH CTE (StoreID, Subcategory, Quantity)   
    AS (  
    SELECT 200 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 2002 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Camcorders' AS Subcategory, 1954 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Accessories' AS Subcategory, 1895 AS Quantity  
    UNION SELECT  199 AS StoreID, 'Digital Cameras' AS Subcategory, 1849 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1579 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Camcorders' AS Subcategory, 1561 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital Cameras' AS Subcategory, 1553 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Accessories' AS Subcategory, 1534 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Accessories' AS Subcategory, 1755 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Camcorders' AS Subcategory, 1631 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1772 AS Quantity)  
    SELECT StoreID, Subcategory, Quantity  
    FROM CTE  
    ```  
  
     Esta consulta combina os resultados de várias instruções SELECT [!INCLUDE[tsql](../includes/tsql-md.md)] dentro de uma expressão de tabela comum para especificar valores baseados em dados simplificados do banco de dados de exemplo Contoso. Os dados de vendas em Contoso representam os dados de vendas internacionais de bens de consumo. Este tutorial usa dados de vendas de câmeras. As subcategorias representam câmeras digitais, câmeras digitais SLR (reflex de lente única), filmadoras e acessórios.  
  
     A consulta especifica nomes de coluna que incluem um identificador de repositório, uma subcategoria de item de vendas e a quantidade solicitada para ordens de venda de três repositórios. Nesta consulta, o nome do repositório não faz parte do conjunto de resultados. Posteriormente neste tutorial, você irá pesquisar o nome do repositório que corresponde ao identificador de repositório de um conjunto de dados separado.  
  
     Esta consulta não contém parâmetros de consulta. Você adicionará parâmetros de consulta posteriormente neste tutorial.  
  
11. Na barra de ferramentas do designer de consultas, clique em **Executar** (**!**). O conjunto de resultados exibe 11 linhas de dados que mostram a quantidade de itens vendidos para cada subcategoria de quatro repositórios e inclui as seguintes colunas: StoreID, Subcategory, Quantity.  
  
12. Clique em **Avançar**.  
  
##  <a name="CompleteWizard"></a> 2. Organizar dados, escolher layout e estilo no Assistente de Tabela ou Matriz  
 Use o assistente para fornecer um design inicial no qual exibir dados. O painel de visualização no assistente ajuda a visualizar o resultado do agrupamento de dados antes de concluir o design da tabela ou da matriz.  
  
#### <a name="to-organize-data-into-groups"></a>Para organizar dados em grupos  
  
1.  Na página **Organizar campos** , arraste Subcategoria até **Grupos de linhas**.  
  
2.  Arraste StoreID até **Grupos de colunas**.  
  
3.  Arraste Quantity até **Valores**.  
  
     Você organizou os valores das quantidades vendidas em linhas agrupadas por subcategoria. Haverá uma coluna para cada repositório.  
  
4.  Clique em **Avançar**.  
  
5.  No **escolher um Layout** página, em **opções**, verifique **Mostrar subtotais e totais gerais** está selecionado.  
  
     Quando você executar o relatório, a última coluna mostrará a quantidade total de cada subcategoria para todos os repositórios, e a última linha mostrará a quantidade total para todas as subcategorias de cada repositório.  
  
6.  Clique em **Avançar**.  
  
7.  Sobre o **escolher um estilo** página, no painel Estilos, selecione um estilo.  
  
8.  Clique em **Concluir**.  
  
     A matriz é adicionada à superfície de design. A matriz exibe três colunas e três linhas. As células na primeira linha contêm Subcategory, [StoreID] e Total. As células na segunda linha contêm expressões que representam a subcategoria, a quantidade de itens vendidos para cada repositório e a quantidade total de cada subcategoria para todos os repositórios. As células na linha final exibem o total geral de cada repositório.  
  
9. Clique na matriz, passe o mouse sobre a borda da primeira coluna e arraste a alça para aumentar a largura da coluna.  
  
10. Clique em **Executar** para visualizar o relatório.  
  
 O relatório será executado no servidor de relatório e exibirá o título e a hora em que o processamento de relatório ocorreu.  
  
 Neste cenário, os títulos de coluna exibem o identificador, mas não o nome do repositório. Posteriormente, você irá adicionar uma expressão para pesquisar o nome do repositório em um conjunto de dados contendo pares de identificador/nome do repositório.  
  
##  <a name="Query"></a> 3. Adicionar um parâmetro de consulta para criar um parâmetro de relatório  
 Quando você adicionar um parâmetro de consulta a uma consulta, o Construtor de Relatórios criará automaticamente um parâmetro de relatório de valor único com propriedades padrão para nome, aviso e tipo de dados.  
  
#### <a name="to-add-a-query-parameter"></a>Para adicionar um parâmetro de consulta  
  
1.  Alterne para o modo Design.  
  
2.  No painel Dados do Relatório, expanda a pasta **Conjuntos de Dados** , clique com o botão direito do mouse em **DataSet1**e clique em **Consulta**.  
  
3.  Adicione o seguinte [!INCLUDE[tsql](../includes/tsql-md.md)] `WHERE` cláusula como a última linha na consulta:  
  
    ```  
    WHERE StoreID = (@StoreID)  
    ```  
  
     O `WHERE` cláusula limita os dados recuperados ao identificador de loja especificado pelo parâmetro de consulta *@StoreID*.  
  
4.  Na barra de ferramentas do designer de consultas, clique em **Executar** (**!**). A caixa de diálogo **Definir Parâmetros de Consulta** é aberta e solicita um valor para o parâmetro de consulta *@StoreID*.  
  
5.  Em **Valor do Parâmetro**, digite **200**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     O conjunto de resultados exibe as quantidades vendidas de Acessórios, Filmadoras e Câmeras Digitais SLR do identificador de loja **200**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  No painel Dados do Relatório, expanda a pasta **Parâmetros** .  
  
 Observe que agora há um parâmetro de relatório denominado *@StoreID*. Por padrão, o parâmetro tem tipo de dados **texto**. Como o identificador de repositório é um inteiro, você precisará alterar o tipo de dados para Inteiro no próximo procedimento.  
  
##  <a name="ChangeDefaultProperties"></a> 4. Alterar o tipo de dados padrão e outras propriedades de um parâmetro de relatório  
 Depois de criar um parâmetro, você pode ajustar os valores padrão de propriedades.  
  
#### <a name="to-change-the-default-data-type-for-a-report-parameter"></a>Para alterar o tipo de dados padrão de um parâmetro de relatório  
  
1.  No painel de dados do relatório na **parâmetros** nó, clique com botão direito *@StoreID*e, em seguida, clique em **propriedades do parâmetro**.  
  
2.  No Prompt, digite **identificador Store?** Este texto aparece na barra de ferramentas do visualizador de relatórios quando você executa o relatório.  
  
3.  Em **Tipo de dados**, na lista suspensa, selecione **Inteiro**.  
  
4.  Aceite os valores padrão restantes na caixa de diálogo.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Visualize o relatório. O Visualizador de relatórios exibe o prompt para *@StoreID*.  
  
7.  Na barra de ferramentas do visualizador de relatórios, ao lado de ID da Loja, digite **200**e clique em **Exibir Relatório**.  
  
##  <a name="AddDataset"></a> 4a. Adicionar um conjunto de dados para fornecer valores disponíveis e nomes para exibição  
 Para garantir que um usuário possa digitar somente valores válidos para um parâmetro, você pode criar uma lista suspensa de valores a serem escolhidos. Os valores podem vir de um conjunto de dados ou de uma lista especificada por você. Devem ser fornecidos valores disponíveis de um conjunto de dados que contenha uma consulta sem referência ao parâmetro.  
  
#### <a name="to-create-a-dataset-for-valid-values-for-a-parameter"></a>Para criar um conjunto de dados com valores válidos para um parâmetro  
  
1.  Alterne para o modo Design.  
  
2.  No painel Dados do Relatório, clique com o botão direito do mouse na pasta **Conjuntos de Dados** e clique em **Adicionar Conjunto de Dados**.  
  
3.  Em **Nome**, digite **Lojas**.  
  
4.  Selecione o **usar um conjunto de dados inserido em meu relatório** opção.  
  
5.  Na **fonte de dados**, na lista suspensa, escolha a fonte de dados que você criou no primeiro procedimento.  
  
6.  Em **Tipo de consulta**, verifique se **Texto** está selecionado.  
  
7.  Em **Consulta**, cole o seguinte texto:  
  
    ```  
    SELECT 200 AS StoreID, 'Contoso Catalog Store' as StoreName  
    UNION SELECT 199 AS StoreID, 'Contoso North America Online Store' as StoreName  
    UNION SELECT 307 AS StoreID, 'Contoso Asia Online Store' as StoreName  
    UNION SELECT 306 AS StoreID, 'Contoso Europe Online Store' as StoreName  
    ```  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     O painel Dados do Relatório exibe os campos StoreID e StoreName no nó de conjunto de dados **Lojas** .  
  
##  <a name="AvailableValues"></a> 4B. Especificar os valores disponíveis para criar uma lista suspensa de valores  
 Depois de criar um conjunto de dados para fornecer valores disponíveis, altere as propriedades do relatório para especificar o conjunto de dados e o campo a serem usados para preencher a lista suspensa de valores válidos na barra de ferramentas do visualizador de relatórios.  
  
#### <a name="to-provide-available-values-for-a-parameter-from-a-dataset"></a>Para fornecer valores disponíveis para um parâmetro a partir de um conjunto de dados  
  
1.  No painel de dados do relatório, clique com botão direito o parâmetro *@StoreID*e, em seguida, clique em **as propriedades de parâmetro**.  
  
2.  Clique em **Valores Disponíveis**e em **Obter valores de uma consulta**.  
  
3.  Em **Conjunto de Dados**, na lista suspensa, clique em **Repositórios**.  
  
4.  Em **Campo de valor**, na lista suspensa, clique em StoreID.  
  
5.  Em **Campo de rótulo**, na lista suspensa, clique em StoreName. O campo de rótulo especifica o nome para exibição do valor.  
  
6.  Clique em **Geral**.  
  
7.  No Prompt, digite **nome Store?**  
  
     O usuário selecionará agora em uma lista de nomes de repositório, em vez de identificadores de repositório. Observe que o tipo de dados de parâmetro permanece **Inteiro** porque o parâmetro se baseia no identificador de loja, não no nome de loja.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Visualize o relatório.  
  
     Na barra de ferramentas do Visualizador de relatórios, a caixa de texto de parâmetro agora é uma lista suspensa que exibe  **\<selecione um valor >**.  
  
10. Na lista suspensa, selecione Contoso catálogo Store e, em seguida, clique em **Exibir relatório**.  
  
 O relatório exibe a quantidade vendida de Acessórios, Filmadoras e Câmeras Digitais SLR para o identificador de repositório **200**.  
  
##  <a name="DefaultValues"></a> 4 núcleos. Especificar os valores padrão para que o relatório seja executado automaticamente  
 Você pode especificar um valor padrão para cada parâmetro, de forma que o relatório seja executado automaticamente.  
  
#### <a name="to-specify-a-default-value-from-a-dataset"></a>Para especificar um valor padrão a partir de um conjunto de dados  
  
1.  Alterne para o modo Design.  
  
2.  No painel Dados do Relatório, clique com o botão direito do mouse em *@StoreID*e clique em **Propriedades do Parâmetro**.  
  
3.  Clique em **valores padrão**e, em seguida, clique em **obter valores de uma consulta**.  
  
4.  Em **Conjunto de Dados**, na lista suspensa, clique em **Repositórios**.  
  
5.  Em **Campo de valor**, na lista suspensa, clique em StoreID.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Visualize o relatório.  
  
 Para *@StoreID*, o Visualizador de relatórios exibe o valor "Contoso North America Online Store". Este é o primeiro valor do conjunto de resultados para o conjunto de dados **repositórios**. O relatório exibe a quantidade vendida de Câmeras Digitais do identificador de loja **199**.  
  
#### <a name="to-specify-a-custom-default-value"></a>Para especificar um valor padrão personalizado  
  
1.  Alterne para o modo Design.  
  
2.  No painel Dados do Relatório, clique com o botão direito do mouse em *@StoreID*e clique em **Propriedades do Parâmetro**.  
  
3.  Clique em **valores padrão**e clique em **especificar valores**e, em seguida, clique em **adicionar**. Uma nova linha de valor é adicionada.  
  
4.  Em **Valor**, digite **200**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Visualize o relatório.  
  
 Para *@StoreID*, o Visualizador de relatórios exibe o valor "Store de catálogos Contoso". Esse é o nome de exibição para o identificador de repositório **200**. O relatório exibe a quantidade vendida de Acessórios, Filmadoras e Câmeras Digitais SLR para o identificador de repositório **200**.  
  
##  <a name="NameValue"></a> 4d. Pesquisar um valor em um conjunto de dados com pares de nome/valor  
 Um conjunto de dados pode conter o identificador e o campo de nome correspondente. Quando você só tiver um identificador, poderá pesquisar o nome correspondente em um conjunto de dados criado por você, incluindo pares de nome/valor.  
  
#### <a name="to-look-up-a-value-from-a-dataset"></a>Para pesquisar um valor em um conjunto de dados  
  
1.  Alterne para o modo Design.  
  
2.  Na superfície de design, dentro da matriz, no cabeçalho de coluna da primeira linha, clique com o botão direito do mouse em `[StoreID]` e clique em **Expressão**.  
  
3.  No painel de expressão, exclua todo o texto exceto o `equals` (=) inicial.  
  
4.  Em **Categoria**, expanda **Funções Comuns**e clique em **Diversos**. O painel Item exibe um conjunto de funções.  
  
5.  Em Item, clique duas vezes em **Pesquisa**. O painel de expressão exibe `=Lookup(`. O painel Exemplo exibe um exemplo de sintaxe de Pesquisa.  
  
6.  Digite a seguinte expressão: `=Lookup(Fields!StoreID.Value,Fields!StoreID.Value,Fields!StoreName.Value,"Stores")`  
  
     A função Pesquisa irá pesquisar o valor de StoreID no conjunto de dados "Repositórios" e retornar o valor StoreName.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     O cabeçalho de coluna de repositórios contém o texto exibido para uma expressão complexa:  **< \<Expr >>**.  
  
8.  Visualize o relatório.  
  
 A caixa de texto na parte superior de cada página exibe o nome do repositório, em vez do identificador do repositório.  
  
##  <a name="Expression"></a> 5. Exibir o valor selecionado de parâmetro no relatório  
 Quando um usuário tem dúvidas sobre um relatório, é útil saber quais foram os valores de parâmetros escolhidos. Você pode preservar os valores selecionados pelos usuários para cada parâmetro no relatório. Uma forma de fazer isso é exibir os parâmetros em uma caixa de texto no rodapé da página.  
  
#### <a name="to-display-the-selected-parameter-value-and-label-on-a-page-footer"></a>Para exibir o valor de parâmetro selecionado e o rótulo em um rodapé de página  
  
1.  Alterne para o modo Design.  
  
2.  Clique com botão direito no rodapé da página, aponte para **inserir**e, em seguida, clique em **caixa de texto**. Arraste a caixa de texto para junto da caixa de texto com o carimbo de data/hora. Arraste a alça lateral da caixa de texto para expandir sua largura.  
  
3.  No painel Dados do Relatório, arraste o parâmetro *@StoreID* até a caixa de texto. A caixa de texto exibe `[@StoreID]`.  
  
4.  Para exibir o rótulo de parâmetro, clique na caixa de texto até aparecer o cursor de inserção depois da expressão existente, digite um espaço e arraste outra cópia do parâmetro do painel de dados do relatório para a caixa de texto. A caixa de texto exibe `[@StoreID] [@StoreID]`.  
  
5.  A primeira expressão com o botão direito e clique em **expressão**. A caixa de diálogo **Expressão** é aberta. Substitua o texto `Value` por `Label`.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     O texto exibe: `[@StoreID.Label] [@StoreID]`.  
  
7.  Visualize o relatório.  
  
##  <a name="Filter"></a> 6. Usar o parâmetro de relatório em um filtro  
 Os filtros ajudam a controlar os dados a serem usados em um relatório, depois de recuperados em uma fonte de dados externa. Para permitir que um usuário ajude a controlar os dados que deseja consultar, você pode incluir o parâmetro de relatório em um filtro para a matriz.  
  
#### <a name="to-specify-a-parameter-in-a-matrix-filter"></a>Para especificar um parâmetro em um filtro de matriz  
  
1.  Alterne para o modo Design.  
  
2.  Clique com o botão direito do mouse em um identificador de cabeçalho de linha ou coluna na matriz e clique em **Propriedades do Tablix**.  
  
3.  Clique em **Filtros**e em **Adicionar**. Uma nova linha de filtro é exibida.  
  
4.  Em **Expressão**, na lista suspensa, selecione o campo de conjunto de dados StoreID. O tipo de dados exibe **Inteiro**. Quando o valor da expressão for um campo de conjunto de dados, o tipo de dados será definido automaticamente.  
  
5.  Na **operador**, verifique `equals` (=) está selecionado.  
  
6.  Em **Valor**, digite `[@StoreID]`. `[@StoreID]` é a sintaxe de expressão simples que representa `=Parameters!StoreID.Value`.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Visualize o relatório.  
  
     A matriz só exibe dados para o "Repositório de Catálogos Contoso".  
  
9. Na barra de ferramentas do visualizador de relatórios, para **Nome da loja?**, selecione **Loja Online Contoso na Ásia**e clique em **Exibir Relatório**.  
  
 A matriz exibe dados correspondentes ao repositório que você selecionou.  
  
##  <a name="Multivalued"></a> 7. Alterar o parâmetro de relatório para aceitar vários valores  
 Para alterar um parâmetro de valor único para vários valores, você deve alterar a consulta e todas as expressões que contêm alguma referência ao parâmetro, inclusive filtros. Um parâmetro de vários valores é uma matriz de valores. Em uma consulta de conjunto de dados, a sintaxe de consulta deve testar a inclusão de um valor em um conjunto de valores. Em uma expressão de relatório, a sintaxe da expressão deve acessar uma matriz de valores, em vez de um valor individual.  
  
#### <a name="to-change-a-parameter-from-single-to-multivalued"></a>Para alterar um parâmetro de valor único para vários valores  
  
1.  Alterne para o modo Design.  
  
2.  No painel Dados do Relatório, clique com o botão direito do mouse em *@StoreID*e clique em **Propriedades do Parâmetro**.  
  
3.  Selecione **Permitir vários valores**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  No painel Dados do Relatório, expanda a pasta **Conjuntos de Dados** , clique com o botão direito do mouse em **DataSet1**e clique em **Consulta**.  
  
6.  Alteração `equals` (=) para `IN` na [!INCLUDE[tsql](../includes/tsql-md.md)] `WHERE` cláusula na última linha na consulta:  
  
    ```  
    WHERE StoreID IN (@StoreID)  
    ```  
  
     O operador `IN` testa um valor para inclusão em um conjunto de valores.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Clique com o botão direito do mouse em um identificador de cabeçalho de linha ou coluna na matriz e clique em **Propriedades do Tablix**.  
  
9. Clique em **Filtros**.  
  
10. Em **Operador**, selecione **Dentro**.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Na caixa de texto que exibe o parâmetro no rodapé da página, exclua todo o texto.  
  
13. Clique com o botão direito do mouse na caixa de texto e clique em **Expressão**. Digite a seguinte expressão: `=Join(Parameters!StoreID.Label, ", ")`  
  
     Esta expressão concatena todos os nomes de repositório selecionados pelo usuário.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. Clique na caixa de texto em frente à expressão que você acaba de criar e digite o seguinte: Valores de Parâmetros Selecionados:.  
  
16. Visualize o relatório.  
  
17. Clique na lista suspensa junto a Nome do Repositório?  
  
     Cada valor válido aparece junto a uma caixa de seleção.  
  
18. Clique em **Selecionar Tudo**e em **Exibir Relatório**.  
  
     O relatório exibe a quantidade vendida de todas as subcategorias de todos os repositórios.  
  
19. Na lista suspensa, clique em **Selecionar Tudo** para limpar a lista, clique em “Loja de Catálogos Contoso” e em “Loja Online Contoso na Ásia” e em **Exibir Relatório**.  
  
##  <a name="Boolean"></a> 8. Adicionar um parâmetro booliano para visibilidade condicional  
  
#### <a name="to-add-a-boolean-parameter"></a>Para adicionar um parâmetro booliano  
  
1.  Na superfície de design, no painel Dados do Relatório, clique com o botão direito do mouse em **Parâmetros**e clique em **Adicionar Parâmetro**.  
  
2.  Em **Nome**, digite ShowSelections.  
  
3.  Em **Prompt**, digite Mostrar seleções?  
  
4.  Na **tipo de dados**, na lista suspensa, clique em **booliano**.  
  
5.  Clique em **Valores Padrão**.  
  
6.  Clique em **Especificar valor**e em **Adicionar**.  
  
7.  Em **Valor**, digite **False**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-set-visibility-based-on-a-boolean-parameter"></a>Para definir a visibilidade com base em um parâmetro booliano  
  
1.  Na superfície de design, clique com o botão direito do mouse na caixa de texto no rodapé de página que exibe os valores de parâmetros e clique em **Propriedades da Caixa de Texto**.  
  
2.  Clique em **Visibilidade**.  
  
3.  Selecione a opção **Mostrar ou ocultar com base em uma expressão**e clique no botão de expressão **Fx**.  
  
4.  Digite a seguinte expressão: `=Not Parameters!ShowSelections.Value`  
  
     A opção de Visibilidade de caixa de texto é controlada pela propriedade Oculta. Aplique o operador `Not` de forma que, quando o parâmetro for selecionado, a propriedade Oculta seja falsa e a caixa de texto seja exibida.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Visualize o relatório.  
  
     A caixa de texto que exibe as escolhas de parâmetro não aparece.  
  
8.  Na barra de ferramentas do Visualizador de relatórios, ao lado **mostrar seleções**, clique em `True`.  
  
9. Visualize o relatório.  
  
 A caixa de texto no rodapé da página exibe todos os nomes de repositório selecionados por você.  
  
##  <a name="Title"></a> 9. Adicionar um título de relatório  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite Vendas de Produto com Parâmetros e clique fora da caixa de texto.  
  
##  <a name="Save"></a> 10. Salvar o relatório  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
     A mensagem **Conectando-se a um servidor de relatório**é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por Relatório de Vendas com Parâmetros.  
  
5.  Clique em **Salvar**.  
  
 O relatório será salvo no servidor de relatório. O servidor de relatório ao qual você está conectado aparece na barra de status na parte inferior da janela.  
  
## <a name="next-steps"></a>Próximas etapas  
 Isso conclui o passo a passo da adição de um parâmetro ao seu relatório. Para saber mais sobre parâmetros, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
