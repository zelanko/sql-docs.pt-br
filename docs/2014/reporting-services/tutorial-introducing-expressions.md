---
title: 'Tutorial: Apresentação de expressões | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 79563abac2c6a9ed64dff93667ff3d3966b70bc5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098852"
---
# <a name="tutorial-introducing-expressions"></a>Tutorial: Apresentando expressões
  As expressões o ajudam a criar relatórios avançados e flexíveis. Este tutorial ensina a criar e implementar expressões que utilizam funções e operadores comuns. Você usará a caixa de diálogo **expressão** para escrever expressões que concatenam valores de nome, pesquisam valores em um conjunto de um DataSet separado, exibem imagens diferentes com base em valores de campo e assim por diante.  
  
 O relatório é um relatório de barras com cores de linhas alternadas em branco e uma cor. O relatório inclui um parâmetro para selecionar a cor das linhas que não são brancas.  
  
 A ilustração a seguir mostra um relatório semelhante ao que você criará.  
  
 ![rs_ExpressionsTutorial](../../2014/tutorials/media/rs-expressionstutorial.gif "rs_ExpressionsTutorial")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
1.  [Criar um relatório de tabela e conjunto de dados no Assistente de Tabela ou Matriz](#Setup)  
  
2.  [Atualizar nomes padrão da fonte de dados ou do conjunto de dados](#UpdateNames)  
  
3.  [Exibir nome, inicial e sobrenome](#Concatenate)  
  
4.  [Usar imagens para exibir sexo](#Gender)  
  
5.  [Pesquisar nome de CountryRegion](#Lookup)  
  
6.  [Contar dias desde a última compra](#Count)  
  
7.  [Usar um indicador para mostrar comparação de vendas](#Indicator)  
  
8.  [Tornar o relatório um relatório de "barra verde"](#GreenBar)  
  
### <a name="other-optional-steps"></a>Outras etapas opcionais  
  
-   [Formatar coluna de data](#DateFormat)  
  
-   [Adicionar um título de relatório](#Title)  
  
-   [Salvar o relatório](#Save)  
  
 Tempo estimado para concluir este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-table-report-and-dataset-from-the-table-or-matrix-wizard"></a><a name="Setup"></a>1. criar um relatório de tabela e um conjunto de relatórios do assistente de tabela ou matriz  
 Crie um relatório de tabela, uma fonte de dados e um conjunto de dados. Ao criar o layout da tabela, você incluirá apenas alguns campos. Depois de concluir o assistente, você adicionará manualmente colunas. O assistente facilita a criação de layout da tabela e a aplicação de um estilo.  
  
> [!NOTE]  
>  Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
> [!NOTE]  
>  Neste tutorial, as etapas do assistente são consolidadas em um procedimento. Para obter instruções passo a passo sobre como procurar um servidor de relatório, escolher uma fonte de dados e criar um conjunto de dados, consulte o primeiro tutorial desta série: [Tutorial: Criação de um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
#### <a name="to-create-a-new-table-report"></a>Para criar um novo relatório de tabela  
  
1.  Clique em **Iniciar**, aponte para **programas**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]clique em **Construtor de relatórios**e, em seguida, clique em **Construtor de relatórios**.  
  
     A caixa de diálogo **introdução** é exibida.  
  
    > [!NOTE]  
    >  Se a caixa de diálogo **introdução** não for exibida, no botão **Construtor de relatórios** , clique em **novo**.  
  
    > [!NOTE]  
    >  Se preferir usar a versão do ClickOnce do Construtor de Relatórios, abra Report Manager e clique em **Construtor de relatórios**ou vá para um site do SharePoint no qual Reporting Services tipos de conteúdo como relatórios estão habilitados e clique em **Construtor de relatórios relatório** no menu **novo documento** na guia **documentos** de uma biblioteca de documentos compartilhados.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Tabela ou Matriz**.  
  
4.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados**.  
  
5.  Clique em **Avançar**.  
  
6.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados do tipo **SQL Server**. Selecione uma fonte de dados na lista ou navegue até o servidor de relatório para selecionar uma.  
  
7.  Clique em **Avançar**.  
  
8.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
9. Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Unknown' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2010-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2010-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2010-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2010-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2010-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2010-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2010-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2010-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2010-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2010-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2010-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2010-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2010-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2010-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2010-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2010-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2010-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2010-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2010-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2010-11-30' AS date) AS LastPurchase  
    ```  
  
     A consulta especifica nomes de colunas que incluem data de nascimento, nome, sobrenome, estado ou província, identificador de país/região, sexo e compras desde o início do ano.  
  
10. Na barra de ferramentas do designer de consultas, clique em **executar** (**!**). O conjunto de resultados exibe 20 linhas de dados e inclui as seguintes colunas: FirstName, LastName, StateProvince, CountryRegionID, Gender, YTDPurchase e LastPurchase.  
  
11. Clique em **Avançar**.  
  
12. Na página **Organizar campos** , arraste os campos a seguir, na ordem especificada, da lista **Campos Disponíveis** para a lista **Valores** .  
  
    -   StateProvince  
  
    -   CountryRegionID  
  
    -   LastPurchase  
  
    -   YTDPurchase  
  
     Como CountryRegionID e YTDPurchase contêm dados numéricos, a agregação SUM é aplicada a eles por padrão.  
  
    > [!NOTE]  
    >  Os campos FirstName e LastName não estão incluídos. Você irá adicioná-los em uma etapa posterior.  
  
13. Na lista **valores** , clique `CountryRegionID` com o botão direito do mouse e clique na opção **soma** .  
  
     A Soma não é mais aplicada a CountryRegionID.  
  
14. Na lista **Valores** , clique com o botão direito do mouse em **YTDPurchase** e clique na opção **Soma** .  
  
     A Soma não é mais aplicada a YTDPurchase.  
  
15. Clique em **Avançar**.  
  
16. Na página **Escolher o layout**, clique em **Avançar**.  
  
17. Na página **escolher um estilo** , clique em **Tablet**e em **concluir**.  
  
##  <a name="2-update-default-names-of-the-data-source-and-dataset"></a><a name="UpdateNames"></a>2. atualizar os nomes padrão da fonte de dados e do DataSet  
  
#### <a name="to-update-the-default-name-of-the-data-source"></a>Para atualizar o nome padrão da fonte de dados  
  
1.  No painel Dados do Relatório, expanda **Fontes de Dados**.  
  
2.  Clique com o botão direito do mouse em **DataSource1** e clique em **Propriedades da Fonte de Dados**.  
  
3.  Na caixa **Nome** , digite **ExpressionsDataSource**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-update-the-default-name-of-the-dataset"></a>Para atualizar o nome padrão do conjunto de dados  
  
1.  No painel Dados do Relatório, expanda **Conjuntos de Dados**.  
  
2.  Clique com o botão direito do mouse em **DataSet1** e clique em **Propriedades do Conjunto de Dados**.  
  
3.  Na caixa **Nome** , digite **Expressions**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="3-display-first-name-initial-and-last-name"></a><a name="Concatenate"></a>3. exibir nome, inicial e sobrenome  
 Use a função **Left** e o operador **Concatenate** (**&**) em uma expressão avaliada com um nome que inclui uma inicial e um sobrenome. Você pode criar a expressão passo a passo ou ignorá-la no procedimento e copiar/colar a expressão do tutorial na caixa de diálogo **Expressão** .  
  
#### <a name="to-add-the-name-column"></a>Para adicionar a coluna Nome  
  
1.  Clique com o botão direito do mouse na coluna **StateProvince** , aponte para **Inserir Coluna**e clique em **Esquerda**.  
  
     Uma nova coluna é adicionada à esquerda da coluna **StateProvince** .  
  
2.  Clique no título da nova coluna e digite **Name**  
  
3.  Clique com o botão direito do mouse na célula de dados da coluna **Name** e clique em **Expressão**.  
  
4.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns**e clique em **Texto**.  
  
5.  Na lista **Item** , clique duas vezes em **Left**.  
  
     A função **Left** é adicionada à expressão.  
  
6.  Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
7.  Na lista **Valores** , clique duas vezes em **FirstName**.  
  
8.  Digite **, 1)**  
  
     Essa expressão extrai um caractere do valor **FirstName** , contando a partir da esquerda.  
  
9. Digite **& "" &**  
  
10. Na lista **Valores** , clique duas vezes em **LastName**.  
  
     A expressão completa é: `=Left(Fields!FirstName.Value, 1) &" "& Fields!LastName.Value`  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Clique em **Executar** para visualizar o relatório.  
  
##  <a name="4-use-images-to-display-gender"></a><a name="Gender"></a>4. usar imagens para exibir o gênero  
 Use imagens para mostrar o sexo de uma pessoa e identificar valores de sexo desconhecidos, usando uma terceira imagem. Você adicionará ao relatório três imagens ocultas e uma nova coluna para exibir as imagens. Em seguida, determine a imagem que aparece na coluna, com base no valor do campo Sexo.  
  
 Para aplicar uma cor à célula da tabela que contém a imagem quando você transforma o relatório em um relatório de barras, adicione um retângulo e, depois, adicione a imagem ao retângulo. Você precisa usar um retângulo porque pode aplicar uma cor do plano de fundo a um retângulo, mas não a uma imagem.  
  
 O tutorial usa imagens que são instaladas com o Windows, mas você pode usar quaisquer imagens disponíveis. Você usará imagens inseridas e elas não precisam ser instaladas no computador local nem no servidor de relatório.  
  
#### <a name="to-add-images-to-the-report-body"></a>Para adicionar imagens ao corpo do relatório  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Na guia **Inserir** da faixa de opções, clique em **Imagem** e no corpo do relatório, abaixo da tabela.  
  
     A caixa de diálogo **Propriedades da Imagem** será aberta.  
  
3.  Clique em **Importar** e procure C:\Users\Public\Public Pictures\Sample Pictures.  
  
4.  Clique em Penguins.JPG e em **Abrir**.  
  
     Na caixa de diálogo **Propriedades da Imagem**, clique em **Visibilidade** e na opção **Ocultar**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Repita as etapas 2 a 5, mas escolha Koala.JPG.  
  
7.  Repita as etapas 2 a 5, mas escolha Tulips.JPG.  
  
#### <a name="to-add-the-gender-column"></a>Para adicionar a coluna Sexo  
  
1.  Clique com o botão direito do mouse na coluna **Name**, aponte para **Inserir Coluna** e clique em **Direita**.  
  
     Uma nova coluna é adicionada à direita da coluna **Name**.  
  
2.  Clique no título da nova coluna e digite **Gênero**  
  
#### <a name="to-add-a-rectangle"></a>Para adicionar um retângulo  
  
-   Na guia **Inserir** da faixa de opções, clique em **Retângulo** e na célula de dados da coluna **Gênero**.  
  
     Um retângulo é adicionado à célula.  
  
#### <a name="to-add-an-image-to-the-rectangle"></a>Para adicionar uma imagem ao retângulo  
  
1.  Clique com o botão direito do mouse no retângulo, aponte para **Inserir** e clique em **Imagem**.  
  
2.  Na caixa de diálogo **Propriedades da Imagem**, clique na seta para baixo, ao lado de **Usar esta imagem**, e selecione uma das imagens adicionadas; por exemplo, Penguins.JPG.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-use-images-to-show-gender"></a>Para usar imagens para mostrar o sexo  
  
1.  Clique com o botão direito do mouse na imagem na célula de dados na coluna **Gênero** e clique em **Propriedades da Imagem**.  
  
2.  Na caixa de diálogo **Propriedades da Imagem**, clique no botão de expressão **fx** ao lado da caixa de texto **Usar esta imagem**.  
  
3.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns** e clique em **Fluxo do Programa**.  
  
4.  Na lista **Item** , clique duas vezes em **Mudar**.  
  
5.  Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
6.  Na lista **Valores** , clique duas vezes em **Gênero**.  
  
7.  Digite **="Male", "Koala",**  
  
8.  Na lista **Valores** , clique duas vezes em **Gênero**.  
  
9. Digite **="Female", "Penguins",**  
  
10. Na lista **Valores** , clique duas vezes em **Gênero**.  
  
11. Digite **="Unknown", "Tulips")**  
  
     A expressão completa é: `=Switch(Fields!Gender.Value ="Male", "Koala",Fields!Gender.Value ="Female","Penguins",Fields!Gender.Value ="Unknown","Tulips")`  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. Clique novamente em **OK** para fechar a caixa de diálogo **Propriedades da Imagem**.  
  
14. Clique em **Executar** para visualizar o relatório.  
  
##  <a name="5-look-up-countryregion-name"></a><a name="Lookup"></a>5. Pesquisar nome do CountryRegion  
 Crie o conjunto de dados CountryRegion e use a função **Lookup** para exibir o nome de um país/região, em vez do identificador do país/região.  
  
#### <a name="to-create-the-countryregion-dataset"></a>Para criar o conjunto de dados CountryRegion  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  No painel dados do relatório, clique em **novo** e, em seguida, clique em **DataSet**.  
  
3.  Clique em **Usar um conjunto de dados inserido no meu relatório**.  
  
4.  Na lista **Fonte de dados** , selecione ExpressionsDataSource.  
  
5.  Na caixa **Nome** , digite **CountryRegion**  
  
6.  Verifique se o tipo de consulta **Texto** está selecionado e clique em **Designer de Consultas**.  
  
7.  Clique em **Editar como Texto**.  
  
8.  Copie e cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT 1 AS ID, 'American Samoa' AS CountryRegion  
    UNION SELECT 2 AS CountryRegionID, 'Australia' AS CountryRegion  
    UNION SELECT 3 AS ID, 'Canada' AS CountryRegion  
    UNION SELECT 4 AS ID, 'Germany' AS CountryRegion  
    UNION SELECT 5 AS ID, 'Micronesia' AS CountryRegion  
    UNION SELECT 6 AS ID, 'France' AS CountryRegion  
    UNION SELECT 7 AS ID, 'United States' AS CountryRegion  
    UNION SELECT 8 AS ID, 'Brazil' AS CountryRegion  
    UNION SELECT 9 AS ID, 'Mexico' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Japan' AS CountryRegion  
    UNION SELECT 10 AS ID, 'Australia' AS CountryRegion  
    UNION SELECT 12 AS ID, 'United Kingdom' AS CountryRegion  
    ```  
  
9. Clique em **executar** (**!**) para executar a consulta.  
  
     Os resultados da consulta são os identificadores e nomes de país/região.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Clique novamente em **OK** para fechar a caixa de diálogo **Propriedades do Conjunto de Dados** .  
  
#### <a name="to-look-up-values-in-the-countryregion-dataset"></a>Para pesquisar valores no conjunto de dados CountryRegion  
  
1.  Clique no título da coluna **Identificação de país ou região** e exclua o texto: Identificação.  
  
2.  Clique com o botão direito do mouse na célula de dados da coluna **Country Region** e clique em **Expressão**.  
  
3.  Exclua a expressão, exceto o sinal de igual (=) inicial.  
  
     A expressão restante é: `=`  
  
4.  Na caixa de diálogo **Expressão**, expanda **Funções Comuns** e clique em **Diversos**.  
  
5.  Na lista **Item**, clique duas vezes em **Pesquisar**.  
  
6.  Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
7.  Na lista **valores** , clique duas vezes em `CountryRegionID`.  
  
8.  Se o cursor não estiver logo após `CountryRegionID.Value`, posicione-o lá.  
  
9. Exclua o parêntese à direita e digite **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")**  
  
     A expressão completa é: `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
     A sintaxe da função **Lookup** especifica uma pesquisa entre CountryRegionID e ID no conjunto de dados CountryRegion que retorna o valor CountryRegion, que também se encontra no conjunto de dados CountryRegion.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Clique em **Executar** para visualizar o relatório.  
  
##  <a name="6-count-days-since-last-purchase"></a><a name="Count"></a>6. contagem de dias desde a última compra  
 Adicione uma coluna e, em seguida **Now** , use a função `ExecutionTime` Now ou a variável global interna para calcular o número de dias a partir de hoje desde a última compra de uma pessoa.  
  
#### <a name="to-add-the-days-ago-column"></a>Para adicionar a coluna Days Ago  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique com o botão direito do mouse na coluna **Last Purchase** , aponte para **Inserir Coluna**e clique em **Direita**.  
  
     Uma nova coluna é adicionada à direita da coluna **Last Purchase** .  
  
3.  No cabeçalho de coluna, digite **Dias Atrás**  
  
4.  Clique com o botão direito do mouse na célula de dados da coluna **Dias Atrás** e clique em **Expressão**.  
  
5.  Na caixa de diálogo **Expressão**, expanda **Funções Comuns** e clique em **Data e Hora**.  
  
6.  Na lista **Item** , clique duas vezes em **DateDiff**.  
  
7.  Se o cursor não estiver logo após `DateDiff(`, posicione-o lá.  
  
8.  Digite **"d",**  
  
9. Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
10. Na lista **Valores**, clique duas vezes em **LastPurchase**.  
  
11. Se o cursor não estiver logo após `Fields!LastPurchase.Value`, posicione-o lá.  
  
12. Tipo **,**  
  
13. Na lista **Categoria**, clique em **Data e Hora** novamente.  
  
14. Na lista **Item**, clique duas vezes em **Agora**.  
  
    > [!WARNING]  
    >  Em relatórios de produção, não use a função **Now** em expressões que são avaliadas diversas vezes como os renderizadores de relatório (por exemplo, nas linhas de detalhes de um relatório). O valor de **Now** muda de acordo com a linha e valores diferentes afetam os resultados de avaliação de expressões, o que leva a resultados um pouco inconsistentes. Procure utilizar a variável global `ExecutionTime` fornecida por [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
15. Se o cursor não estiver logo após `Now(`, posicione-o lá.  
  
16. Exclua o parêntese à esquerda e digite **)**  
  
     A expressão completa é: `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="7-use-an-indicator-to-show-sales-comparison"></a><a name="Indicator"></a>7. Use um indicador para mostrar a comparação de vendas  
 Adicione uma nova coluna e use um indicador para mostrar se as compras ACUMULAdas no ano de uma pessoa (no ano) estão acima ou abaixo das compras médias no ano. A função **Round** remove os decimais dos valores.  
  
 A configuração do indicador e seus estados exige várias etapas. Se desejar, no procedimento "para configurar o indicador", você poderá ignorar e copiar/colar as expressões concluídas deste tutorial na caixa de diálogo **expressão** .  
  
#### <a name="to-add-the--or---avg-sales-column"></a>Para adicionar a coluna + ou - AVG Sales  
  
1.  Clique com o botão direito do mouse na coluna **YTD Purchase** , aponte para **Inserir Coluna**e clique em **Direita**.  
  
     Uma nova coluna é adicionada à direita da coluna **YTD Purchase** .  
  
2.  Clique no título da coluna e digite **+ or - AVG Sales**  
  
#### <a name="to-add-an-indicator"></a>Para adicionar um indicador  
  
1.  Na guia **Inserir** da faixa de opções, clique em **Indicador** e na célula de dados da coluna **+ or - AVG Sales**.  
  
     A caixa de diálogo **Selecionar Tipo de Indicador** será aberta.  
  
2.  No grupo **Direcional** dos conjuntos de ícones, clique no conjunto de três setas cinza.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-configure-the-indicator"></a>Para configurar o indicador  
  
1.  Clique com o botão direito do mouse no indicador, clique em **Propriedades do Indicador**e em **Valores e Estados**.  
  
2.  Clique no botão de expressão **fx** ao lado da caixa de texto **Valor** .  
  
3.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns**e clique em **Matemática**.  
  
4.  Na lista **Item** , clique duas vezes em **Arredondar**.  
  
5.  Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
6.  Na lista **Valores**, clique duas vezes em **YTDPurchase**.  
  
7.  Se o cursor não estiver logo após `Fields!YTDPurchase.Value`, posicione-o lá.  
  
8.  Escreva**-**  
  
9. Expanda novamente **Funções Comuns** e clique em **Agregação**.  
  
10. Na lista **Item**, clique duas vezes em **Média**.  
  
11. Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
12. Na lista **Valores**, clique duas vezes em **YTDPurchase**.  
  
13. Se o cursor não estiver logo após `Fields!YTDPurchase.Value`, posicione-o lá.  
  
14. Digite **, "Expressions"))**  
  
     A expressão completa é: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. Na caixa **Unidade de Medida dos Estados** , selecione **Numérica**.  
  
17. Na linha com a seta apontando para baixo, clique no botão **fx** à direita da caixa de texto do valor **Start** .  
  
18. Na caixa de diálogo **Expressão** , expanda **Funções Comuns**e clique em **Matemática**.  
  
19. Na lista **Item** , clique duas vezes em **Arredondar**.  
  
20. Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
21. Na lista **Valores**, clique duas vezes em **YTDPurchase**.  
  
22. Se o cursor não estiver logo após `Fields!YTDPurchase.Value`, posicione-o lá.  
  
23. Escreva**-**  
  
24. Expanda novamente **Funções Comuns** e clique em **Agregação**.  
  
25. Na lista **Item**, clique duas vezes em **Média**.  
  
26. Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
27. Na lista **Valores**, clique duas vezes em **YTDPurchase**.  
  
28. Se o cursor não estiver logo após `Fields!YTDPurchase.Value`, posicione-o lá.  
  
29. Digite **, "Expressions")) < 0**  
  
     A expressão completa é: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. Na caixa de texto do valor **End** , digite **0**  
  
32. Clique na linha com a seta apontando para a horizontal e clique em **Excluir**.  
  
33. Na linha com a seta apontando para cima, na caixa **Iniciar** , digite **0**  
  
34. Clique no botão **fx** à direita da caixa de texto do valor **End** .  
  
35. Na caixa de diálogo **expressão** , crie a expressão:`=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. Clique novamente em **OK** para fechar a caixa de diálogo **Propriedades do indicador** .  
  
38. Clique em **Executar** para visualizar o relatório.  
  
##  <a name="8-make-the-report-a-green-bar-report"></a><a name="GreenBar"></a>8. tornar o relatório um relatório de "barra verde"  
 Use um parâmetro para especificar a cor a ser aplicada para alternar linhas no relatório, transformando-o em um relatório de barras.  
  
#### <a name="to-add-a-parameter"></a>Para adicionar um parâmetro  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  No painel **Dados do Relatório** , clique com o botão direito do mouse em **Parâmetros** e clique em **Adicionar Parâmetro**.  
  
     A caixa de diálogo **Propriedades do Parâmetro do Relatório** é aberta.  
  
3.  Em **Prompt**, digite **Escolher cor**  
  
4.  Em **Nome**, digite **RowColor**  
  
5.  No painel esquerdo, clique em **Valores Disponíveis**.  
  
6.  Clique em **Especificar valores**.  
  
7.  Clique em **Adicionar**.  
  
8.  Na caixa **rótulo** , digite: **amarelo**  
  
9. Na caixa **Valor** , digite **Amarelo**  
  
10. Clique em **Adicionar**.  
  
11. Na caixa **Rótulo** , digite **Verde**  
  
12. Na caixa **Valor** , digite **PaleGreen**  
  
13. Clique em **Adicionar**.  
  
14. Na caixa **Rótulo** , digite **Azul**  
  
15. Na caixa **Valor** , digite **LightBlue**  
  
16. Clique em **Adicionar**.  
  
17. Na caixa **Rótulo** , digite **Rosa**  
  
18. Na caixa **Valor** , digite **Rosa**  
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-apply-alternating-colors-to-detail-rows"></a>Para aplicar cores alternativas a linhas de detalhes  
  
1.  Clique na guia **Exibir** na faixa de opções e verifique se **Propriedades** está selecionado.  
  
2.  Clique na célula de dados da coluna **Name** e pressione a tecla Shift.  
  
3.  Uma a uma, clique nas outras células na linha.  
  
4.  No painel Propriedades, clique em **BackgroundColor**.  
  
     Se o painel Propriedades listar propriedades por categoria, você encontrará **BackgroundColor** na categoria **Preenchimento**.  
  
5.  Clique na seta para baixo e em **Expressão**.  
  
6.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns**e clique em **Fluxo do Programa**.  
  
7.  Na lista **Item** , clique duas vezes em **IIf**.  
  
8.  Expanda **Funções Comuns** e clique em **Agregação**.  
  
9. Na lista **Item**, clique duas vezes em **RunningValue**.  
  
10. Na lista **Categoria** , clique em **Campos (Expressões)**.  
  
11. Na lista **Valores** , clique duas vezes em **FirstName**.  
  
12. Se o cursor não estiver logo após `Fields!FirstName.Value`, coloque-o nesse local e digite **,**  
  
13. Expanda **Funções Comuns** e clique em **Agregação**.  
  
14. Na lista **Item**, clique duas vezes em **Contagem**.  
  
15. Se o cursor não estiver logo após `Count(`, posicione-o lá.  
  
16. Exclua o parêntese esquerdo e, em seguida **, digite "expressões")**  
  
    > [!NOTE]  
    >  Expressions é o nome do conjunto de dados no qual as linhas de dados serão contadas.  
  
17. Expanda **Operadores** e clique em **Aritmético**.  
  
18. Na lista **Item**, clique duas vezes em **Mod**.  
  
19. Se o cursor não estiver logo após `Mod`, posicione-o lá.  
  
20. Digite **2 =0,**  
  
    > [!IMPORTANT]  
    >  Inclua um espaço antes de digitar o número 2.  
  
21. Clique em **Parâmetros** e, na lista **Valores** , clique duas vezes em **RowColor**.  
  
22. Se o cursor não estiver logo após `Parameters!RowColor.Value`, posicione-o lá.  
  
23. Digite **, "White")**  
  
     A expressão completa é: `=IIf(RunningValue(Fields!FirstName.Value,Count, "Expressions") Mod 2 =0, Parameters!RowColor.Value, "White")`  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="run-the-report"></a>Executar o relatório  
  
1.  Se não estiver na guia **Início**, clique em **Início** para retornar ao modo Design.  
  
2.  Clique em **Executar**.  
  
3.  Na lista suspensa **Escolher cor**, selecione a cor das barras que não são brancas no relatório.  
  
4.  Clique em **Exibir Relatório**.  
  
     O relatório é renderizado e linhas alternativas têm o plano de fundo escolhido por você.  
  
##  <a name="optional-format-date-column"></a><a name="DateFormat"></a>adicional Formatar coluna de data  
 Formate a coluna **Last Purchase**, que contém datas.  
  
#### <a name="to-format-date-column"></a>Para formatar coluna de dados  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique com o botão direito do mouse na célula de dados da coluna **Last Purchase** e clique em **Propriedades de Caixa de Texto**.  
  
3.  Na caixa de diálogo **Propriedades da Caixa de Texto**, clique em **Número**, em **Data** e no tipo **\*1/31/2000**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="optional-add-a-report-title"></a><a name="Title"></a>adicional Adicionar um título de relatório  
 Adicione um título ao relatório.  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Resumo de Comparação de Vendas** e clique fora da caixa de texto.  
  
3.  Clique com o botão direito do mouse na caixa de texto que contém **Resumo de Comparação de Vendas** e clique em **Propriedades da Caixa de Texto**.  
  
4.  Na caixa de diálogo **Propriedades da Caixa de Texto** , clique em **Fonte**.  
  
5.  Na lista **Tamanho** , selecione **18pt**.  
  
6.  Na lista **Cor**, selecione **Cinza**.  
  
7.  Selecione **Negrito** e **Itálico**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="optional-save-the-report"></a><a name="Save"></a>adicional Salvar o relatório  
 É possível salvar relatórios em um servidor de relatório, em uma biblioteca do SharePoint ou no computador. Para obter mais informações, consulte [Salvando relatórios &#40;Construtor de Relatórios&#41;](report-builder/saving-reports-report-builder.md).  
  
 Neste tutorial, salve o relatório em um servidor de relatório. Se você não tiver acesso ao servidor de relatório, salve o relatório no computador.  
  
#### <a name="to-save-the-report-to-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
     A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for estabelecida, você verá o conteúdo da pasta de relatório que o administrador do servidor de relatório especificou como o local de relatório padrão.  
  
4.  Em **Nome**, substitua o nome padrão por **Resumo de Comparação de Vendas**.  
  
5.  Clique em **Salvar**.  
  
 O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
#### <a name="to-save-the-report-to-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu Computador**e, em seguida, navegue até a pasta na qual você deseja salvar o relatório.  
  
3.  Em **Nome**, substitua o nome padrão por **Resumo de Comparação de Vendas**.  
  
4.  Clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md)   
 [Imagens, caixas de texto, retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](report-design/rectangles-and-lines-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
