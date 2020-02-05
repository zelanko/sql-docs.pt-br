---
title: 'Tutorial: Apresentação de expressões | Microsoft Docs'
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 2d05ef4c-5f91-48b2-8795-f0a201a0b3cc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7a26065cc1d65e5c187123ead990888aa4de0e60
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63295894"
---
# <a name="tutorial-introducing-expressions"></a>Tutorial: Apresentando expressões
Neste tutorial do [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] , você usa expressões com funções e operadores comuns para criar relatórios paginados do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] avançados e flexíveis. 

Você escreverá expressões que concatenam valores de nome, pesquisará valores em um conjunto de dados separado, exibirá diferentes cores com base em valores de campo e assim por diante.  
  
O relatório é um relatório em tiras com cores de linhas alternadas em branco e uma cor. O relatório inclui um parâmetro para selecionar a cor das linhas que não são brancas.  
  
A ilustração mostra um relatório semelhante ao que você criará.  
  
![report-builder-expression-tutorial-in-browser](../reporting-services/media/report-builder-expression-tutorial-in-browser.png) 
  
Tempo estimado para concluir este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Setup"></a>1. Criar um relatório de tabela e conjunto de dados no Assistente de Tabela ou Matriz  
Nesta seção, você cria um relatório de tabela, uma fonte de dados e um conjunto de dados. Ao criar o layout da tabela, você incluirá apenas alguns campos. Depois de concluir o assistente, você adicionará manualmente colunas. O assistente facilita a criação do layout da tabela.  
  
> [!NOTE]  
> Neste tutorial, a consulta contém os valores de dados e, portanto, ela não precisa de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
### <a name="to-create-a-table-report"></a>Para criar um relatório de tabela  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Tabela ou Matriz**.  
  
4.  Na página **Escolher um conjunto de dados** , clique em **Criar um conjunto de dados** > **Avançar**.  
  
6.  Na página **Escolher uma conexão com uma fonte de dados** , selecione uma fonte de dados do tipo **SQL Server**. Selecione uma fonte de dados na lista ou navegue até o servidor de relatório para selecionar uma.  

    > [!NOTE]  
    > A fonte de dados escolhida não tem importância, desde que você tenha as permissões adequadas. Você não obterá dados da fonte de dados. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
7.  Clique em **Próximo**.  
  
8.  Na página **Crie uma consulta** , clique em **Editar como Texto**.  
  
9. Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT 'Lauren' AS FirstName,'Johnson' AS LastName, 'American Samoa' AS StateProvince, 1 AS CountryRegionID,'Female' AS Gender, CAST(9996.60 AS money) AS YTDPurchase, CAST('2015-6-10' AS date) AS LastPurchase  
    UNION SELECT'Warren' AS FirstName, 'Pal' AS LastName, 'New South Wales' AS StateProvince, 2 AS CountryRegionID, 'Male' AS Gender, CAST(5747.25 AS money) AS YTDPurchase, CAST('2015-7-3' AS date) AS LastPurchase  
    UNION SELECT 'Fernando' AS FirstName, 'Ross' AS LastName, 'Alberta' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(9248.15 AS money) AS YTDPurchase, CAST('2015-10-17' AS date) AS LastPurchase  
    UNION SELECT 'Rob' AS FirstName, 'Caron' AS LastName, 'Northwest Territories' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(742.50 AS money) AS YTDPurchase, CAST('2015-4-29' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Bailey' AS LastName, 'British Columbia' AS StateProvince, 3 AS CountryRegionID, 'Male' AS Gender, CAST(1147.50 AS money) AS YTDPurchase, CAST('2015-6-15' AS date) AS LastPurchase  
    UNION SELECT  'Bridget' AS FirstName, 'She' AS LastName, 'Hamburg' AS StateProvince, 4 AS CountryRegionID, 'Female' AS Gender, CAST(7497.30 AS money) AS YTDPurchase, CAST('2015-5-10' AS date) AS LastPurchase  
    UNION SELECT 'Alexander' AS FirstName, 'Martin' AS LastName, 'Saxony' AS StateProvince, 4 AS CountryRegionID, 'Male' AS Gender, CAST(2997.60 AS money) AS YTDPurchase, CAST('2015-11-19' AS date) AS LastPurchase  
    UNION SELECT 'Yolanda' AS FirstName, 'Sharma' AS LastName ,'Micronesia' AS StateProvince, 5 AS CountryRegionID, 'Female' AS Gender, CAST(3247.95 AS money) AS YTDPurchase, CAST('2015-8-23' AS date) AS LastPurchase  
    UNION SELECT 'Marc' AS FirstName, 'Zimmerman' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1200.00 AS money) AS YTDPurchase, CAST('2015-11-16' AS date) AS LastPurchase  
    UNION SELECT 'Katherine' AS FirstName, 'Abel' AS LastName, 'Moselle' AS StateProvince, 6 AS CountryRegionID, 'Female' AS Gender, CAST(2025.00 AS money) AS YTDPurchase, CAST('2015-12-1' AS date) AS LastPurchase  
    UNION SELECT 'Nicolas' as FirstName, 'Anand' AS LastName, 'Seine (Paris)' AS StateProvince, 6 AS CountryRegionID, 'Male' AS Gender, CAST(1425.00 AS money) AS YTDPurchase, CAST('2015-12-11' AS date) AS LastPurchase  
    UNION SELECT 'James' AS FirstName, 'Peters' AS LastName, 'England' AS StateProvince, 12 AS CountryRegionID, 'Male' AS Gender, CAST(887.50 AS money) AS YTDPurchase, CAST('2015-8-15' AS date) AS LastPurchase  
    UNION SELECT 'Alison' AS FirstName, 'Nath' AS LastName, 'Alaska' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(607.50 AS money) AS YTDPurchase, CAST('2015-10-13' AS date) AS LastPurchase  
    UNION SELECT 'Grace' AS FirstName, 'Patterson' AS LastName, 'Kansas' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(1215.00 AS money) AS YTDPurchase, CAST('2015-10-18' AS date) AS LastPurchase  
    UNION SELECT 'Bobby' AS FirstName, 'Sanchez' AS LastName, 'North Dakota' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(6191.00 AS money) AS YTDPurchase, CAST('2015-9-17' AS date) AS LastPurchase  
    UNION SELECT 'Charles' AS FirstName, 'Reed' AS LastName, 'Nebraska' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8772.00 AS money) AS YTDPurchase, CAST('2015-8-27' AS date) AS LastPurchase  
    UNION SELECT 'Orlando' AS FirstName, 'Romeo' AS LastName, 'Texas' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(8578.00 AS money) AS YTDPurchase, CAST('2015-7-29' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    UNION SELECT 'Cynthia' AS FirstName, 'Randall' AS LastName, 'Utah' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(7218.10 AS money) AS YTDPurchase, CAST('2015-1-11' AS date) AS LastPurchase  
    UNION SELECT 'Rebecca' AS FirstName, 'Roberts' AS LastName, 'Washington' AS StateProvince, 7 AS CountryRegionID, 'Female' AS Gender, CAST(8357.80 AS money) AS YTDPurchase, CAST('2015-10-28' AS date) AS LastPurchase  
    UNION SELECT 'Cristian' AS FirstName, 'Petulescu' AS LastName, 'Wisconsin' AS StateProvince, 7 AS CountryRegionID, 'Male' AS Gender, CAST(3470.00 AS money) AS YTDPurchase, CAST('2015-11-30' AS date) AS LastPurchase  
    ```  

  
10. Na barra de ferramentas do designer de consultas, clique em **Executar** ( **!** ). O conjunto de resultados exibe 23 linhas de dados e nas seguintes colunas: FirstName, LastName, StateProvince, CountryRegionID, Gender, YTDPurchase e LastPurchase.  

    ![report-builder-expression-tutorial-query-as-text](../reporting-services/media/report-builder-expression-tutorial-query-as-text.png)
  
11. Clique em **Próximo**.  
  
12. Na página **Organizar campos** , arraste os campos a seguir, na ordem especificada, da lista **Campos Disponíveis** para a lista **Valores** .  
  
    -   StateProvince   
    -   CountryRegionID  
    -   LastPurchase  
    -   YTDPurchase  
  
    Como CountryRegionID e YTDPurchase contêm dados numéricos, a agregação SUM é aplicada a eles por padrão, mas você não quer que eles sejam somas.  
   
13. Na lista **Valores** , clique com o botão direito do mouse em **CountryRegionID** e desmarque a caixa de seleção **Sum** .  
  
    A Soma não é mais aplicada a CountryRegionID.  
  
14. Na lista **Valores** , clique com o botão direito do mouse em **YTDPurchase** e clique na opção **Soma** .  
  
    A Soma não é mais aplicada a YTDPurchase.  
    
    ![report-builder-expression-not-sum](../reporting-services/media/report-builder-expression-not-sum.png)
  
15. Clique em **Próximo**.  
  
16. Na página **Escolha um layout** , mantenha todas as configurações padrão e clique em **Avançar**.  

    ![report-builder-expression-tutorial-choose-layout](../reporting-services/media/report-builder-expression-tutorial-choose-layout.png)
  
17. Clique em **Concluir**.  
  
## <a name="UpdateNames"></a>2. Atualizar nomes padrão da fonte de dados ou do conjunto de dados  
  
### <a name="to-update-the-default-name-of-the-data-source"></a>Para atualizar o nome padrão da fonte de dados  
  
1.  No painel Dados do Relatório, expanda a pasta **Fontes de Dados** .  
  
2.  Clique com o botão direito do mouse em **DataSource1** e clique em **Propriedades da Fonte de Dados**.  
  
3.  Na caixa **Nome** , digite **ExpressionsDataSource**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-update-the-default-name-of-the-dataset"></a>Para atualizar o nome padrão do conjunto de dados  
  
1.  No painel Dados do Relatório, expanda a pasta **Conjuntos de Dados** .  
  
2.  Clique com o botão direito do mouse em **DataSet1** e clique em **Propriedades do Conjunto de Dados**.  

    ![report-builder-expression-tutorial-rename-dataset](../reporting-services/media/report-builder-expression-tutorial-rename-dataset.png)
  
3.  Na caixa **Nome** , digite **Expressions**  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Concatenate"></a>3. Exibir nome, inicial e sobrenome  
Nesta seção, use a função **Left** e o operador **Concatenate** ( **&** ) em uma expressão avaliada com um nome que inclui uma inicial e um sobrenome. Você pode criar a expressão passo a passo ou ignorá-la no procedimento e copiar/colar a expressão do tutorial na caixa de diálogo **Expressão** .   
  
1.  Clique com o botão direito do mouse na coluna **StateProvince** , aponte para **Inserir Coluna**e clique em **Esquerda**.  
  
    Uma nova coluna é adicionada à esquerda da coluna **StateProvince** . 
    
    ![report-builder-expression-tutorial-insert-column](../reporting-services/media/report-builder-expression-tutorial-insert-column.png) 
  
2.  Clique no cabeçalho da nova coluna e digite **Name**.  
  
3.  Clique com o botão direito do mouse na célula de dados da coluna **Name** e clique em **Expressão**.  

    ![report-builder-expression-tutorial-insert-expression](../reporting-services/media/report-builder-expression-tutorial-insert-expression.png)
  
4.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns**e clique em **Texto**.  
  
5.  Na lista **Item** , clique duas vezes em **Left**.  
  
    A função **Left** é adicionada à expressão.  
    
    ![report-builder-expression-tutorial-left-function](../reporting-services/media/report-builder-expression-tutorial-left-function.png)
  
6.  Na lista **Categoria** , clique em **Campos (Expressões)** .  
  
7.  Na lista **Valores** , clique duas vezes em **FirstName**.  
  
8.  Digite **, 1)**  
  
    Essa expressão extrai um caractere do valor **FirstName** , contando a partir da esquerda.  
  
9. Digite **&". "&**  

    Isso adiciona um ponto e um espaço depois da expressão.
  
10. Na lista **Valores** , clique duas vezes em **LastName**.  
  
    A expressão completa é: `=Left(Fields!FirstName.Value, 1) &". "& Fields!LastName.Value`  
    
    ![report-builder-expression-tutorial-complete-name-expression](../reporting-services/media/report-builder-expression-tutorial-complete-name-expression.png)
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Clique em **Executar** para visualizar o relatório.  

## <a name="DateFormat"></a>(opcional) Formatar as colunas de data e moeda e a linha de cabeçalho  
Nesta seção, você formata a coluna **Last Purchase** , que contém datas, e a coluna YTDPurchase, que contém a moeda. Você também formata a linha de cabeçalho.  
  
### <a name="to-format-the-date-column"></a>Para formatar coluna de data  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Selecione a célula de dados na coluna **Última Compra** e, na guia **Início** > seção **Número**, selecione **Data**.  

    ![report-builder-expression-tutorial-date-format](../reporting-services/media/report-builder-expression-tutorial-date-format.png)
  
3.  Também na seção **Número** , clique na seta ao lado de **Placeholder Styles** e selecione **Valores de Exemplo**. 

    ![report-builder-expression-tutorial-sample-values](../reporting-services/media/report-builder-expression-tutorial-sample-values.png)

    Agora, você pode ver um exemplo da formatação que selecionou. 
  
### <a name="to-format-the-currency-column"></a>Para formatar a coluna de moeda

- Selecione a célula de dados na coluna **YTDPurchase** e, na seção **Número** , selecione **Símbolo de Moeda**.
 
### <a name="to-format-the-column-headers"></a>Para formatar os cabeçalhos de coluna

1. Selecione a linha de cabeçalhos de coluna.

2. Na guia **Início** > seção **Parágrafo**, selecione **Esquerda**. 

    ![report-builder-expression-tutorial-format-headings](../reporting-services/media/report-builder-expression-tutorial-format-headings.png)

3. Clique em **Executar** para visualizar o relatório. 

Este é o relatório até o momento, com datas, moeda e cabeçalhos de coluna formatados.

![report-builder-expression-tutorial-preview-formatted](../reporting-services/media/report-builder-expression-tutorial-preview-formatted.png)

  
## <a name="Gender"></a>4. Usar cor para indicar o sexo  
Nesta seção, você adiciona cor para indicar o sexo de uma pessoa. Você adicionará uma nova coluna para exibir a cor e determinará a cor que aparece na coluna, com base no valor do campo Gender.  
  
Para manter a cor que você aplicou à célula da tabela quando fez o relatório em tiras, você adiciona um retângulo e adiciona a cor da tela de fundo ao retângulo.  
    
 
### <a name="to-add-an-mf-column"></a>Para adicionar uma coluna M/F  
  
1.  Clique com o botão direito do mouse na coluna **Name** , aponte para **Inserir Coluna**e clique em **Esquerda**.  
  
    Uma nova coluna é adicionada à esquerda da coluna **Name** .  
  
2.  Clique no cabeçalho da nova coluna e digite **M/F**.  
  
### <a name="to-add-a-rectangle"></a>Para adicionar um retângulo  
  
1.   Na guia **Inserir** , clique em **Retângulo** e clique na célula de dados da coluna **M/F** .  
  
     Um retângulo é adicionado à célula.  
     
     ![report-builder-expression-tutorial-insert-rectangle](../reporting-services/media/report-builder-expression-tutorial-insert-rectangle.png)
  
2. Arraste o divisor de coluna entre **M/F** e **Name** para deixar a coluna **M/F** mais estreita.

    ![report-builder-expression-tutorial-narrow-column](../reporting-services/media/report-builder-expression-tutorial-narrow-column.png)
  
### <a name="to-use-color-to-show-gender"></a>Para usar cor para indicar o sexo  
  
1.  Clique com o botão direito do mouse no retângulo na célula de dados na coluna **M/F** e clique em **Propriedades do Retângulo**.  
  
2.  Na caixa de diálogo **Propriedades do Retângulo** > guia **Preencher**, clique no botão de expressão **fx** ao lado de **Cor de Preenchimento**.  
  
3.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns** e clique em **Fluxo do Programa**.  
  
4.  Na lista **Item** , clique duas vezes em **Mudar**.  
  
5.  Na lista **Categoria** , clique em **Campos (Expressões)** .  
  
6.  Na lista **Valores** , clique duas vezes em **Gênero**.  
  
7.  Tipo **="Masculino",** (incluindo a vírgula).

8. Na lista **Categoria** , clique em **Constantes**e, na caixa **Valores** , clique em **Azul cobalto**.

    ![report-builder-expression-tutorial-color-expression-cornflower-blue](../reporting-services/media/report-builder-expression-tutorial-color-expression-cornflower-blue.png)

9. Digite uma vírgula depois dela. 
  
5.  Na lista **Categoria** , clique em **Campos (Expressões)** e, na lista **Valores** , clique duas vezes em **Sexo** novamente.  
  
7.  Tipo **="Feminino",** (incluindo a vírgula). 

8. Na lista **Categoria** , clique em **Constantes**e, na caixa **Valores** , clique em **Tomate**.

13. Digite um parêntese de fechamento **)** depois dela. 
  
    A expressão completa é: `=Switch(Fields!Gender.Value ="Male", "CornflowerBlue",Fields!Gender.Value ="Female","Tomato")`  
    
    ![report-builder-expression-tutorial-color-expression-complete](../reporting-services/media/report-builder-expression-tutorial-color-expression-complete.png)
  
12. Clique em **OK**e depois clique em **OK** novamente para fechar a caixa de diálogo **Propriedades do Retângulo** .  
  
14. Clique em **Executar** para visualizar o relatório.  

    ![report-builder-expression-tutorial-preview-m-f-column](../reporting-services/media/report-builder-expression-tutorial-preview-m-f-column.png)

### <a name="to-format-the-color-rectangles"></a>Para formatar os retângulos de cores

1. Clique em **Design** para retornar à exibição de design.  

16. Selecione o retângulo na coluna **M/F** . No painel Propriedades, na seção Borda, defina estas propriedades:

    - BorderColor = Branco
    - BorderStyle = Sólido
    - BorderWidth = 5pt
    
    ![report-builder-expression-tutorial-format-m-f-column](../reporting-services/media/report-builder-expression-tutorial-format-m-f-column.png)

18. Clique em **Executar** para visualizar o relatório novamente. Desta vez, os blocos de cor têm espaço em branco em torno deles.

    ![report-builder-expression-tutorial-preview-formatted-m-f-column](../reporting-services/media/report-builder-expression-tutorial-preview-formatted-m-f-column.png)  
  
## <a name="Lookup"></a>5. Pesquisar o nome de CountryRegion  
Nesta seção, você cria o conjunto de dados CountryRegion e usa a função **Lookup** para exibir o nome de um país/região, em vez do identificador do país/região.  
  
### <a name="to-create-the-countryregion-dataset"></a>Para criar o conjunto de dados CountryRegion  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  No painel Dados do Relatório, clique em **Novo** e em **Conjunto de Dados**.  
  
3.  Em **Propriedades do Conjunto de Dados, clique em **Usar um conjunto de dados inserido em meu relatório**.  
  
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
  
9. Clique em **Executar** ( **!** ) para executar a consulta.  
  
    Os resultados da consulta são os identificadores e nomes de país/região.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Clique novamente em **OK** para fechar a caixa de diálogo **Propriedades do Conjunto de Dados** .  

     Agora, você tem um segundo conjunto de dados na coluna **Dados do Relatório** .
  
### <a name="to-look-up-values-in-the-countryregion-dataset"></a>Para pesquisar valores no conjunto de dados CountryRegion  
  
1.  Clique no cabeçalho da coluna **Country Region ID** e exclua o texto: **ID**, de modo que ele se torna **Country Region**.  
  
2.  Clique com o botão direito do mouse na célula de dados da coluna **Country Region** e clique em **Expressão**.  
  
3.  Exclua a expressão, exceto o sinal de igual (=) inicial.  
  
    A expressão restante é: `=`  
  
4.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns** e clique em **Diversos**e, na lista **Item** , clique duas vezes em **Lookup**.  
  
6.  Na lista **Categoria** , clique em **Campos (Expressões)** e, na lista **Valores** , clique duas vezes em **CountryRegionID**.  
  
8.  Posicione o cursor imediatamente após `CountryRegionID.Value`e digite **,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")**  
  
    A expressão completa é: `=Lookup(Fields!CountryRegionID.Value,Fields!ID.value, Fields!CountryRegion.value, "CountryRegion")`  
  
    A sintaxe da função **Lookup** especifica uma pesquisa entre CountryRegionID no conjunto de dados de Expressão e ID no conjunto de dados CountryRegion que retorna o valor CountryRegion do conjunto de dados CountryRegion.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Clique em **Executar** para visualizar o relatório.  
  
## <a name="Count"></a>6. Contar dias desde a última compra  
Nesta seção, você adiciona uma coluna e usa a função **Now** ou a variável global interna `ExecutionTime` para calcular o número de dias desde a data das últimas compras de um cliente até hoje.  
  
### <a name="to-add-the-days-ago-column"></a>Para adicionar a coluna Days Ago  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique com o botão direito do mouse na coluna **Last Purchase** , aponte para **Inserir Coluna**e clique em **Direita**.  
  
    Uma nova coluna é adicionada à direita da coluna **Last Purchase** .  
  
3.  No cabeçalho de coluna, digite **Dias Atrás**  
  
4.  Clique com o botão direito do mouse na célula de dados da coluna **Dias Atrás** e clique em **Expressão**.  
  
5.  Na caixa de diálogo **Expressão**, expanda **Funções Comuns** e clique em **Data e Hora**.  
  
6.  Na lista **Item** , clique duas vezes em **DateDiff**.  
  
7.  Imediatamente após `DateDiff(`, digite **"d",** (incluindo as aspas "" e a vírgula). 
  
9. Na lista **Categoria** , clique em **Campos (Expressões)** e, na lista **Valores** , clique duas vezes em **LastPurchase**.  
  
11. Imediatamente após `Fields!LastPurchase.Value`, digite **,** (uma vírgula). 
  
13. Na lista **Categoria**, clique novamente em **Data e Hora** e, na lista **Item**, clique duas vezes em **Agora**.  
  
    > [!WARNING]  
    > Em relatórios de produção, não use a função **Now** em expressões que são avaliadas diversas vezes como os renderizadores de relatório (por exemplo, nas linhas de detalhes de um relatório). O valor de **Now** muda de acordo com a linha e valores diferentes afetam os resultados de avaliação de expressões, o que leva a resultados um pouco inconsistentes. Em vez disso, use a variável global `ExecutionTime` fornecida por [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
15. Exclua o parêntese esquerdo após `Now(`e digite um parêntese direito **)**  
  
    A expressão completa é: `=DateDiff("d", Fields!LastPurchase.Value, Now)`  
    
    ![report-builder-expression-tutorial-date-since-last-purchase](../reporting-services/media/report-builder-expression-tutorial-date-since-last-purchase.png)
  
17. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

11. Clique em **Executar** para visualizar o relatório.  
  
## <a name="Indicator"></a>7. Usar um indicador para mostrar comparação de vendas  
Nesta seção, você adiciona uma nova coluna e use um indicador para mostrar se as compras de uma pessoa YTD (desde o início do ano) estão acima ou abaixo da média de compras YTD. A função **Round** remove os decimais dos valores.  
  
Configurar o indicador e seus estados envolve várias etapas. Se desejar, você poderá passar para o procedimento "Para configurar o indicador" e copiar/colar as expressões completas deste tutorial na caixa de diálogo **Expressão**.  
  
### <a name="to-add-the--or---avg-sales-column"></a>Para adicionar a coluna + ou - AVG Sales  
  
1.  Clique com o botão direito do mouse na coluna **YTD Purchase** , aponte para **Inserir Coluna**e clique em **Direita**.  
  
    Uma nova coluna é adicionada à direita da coluna **YTD Purchase** .  
  
2.  Clique no cabeçalho da coluna e digite **+ or - AVG Sales**  
  
### <a name="to-add-an-indicator"></a>Para adicionar um indicador  
  
1.  Na guia **Inserir** , clique em **Indicador**e clique na célula de dados da coluna **+ or - AVG Sales** .  
  
    A caixa de diálogo **Selecionar Tipo de Indicador** será aberta.  
  
2.  No grupo **Direcional** dos conjuntos de ícones, clique no conjunto de três setas cinza.  

    ![report-builder-expression-tutorial-select-indicator](../reporting-services/media/report-builder-expression-tutorial-select-indicator.png)
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-configure-the-indicator"></a>Para configurar o indicador  
  
1.  Clique com o botão direito do mouse no indicador, clique em **Propriedades do Indicador**e em **Valores e Estados**.  
  
2.  Clique no botão de expressão **fx** ao lado da caixa de texto **Valor** .  
  
3.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns**e clique em **Matemática**.  
  
4.  Na lista **Item** , clique duas vezes em **Arredondar**.  
  
5.  Na lista **Categoria** , clique em **Campos (Expressões)** e, na lista **Valores** , clique duas vezes em **YTDPurchase**novamente.  
  
7.  Imediatamente após `Fields!YTDPurchase.Value`, digite  **-** (um sinal de subtração). 
  
9. Expanda **Funções Comuns** novamente, clique em **Agregação**e, na lista **Item** , clique duas vezes em **Méd**.  
  
11. Na lista **Categoria** , clique em **Campos (Expressões)** e, na lista **Valores** , clique duas vezes em **YTDPurchase**novamente.  
  
13. Imediatamente após `Fields!YTDPurchase.Value`, digite **, "Expressões"))**  
  
    A expressão completa é: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions"))`  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. Na caixa **Unidade de Medida dos Estados** , selecione **Numérica**.  
  
17. Na linha com a seta apontando para baixo, clique no botão **fx** à direita da caixa de texto do valor **Start** .  

    ![report-builder-expression-tutorial-indicator-start](../reporting-services/media/report-builder-expression-tutorial-indicator-start.png)
  
18. Na caixa de diálogo **Expressão** , expanda **Funções Comuns**e clique em **Matemática**.  
  
19. Na lista **Item** , clique duas vezes em **Arredondar**.  
  
20. Na lista **Categoria** , clique em **Campos (Expressões)** e, na lista **Valores** , clique duas vezes em **YTDPurchase**novamente.  
  
22. Imediatamente após `Fields!YTDPurchase.Value`, digite  **-** (um sinal de subtração). 
  
24. Expanda **Funções Comuns** novamente e clique em **Agregação**e, na lista **Item** , clique duas vezes em **Méd**.  
  
26. Na lista **Categoria** , clique em **Campos (Expressões)** e, na lista **Valores** , clique duas vezes em **YTDPurchase**novamente.  
  
28. Imediatamente após `Fields!YTDPurchase.Value`, digite **, "Expressões")) < 0**  
  
    A expressão completa é: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) < 0`  
  
30. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
31. Na caixa de texto do valor **End** , digite **0**  
  
32. Clique na linha com a seta apontando para a horizontal e clique em **Excluir**.  

    ![report-builder-expression-tutorial-delete-indicator-state](../reporting-services/media/report-builder-expression-tutorial-delete-indicator-state.png)
    
    Agora, existem apenas duas setas, para cima ou para baixo.
  
33. Na linha com a seta apontando para cima, na caixa **Iniciar** , digite **0**  
  
34. Clique no botão **fx** à direita da caixa de texto do valor **End** .  
  
35. Na caixa de diálogo **Expressão** , exclua **100** e crie a expressão: `=Round(Fields!YTDPurchase.Value - Avg(Fields!YTDPurchase.Value, "Expressions")) >0`  
  
36. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
37. Clique novamente em **OK** para fechar a caixa de diálogo **Propriedades do indicador** .  
  
38. Clique em **Executar** para visualizar o relatório.  

    ![report-builder-expression-tutorial-preview-indicator](../reporting-services/media/report-builder-expression-tutorial-preview-indicator.png)
  
## <a name="GreenBar"></a>8. Criar um relatório em tiras  
Crie um parâmetro para que os leitores do relatório possam especificar a cor a ser aplicada a linhas alternadas no relatório, transformando-o em um relatório em tiras.  
  
### <a name="to-add-a-parameter"></a>Para adicionar um parâmetro  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  No painel **Dados do Relatório** , clique com o botão direito do mouse em **Parâmetros** e clique em **Adicionar Parâmetro**.  

    ![report-builder-expression-tutorial-add-parameter](../reporting-services/media/report-builder-expression-tutorial-add-parameter.png)
  
    A caixa de diálogo **Propriedades do Parâmetro do Relatório** é aberta.  
  
3.  Em **Prompt**, digite **Escolher cor**  
  
4.  Em **Nome**, digite **RowColor**  
  
5.  Na guia **Valores Disponíveis** , clique em **Especificar valores**.  
  
7.  Clique em **Adicionar**.  
  
8.  Na caixa **Rótulo** , digite **Amarelo**  
  
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

    ![report-builder-expression-tutorial-parameter-available](../reporting-services/media/report-builder-expression-tutorial-parameter-available.png)
  
19. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-apply-alternating-colors-to-detail-rows"></a>Para aplicar cores alternativas a linhas de detalhes  
  
1.   Selecione todas as células na linha de dados, exceto pela célula na coluna **M/F** , que tem sua própria cor da tela de fundo.  

     ![report-builder-expression-tutorial-select-banded](../reporting-services/media/report-builder-expression-tutorial-select-banded.png)
  
4.  No painel Propriedades, clique em **BackgroundColor**. 

     Se você não vir o painel Propriedades, na guia **Exibir** , marque a caixa de seleção **Propriedades** .  
  
    Se as propriedades estiverem listadas por categoria no painel Propriedades, você encontrará **BackgroundColor** na categoria **Diversos** .  
  
5.  Clique na seta para baixo e em **Expressão**.  

    ![report-builder-expression-tutorial-banded-color-property](../reporting-services/media/report-builder-expression-tutorial-banded-color-property.png)
  
6.  Na caixa de diálogo **Expressão** , expanda **Funções Comuns**e clique em **Fluxo do Programa**.  
  
7.  Na lista **Item** , clique duas vezes em **IIf**.  
  
8.  Em **Funções Comuns**, clique em **Diversos**e, na lista **Item** , clique duas vezes em **RowNumber**.  

9. Imediatamente após **RowNumber(** , digite **Nada) MOD 2,**
  
8. Clique em **Parâmetros** e, na lista **Valores** , clique duas vezes em **RowColor**.  
  
22. Imediatamente após `Parameters!RowColor.Value`, digite **, "Branco")**  
  
    A expressão completa é: `=IIF(RowNumber(Nothing) MOD 2, Parameters!RowColor.Value, "White")`  
    
    ![report-builder-expression-tutorial-banded-color-expressn](../reporting-services/media/report-builder-expression-tutorial-banded-color-expressn.png)
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="run-the-report"></a>Executar o relatório  
  
1.  Na guia **Início** , clique em **Executar**.  

    Agora, quando executa o relatório, você não vê o relatório até escolher uma cor para as faixas não são brancas.
  
3.  Na lista **Escolher cor** , selecione uma cor para as faixas do relatório que não são brancas.  
    
    ![report-builder-expression-tutorial-select-color](../reporting-services/media/report-builder-expression-tutorial-select-color.png)
  
4.  Clique em **Exibir Relatório**.  
  
    O relatório é renderizado e linhas alternativas têm o plano de fundo escolhido por você. 
    
    ![report-builder-expression-tutorial-preview-banded](../reporting-services/media/report-builder-expression-tutorial-preview-banded.png) 
  
## <a name="Title"></a>(opcional) Adicionar um título de relatório  
Adicione um título ao relatório.  
  
### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Resumo de Comparação de Vendas**e selecione o texto.  
  
3.  Na guia **Início** , na caixa **Fonte** , defina:

    -  Tamanho = 18
    -  Cor = Cinza
    -  Negrito
  
4.  Na guia **Início** , clique em **Executar**.  
  
3.  Selecione uma cor para as faixas do relatório que não são brancas e clique em **Exibir Relatório**.  
  
## <a name="Save"></a>(opcional) Salvar o relatório  
É possível salvar relatórios em um servidor de relatório, em uma biblioteca do SharePoint ou no computador. Para obter mais informações, consulte [Salvando relatórios &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder/saving-reports-report-builder.md).  
  
Neste tutorial, você salva o relatório em um servidor de relatório. Se você não tiver acesso ao servidor de relatório, salve o relatório no computador.  
  
### <a name="to-save-the-report-to-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No menu **Arquivo** > **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
    A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for estabelecida, você verá o conteúdo da pasta de relatório que o administrador do servidor de relatório especificou como o local de relatório padrão.  
  
4.  Dê um nome ao relatório e clique em **Salvar**.  
  
O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.

Agora, os leitores do relatório podem exibir o relatório no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .

![report-builder-expression-tutorial-final-in-browser](../reporting-services/media/report-builder-expression-tutorial-final-in-browser.png)

   
## <a name="see-also"></a>Consulte Também  
[Expressões &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
[Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
[Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
[Imagens, caixas de texto, retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)  
[Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[Conjuntos de dados de relatório &#40;SSRS&#41;](../reporting-services/report-data/report-datasets-ssrs.md)  
  
  
  

