---
title: 'Tutorial: Relatório de mapa (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3b456d165ef9c4f09bb040cefb63644efb51c112
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098858"
---
# <a name="tutorial-map-report-report-builder"></a>Tutorial: Relatório de mapa (construtor de relatórios)
  Este tutorial foi desenvolvido para ajudá-lo a aprender sobre os recursos de mapa que você pode usar para exibir dados de relatório em comparação com um plano de fundo geográfico.  
  
 Os mapas se baseiam em dados espaciais que geralmente consistem em pontos, linhas e polígonos. Por exemplo, um polígono pode representar a estrutura de tópicos de um município, uma linha pode representar uma estrada e um ponto pode representar o local de uma cidade. Cada tipo de dados espaciais é exibido em uma camada do mapa separada como um conjunto de elementos de mapa.  
  
 Para variar a aparência de elementos de mapas, especifique um campo com valores que correspondem aos elementos de mapas com dados analíticos de um conjunto de dados. Também é possível definir regras que variam em cor, tamanho ou outras propriedades com base em intervalos de dados.  
  
 Neste tutorial, você criará um relatório de mapa que exibe a localização de lojas em municípios estatais de Nova York.  
  
##  <a name="BackToTop"></a> O que você aprenderá  
 Neste tutorial, você aprenderá a:  
  
1.  [Criar um mapa com uma camada de polígono do Assistente de mapa](#Map)  
  
2.  [Adicionar uma camada de ponto do mapa para locais de Store de exibição](#PointLayer)  
  
3.  [Adicionar uma camada de linha do mapa para exibir uma rota](#LineLayer)  
  
4.  [Adicionar um plano de fundo do Bing Maps](#TileLayer)  
  
5.  [Tornar uma camada transparente](#Transparent)  
  
6.  [Variar as cores de municípios com base em vendas](#Vary)  
  
    1.  [Crie uma relação entre dados espaciais e analíticos](#Relationship)  
  
    2.  [Especifique regras de cores para polígonos](#ColorRules)  
  
    3.  [Formatar os dados na escala de cores como moeda](#ColorScale)  
  
    4.  [Criar uma nova legenda](#NewLegend)  
  
    5.  [Regras de cores e legenda associada](#Associate)  
  
    6.  [Limpar cores dos municípios sem dados](#NoData)  
  
7.  [Adicionar um ponto personalizado](#CustomPoint)  
  
8.  [Centralizar a exibição de mapa](#CenterView)  
  
9. [Adicionar um título de relatório](#Title)  
  
10. [Salvar o relatório](#Save)  
  
> [!NOTE]  
>  Neste tutorial, as etapas do assistente são consolidadas em dois procedimentos: um para criar o conjunto de dados e um para criar uma tabela. Para obter instruções passo a passo sobre como navegar até um servidor de relatório, escolher uma fonte de dados, criar um conjunto de dados e executar o assistente, confira o primeiro tutorial desta série: [Tutorial: Ciar um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo estimado para concluir este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Map"></a> 1. Criar um mapa com uma camada de polígono usando o Assistente de Mapas  
 Adicionar um mapa em seu relatório a partir da galeria de mapas. O mapa tem uma camada que exibe os municípios do estado de Nova York. A forma de cada município é um polígono com base em dados espaciais inseridos no mapa a partir da galeria de mapas.  
  
#### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>Para adicionar um mapa com o assistente de mapa em um novo relatório  
  
1.  Clique em **inicie**, aponte para **programas**, aponte para [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **construtor de relatórios**e, em seguida, clique em **construtor de relatórios**.  
  
     A caixa de diálogo Guia de Introdução é exibida.  
  
    > [!NOTE]  
    >  Se a caixa de diálogo Guia de Introdução não for exibida, no botão Construtor de Relatórios, clique em **Novo**.  
  
2.  No painel esquerdo, verifique se **Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Mapa**.  
  
4.  Clique em **Criar**.  
  
5.  Na página**Escolher uma fonte de dados espaciais** , verifique se a **Galeria de mapas** está selecionada.  
  
6.  No painel de Galeria de Mapas, expanda **Estados por País** em **EUA**e clique em **Nova York**.  
  
     O painel de Visualização de Mapa exibe o mapa do município de Nova York.  
  
7.  Clique em **Avançar**.  
  
8.  Na página **Escolher as opções de dados espaciais e de exibição de mapa** , aceite os padrões. Por padrão, os elementos do mapa de uma galeria de mapas serão inseridos automaticamente na definição do relatório.  
  
9. Clique em **Avançar**.  
  
10. Na página **Escolher visualização do mapa** , verifique se **Mapa Básico** está selecionado e clique em **Avançar**.  
  
11. Na página **Escolher o tema da cor e a visualização dos dados** , selecione a opção **Exibir rótulos** .  
  
12. Se estiver selecionada, desmarque a opção **Mapa de cor única** .  
  
13. Na lista suspensa **Campo de dados** , clique em #COUNTYNAME. O painel Visualização de Mapa no assistente exibe os seguintes itens:  
  
    -   Um título com o texto **Título do Mapa**.  
  
    -   Um mapa que exibe os municípios em Nova York onde cada município é uma cor diferente e o nome do município aparece onde possível na área do município.  
  
    -   Uma legenda que contém um título e uma lista de itens de 1 a 5.  
  
    -   Uma escala de cores que contém valores de 0 a 160 e nenhuma cor.  
  
    -   Uma escala de distância que exibe quilômetros (km) e milhas (mi).  
  
14. Clique em **Concluir**.  
  
     O mapa é adicionado à superfície de design.  
  
15. Clique no mapa para selecioná-lo e exibir o painel **Camadas do Mapa**. O painel **Camadas do Mapa** mostra uma camada de polígono de tipo de camada **Inserido**. Cada região é um elemento do mapa inserido nessa camada.  
  
    > [!NOTE]  
    >  Se você não vir o painel **Camadas do Mapa** , talvez ele esteja fora da exibição atual. Use a barra de rolagem na parte inferior da janela do modo Design para alterar sua exibição. Opcionalmente, na guia **Exibir** , desmarque as **Propriedades** ou a opção **Dados do Relatório** para fornecer mais área de superfície de design.  
  
16. Clique com o botão direito do mouse no título do mapa e clique em **Propriedades do Título**.  
  
17. Substitua o texto do título por **Vendas por Loja**.  
  
18. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
19. Visualize o relatório.  
  
 O relatório renderizado exibe o título do mapa, o mapa e a escala de distância. Os municípios estão em uma camada do polígono de mapas. Cada município é um polígono que varia por cor de uma paleta de cores, mas as cores não estão associadas a nenhum dado. A escala de distância exibe distâncias em quilômetros e em milhas.  
  
 A legenda de mapa e a escala de cores ainda não são exibidos porque não há dados analíticos associados a cada município. Você adicionará dados analíticos posteriormente neste tutorial.  
  
##  <a name="PointLayer"></a> 2. Adicionar uma camada de ponto de mapa para exibir locais de loja  
 Use o assistente de camada do mapa para adicionar uma camada de pontos que exibe a localização das lojas.  
  
> [!NOTE]  
>  Neste tutorial, a consulta contém os valores de dados para que não precise de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
#### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>Para adicionar uma camada de ponto com base em uma consulta espacial do SQL Server  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . Na barra de ferramentas, clique no botão **Assistente de Nova Camada** ![rs_IconMapLayerWizard](../../2014/tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard").  
  
3.  Na página **Escolher uma fonte de dados espaciais** , selecione **Consulta espacial do SQL Server**e clique em **Avançar**.  
  
4.  Na página **Escolha um conjunto de dados com dados espaciais do SQL Server** , clique em **Adicionar um novo conjunto de dados com dados espaciais do SQL Server**e clique em **Avançar**.  
  
5.  Na página **Escolha uma conexão com uma fonte de dados espaciais do SQL Server** , selecione uma fonte de dados existente ou navegue até o servidor de relatório e selecione uma fonte de dados.  
  
6.  Clique em **Avançar**.  
  
7.  Na página Criar uma Consulta, clique em **Editar como Texto**.  
  
8.  Cole o seguinte texto de consulta no painel da consulta:  
  
    ```  
    Select 114 as StoreKey, 'Contoso Albany Store' as StoreName, 1125 as SellingArea, 'Albany' as City, 'Albany' as County,   
     CAST(1000000 as money) as Sales, CAST('POINT(-73.7472924218681 42.6564617079878)' as geography) AS SpatialLocation  
    UNION ALL SELECT 115 AS StoreKey, 'Contoso New York No.1 Store' AS  StoreName, 500 as SellingArea, 'New York' AS City, 'New York City' as County,  
     CAST('2000000' as money) as Sales, CAST('POINT(-73.9922069374483 40.7549638237402)' as geography) AS SpatialLocation  
    UNION ALL Select 116 as StoreKey, 'Contoso Rochester No.1 Store' as StoreName, 462 as SellingArea, 'Rochester' as City,  'Monroe' as County,    
     CAST(3000000 as money) as Sales, CAST('POINT(-77.624041566786 43.1547066024338)' as geography)  AS SpatialLocation  
    UNION ALL Select 117 as StoreKey, 'Contoso New York No.2 Store' as StoreName, 700 as SellingArea, 'New York' as City,'New York City' as County,    
      CAST(4000000 as money) as Sales, CAST('POINT(-73.9712488 40.7830603)' as geography) AS SpatialLocation  
    UNION ALL Select 118 as StoreKey, 'Contoso Syracuse Store' as StoreName, 680 as SellingArea, 'Syracuse' as City, 'Onondaga' as County,  
     CAST(5000000 as money) as Sales, CAST('POINT(-76.1349120532546 43.0610223535974)' as geography) AS SpatialLocation  
    UNION ALL Select 120 as StoreKey, 'Contoso Plattsburgh Store' as StoreName, 560 as SellingArea, 'Plattsburgh' as City,  'Clinton' as County,  
     CAST(6000000 as money) as Sales, CAST('POINT(-73.4728622833178 44.7028831413324)' as geography) AS SpatialLocation  
    UNION ALL Select 121 as StoreKey, 'Contoso Brooklyn Store' as StoreName, 1125 as SellingArea, 'Brooklyn' as City, 'New York City' as County,  
     CAST(7000000 as money) as Sales, CAST('POINT (-73.9638533447143 40.6785123489351)' as geography) AS SpatialLocation  
    UNION ALL Select 122 as StoreKey, 'Contoso Oswego Store' as StoreName, 500 as SellingArea, 'Oswego' as City, 'Oswego' as County,    
     CAST(8000000 as money) as Sales, CAST('POINT(-76.4602850815536 43.4353224527794)' as geography) AS SpatialLocation  
    UNION ALL Select 123 as StoreKey, 'Contoso Ithaca Store' as StoreName, 460 as SellingArea, 'Ithaca' as City, 'Tompkins' as County,  
     CAST(9000000 as money) as Sales, CAST('POINT(-76.5001866085881 42.4310489934743)' as geography) AS SpatialLocation  
    UNION ALL Select 124 as StoreKey, 'Contoso Rochester No.2 Store' as StoreName, 700 as SellingArea, 'Rochester' as City, 'Monroe' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-77.6240415667866 43.1547066024338)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. Na barra de ferramentas do designer de consultas, clique em **Executar** (**!**).  
  
     O conjunto de resultados exibe sete colunas: StoreKey, StoreName, SellingArea, City, County, Sales e SpatialLocation. Esses dados representam um conjunto de lojas no Estado de Nova York que vendem bens de consumo. Cada linha no conjunto de resultados contém um identificador de loja, o nome da loja, a área disponível para exibição do produto, a cidade e o município no qual a loja está localizada, o total de vendas e o local espacial em longitude e latitude. A área de exibição varia de 455 pés quadrados a 1.125 pés quadrados.  
  
10. Clique em **Avançar**.  
  
     O conjunto de dados de relatório chamado DataSet1 é criado para você. Após a conclusão do assistente, você poderá usar os Dados do Relatório para exibir sua coleção de campos.  
  
11. Sobre o **escolha dados espaciais e opções de exibição de mapa** página, verifique o **campo espacial** é `SpatialLocation` e que o **tipo de camada** é **ponto**. Aceite os outros padrões nesta página.  
  
     A exibição do mapa mostra círculos que marcam o local de cada loja.  
  
12. Clique em **Avançar**.  
  
13. Especifique um tipo de mapa que exiba marcadores que variem por dados analíticos. Na página Escolher visualização do mapa, clique em **Mapa de Marcador Analítico**e clique em **Avançar**.  
  
14. Na página **Escolher o conjunto de dados analíticos** , clique em DataSet1. Esse conjunto de dados contém dados analíticos e dados espaciais que serão exibidos na nova camada de ponto.  
  
15. Clique em **Avançar**.  
  
16. Na página **Escolher o tema da cor e a visualização dos dados** , desmarque a opção **Usar cores de marcador para visualizar dados** e selecione **Usar tipos de marcador para visualizar dados**.  
  
17. No **Campo de dados**, selecione `[Sum(SellingArea)]` para variar os tipos de marcador conforme o tamanho da área que uma loja reserva para exibir os produtos.  
  
18. Clique em **Concluir**.  
  
     A camada do mapa é adicionada ao relatório. A legenda exibe os tipos de marcadores com base nos valores SellingArea.  
  
     Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . O painel **Camada do Mapa** exibe uma nova camada, PointLayer1, com o tipo de fonte de dados espaciais **DataRegion**.  
  
19. Adicione um título à legenda. Clique com o botão direito do mouse no título e clique em **Propriedades do Título da Legenda**.  
  
20. Exclua o título e digite a **Área de Exibição (Pés Quadrados)**.  
  
21. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
22. Exiba os valores padrão que foram definidos pelo assistente. No painel **Camadas do Mapa**, clique com o botão direito na camada de ponto e clique em **Regra de Tipo de Marcador**.  
  
     Na guia **Geral** , os marcadores são listados na ordem na qual eles são exibidos na legenda. Na guia **Distribuição** , o número de subintervalos é 5. Na guia **Legenda** , o texto de legenda é definido para exibir o valor de início e término em cada intervalo.  
  
23. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. Visualize o relatório.  
  
 O mapa exibe os locais de lojas no estado de Nova York. O tipo de marcador para cada loja se baseia na área de exibição. Foram calculados cinco intervalos de área de exibição automaticamente para você.  
  
##  <a name="LineLayer"></a> 3. Adicionar uma camada de linha de mapa para exibir uma rota  
 Use o assistente de camada do mapa para adicionar uma camada do mapa que exibe uma rota entre duas lojas. Neste tutorial, o caminho é criado de três locais de loja. Em um aplicativo comercial, o caminho pode ser a melhor rota entre lojas.  
  
#### <a name="to-add-a-line-layer-to-map"></a>Para adicionar uma camada de linha ao mapa  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . Na barra de ferramentas, clique em **Assistente de nova camada**.  
  
3.  Na página **Escolher uma fonte de dados espaciais** , selecione **Consulta espacial do SQL Server** e clique em **Avançar**.  
  
4.  Na página **Escolher um conjunto de dados com dados espaciais do SQL Server** , clique em **Adicionar um novo conjunto de dados com dados espaciais do SQL Server** e clique em **Avançar**.  
  
5.  Em **Escolher uma conexão com uma fonte de dados espaciais do SQL Server**, selecione DataSource1, a fonte de dados que você criou no primeiro procedimento.  
  
6.  Clique em **Avançar**.  
  
7.  Na página **Crie uma Consulta** , clique em **Editar como Texto**. O designer de consulta alterna para o modo baseado no texto.  
  
8.  Cole o seguinte texto de consulta no painel da consulta:  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. Clique em **Avançar**.  
  
     Um caminho é exibido no mapa que conecta três lojas.  
  
10. Na página **Escolher as opções de dados espaciais e de exibição de mapa** , verifique se o **Campo espacial** é **Route** e se o **Tipo de camada** é **Linha**. Aceite os outros padrões.  
  
     A exibição de mapa exibe um caminho de uma loja na parte norte do estado de Nova York até uma loja na parte sul do estado de Nova York.  
  
11. Clique em **Avançar**.  
  
12. Na página **Escolher visualização do mapa** , clique em **Mapa da Linha Básica**e clique em **Avançar**.  
  
13. Em **Escolher o tema da cor e a visualização dos dados**, selecione a opção **Mapa de Cor Única**. O caminho é exibida em uma única cor com base no tema selecionado.  
  
14. Clique em **Concluir**.  
  
 O mapa exibe uma nova camada de linha com o tipo de fonte de dados espaciais **DataSet**. Neste exemplo, os dados espaciais vêm de um conjunto de dados, mas nenhum dado analítico é associado à linha.  
  
##  <a name="TileLayer"></a> 4. Adicionar um plano de fundo lado a lado do Bing Maps  
 Adicione uma camada do mapa que exibe um plano de fundo lado a lado do Bing Maps.  
  
#### <a name="to-add-a-virtual-earth-tile-background"></a>Para adicionar plano de fundo lado a lado de Terra Virtual  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . Na barra de ferramentas, clique em **Adicionar camada**![rs_IconMapAddLayer](../../2014/tutorials/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer").  
  
3.  Na lista suspensa, clique em **Camada do Bloco**.  
  
     A última camada no painel **Camada do Mapa** é TileLayer1. Por padrão, a camada lado a lado exibe o estilo de mapa rodoviário.  
  
    > [!NOTE]  
    >  No assistente, você também pode adicionar uma camada lado a lado na página **Escolher as opções de dados espaciais e de exibição do mapa** . Para fazer isso, selecione **Adicionar um plano de fundo do Bing Maps a esta exibição de mapa**. Em um relatório renderizado, o plano de fundo lado a lado exibirá itens lado a lado do Bing Maps para o visor e o nível de zoom do mapa atual.  
  
4.  Clique na seta para baixo em TileLayer1 e em **Propriedades da Peça**.  
  
5.  Em **Tipo**, selecione **Aéreo**. A vista aérea não contém texto.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Transparent"></a> 5. Tornar uma camada transparente  
 Para deixar que os itens em uma camada sejam exibidos por outra camada, você pode ajustar a ordem de camadas e a transparência de cada camada para obter o efeito desejado.  
  
#### <a name="to-set-the-transparency-of-a-layer"></a>Para definir a transparência de uma camada  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** .  
  
3.  Clique na seta para baixo em PolygonLayer1 e em **Dados da Camada**. A caixa de diálogo **Mapear Propriedades de Camada do Polígono** aparece.  
  
4.  Clique em **Visibilidade**.  
  
5.  Em **Transparência (%)**, digite **30**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 A superfície de design exibe os municípios como semitransparentes.  
  
##  <a name="Vary"></a> 6. Variar as cores de municípios com base em vendas  
 Cada município na camada do polígono tem uma cor diferente porque o processador de relatório atribui um valor de cor automaticamente da paleta de cores com base no tema que você escolheu na última página do assistente de mapa.  
  
 Nas etapas a seguir, especifique uma regra de cor para associar cores específicas a um intervalo de vendas de lojas para cada município. As cores vermelho-amarelo-verde indicam vendas altas-médias-baixas relativas. Formate a escala de cores para mostrar a moeda. Exiba os intervalos de vendas anuais em uma nova legenda. Para municípios que não contêm lojas, não use nenhuma cor para mostrar que não há dados associados.  
  
###  <a name="Relationship"></a> 6a. Criar um relacionamento entre dados espaciais e analíticos  
 Para variar as formas do município por cor, com base em dados analíticos, primeiro associe os dados analíticos aos dados espaciais. Neste tutorial, você usará o nome do município para correspondência.  
  
##### <a name="to-build-a-relationship-between-spatial-data-and-analytical-data"></a>Para criar uma relação entre os dados espaciais e os dados analíticos  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** .  
  
3.  Clique na seta para baixo em PolygonLayer1 e em **Dados da Camada**. A caixa de diálogo **Mapear Propriedades de Camada do Polígono** aparece.  
  
4.  Clique em **Dados Analíticos**.  
  
5.  Na lista suspensa, selecione DataSet1. Esse conjunto de dados foi criado pelo assistente quando você especificou a consulta de dados espaciais para os municípios.  
  
6.  Em **Campos a serem associados**, clique em **Adicionar**. Uma nova linha será adicionada.  
  
7.  Em **Do conjunto de dados espacial**, na lista suspensa, clique em COUNTYNAME.  
  
8.  Em **Do conjunto de dados analítico**, na lista suspensa, clique em [County].  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Visualize o relatório.  
  
 Ao especificar um campo de correspondência com base na fonte de dados espaciais e no conjunto de dados analítico, você permite que o processador de relatório agrupe dados analíticos com base nos elementos do mapa. Um elemento de mapa com ligação de dados tem uma correspondência para os valores especificados.  
  
 Cada município que contém uma loja tem uma cor baseada na paleta de cores para o estilo escolhido no assistente.  
  
###  <a name="ColorRules"></a> 6b. Especificar as regras de cores para polígonos  
 Para criar uma regra que varia a cor de cada município baseada em vendas da loja, você deve especificar os valores de intervalo, o número de divisões dentro daquele intervalo que você deseja exibir, e as cores a serem usadas.  
  
##### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>Para especificar regras de cores para todos os polígonos com dados associados  
  
1.  Alterne para o modo Design.  
  
2.  Clique na seta para baixo em PolygonLayer1 e clique em **Regra de Cor do Polígono**. A caixa de diálogo **Mapear Propriedades de Regras de Cor** é aberta. Observe que a opção de regra de cor **Visualizar dados usando a paleta de cores** está selecionada. Esta opção foi definida no assistente.  
  
3.  Selecione **Visualizar dados usando intervalos de cores**. A opção da paleta é substituída pelas opções de cor inicial, cor intermediária e cor final.  
  
4.  Defina valores de intervalo para vendas por município. Em **Campo de dados**, na lista suspensa, selecione `[Sum(Sales)]`.  
  
5.  Para alterar o formato para exibir moeda em milhares, altere a expressão para o seguinte: `=Sum(Fields!Sales.Value)/1000`  
  
6.  Altere **Cor inicial** para **Vermelho**.  
  
7.  Altere **Cor final** para **Verde**.  
  
     **Vermelho** representa baixos valores de vendas, **Amarelo** representa valores de vendas intermediários e **Verde** representa valores de vendas altos. O processador de relatório calcula um intervalo de cores com base nesses valores e as opções que você escolhe na página **Distribuição** .  
  
8.  Clique em **Distribuição**.  
  
9. Verifique se o tipo de distribuição é **Ideal**. Para a expressão da etapa 5, a distribuição ideal divide os valores em subintervalos que equilibram o número de itens em cada intervalo e abrangem cada intervalo.  
  
10. Aceite os valores padrão para outras opções nesta página. Quando você selecionar o tipo de distribuição ideal, o número de subintervalos será calculado quando o relatório for executado.  
  
11. Clique em **Legenda**.  
  
12. Em **Opções de escala de cores**, verifique se a opção **Mostrar em escala de cores** está selecionada.  
  
13. Em **Mostrar nesta legenda**, selecione a linha em branco na lista suspensa. Por enquanto, você mostrará apenas os intervalos de cores na escala de cores.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 A escala de cores exibe cinco cores: vermelho, laranja, amarelo, verde-amarelado e verde. Cada cor representa um intervalo de vendas que é calculado automaticamente com base nas vendas por município.  
  
###  <a name="ColorScale"></a> 6c. Formatar os dados na escala de cores como moeda  
 Por padrão, os dados têm um formato geral. Você pode aplicar formatos personalizados.  
  
##### <a name="to-set-the-format-for-the-color-scale"></a>Para definir o formato da escala de cores  
  
1.  Clique com o botão direito do mouse na escala de cores e clique em **Propriedades da Escala de Cores**.  
  
2.  Clique em **Número**.  
  
3.  Em **Categoria**, clique em **Moeda**.  
  
4.  Em **Casas decimais**, digite **0**. Esse formato especifica que não haverá nenhuma casa decimal para moeda.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Visualize o relatório.  
  
 A escala de cores exibe as vendas anuais no formato de moeda para cada intervalo.  
  
###  <a name="NewLegend"></a> 6d. Criar uma nova legenda  
 Por padrão, todas as regras são exibidas na primeira legenda. Para melhorar a exibição de um mapa, adicione legendas.  
  
 Para alterar a exibição padrão, há duas etapas: crie uma nova legenda e associe os resultados da regra para uma camada do mapa à nova legenda.  
  
##### <a name="to-create-a-new-legend"></a>Para criar uma nova legenda  
  
1.  Alterne para o modo Design.  
  
2.  Clique com o botão direito do mouse no mapa fora do visor e clique em **Adicionar Legenda**. Uma nova legenda será adicionada ao mapa em um local padrão.  
  
3.  Clique com o botão direito do mouse na legenda e clique em **Propriedades da Legenda**.  
  
4.  Em **Opções de Posição**, clique no local que especifica onde você deseja que a legenda apareça em relação ao visor. O mapa na superfície de design é alterado para mostrar o efeito de suas seleções.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Clique em **Título** na legenda para selecionar o título de legenda.  
  
7.  Clique em **Título** novamente para entrar no modo de inserção de texto. Substitua o **Título** por **Vendas (Milhares)** e clique fora do texto.  
  
 A legenda se expande para exibir o título.  
  
###  <a name="Associate"></a> 6e. Associar regras de cores e legenda  
 Cada legenda pode exibir um ou mais conjuntos de resultados de regra.  
  
##### <a name="to-associate-a-legend-with-color-rules"></a>Para associar uma legenda a regras de cores  
  
1.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** .  
  
2.  Clique na seta para baixo em PolygonLayer1 e clique em **Regra de Cor do Polígono**. A caixa de diálogo **Mapear Propriedades de Regras de Cor** é aberta.  
  
3.  Clique em **Legenda**.  
  
4.  Em **Opções de escala de cores**, limpe **Mostrar em escala de cores**.  
  
5.  Em **Opções de legenda**, na lista suspensa, selecione Legend2. A opção de texto da legenda aparece. Por padrão, texto de legenda é formatado com uma cadeia de formato geral do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] . Os 0 em N0 não especifica nenhum dígito decimal.  
  
6.  Na **texto de legenda**, use o seguinte formato para especificar a moeda sem dígitos decimais: `#FROMVALUE {C0} - #TOVALUE {C0}`  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Na superfície de design, a legenda exibe os intervalos de cores com dados de exemplo formatados como moeda.  
  
8.  Visualize o relatório.  
  
 Os municípios que têm lojas e vendas associadas são exibidos de acordo com as regras de cores. Municípios que não têm nenhuma venda não têm cores.  
  
###  <a name="NoData"></a> 6f. Alterar a cor dos municípios para os quais não há dados  
 Você pode definir as opções de exibição padrão para todos os elementos de mapas em uma camada. As regras de cores têm precedência sobre essas opções de exibição.  
  
##### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>Para definir as propriedades de exibição para todos os elementos em uma camada  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** .  
  
3.  Clique na seta para baixo em PolygonLayer1 e clique em **Propriedades do Polígono**. A caixa de diálogo **Mapear Propriedades do Polígono** aparece. As opções de exibição definidas nesta caixa de diálogo se aplicam a todos os polígonos na camada antes de as opções de exibição baseadas em regras serem aplicadas.  
  
4.  Clique em **Preenchimento**.  
  
5.  Verifique se o estilo de preenchimento é **Sólido.** Gradações e padrões se aplicam a todas as cores.  
  
6.  Em **Cor**, clique na seta para baixo e clique em **Azul Claro Acinzentado**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Visualize o relatório.  
  
 Municípios sem dados associados são exibidos em azul. Somente os municípios com dados analíticos associados são exibidos nas cores de **Vermelho** a **Green** das regras de cores especificadas.  
  
##  <a name="CustomPoint"></a> 7. Adicionar um ponto personalizado  
 Para representar uma nova loja que ainda não foi construída, especifique um ponto e use o tipo de marcador **PushPin** .  
  
#### <a name="to-add-a-custom-point"></a>Para adicionar um ponto personalizado  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . Na barra de ferramentas, clique em **Adicionar Camada**e em **Camada de Ponto**.  
  
     Uma nova camada de ponto é adicionada ao mapa. Por padrão, a camada de ponto tem o tipo de dados espacial **Inserido**.  
  
3.  Clique na seta para baixo em PointLayer2 e em **Adicionar Ponto**.  
  
4.  Mova o ponteiro sobre o visor do mapa. O cursor se transforma em uma cruz.  
  
5.  Clique no local no mapa em que você deseja adicionar um ponto. Neste tutorial, clique em um local em um município no início da rota. Um ponto marcado por um círculo é adicionado à camada no local em que você clicou. Por padrão, o ponto é selecionado.  
  
6.  Clique com o botão direito do mouse no ponto adicionado e clique em **Propriedades de Ponto Inserido**.  
  
7.  Selecione a opção **Substituir opções de ponto para esta camada**. Páginas adicionais aparecem na caixa de diálogo. Os valores que você definiu aqui têm precedência sobre as opções de exibição da camada ou para regras de cores.  
  
8.  Clique em **Marcador**.  
  
9. Para **Tipo de marcador**, selecione **Estrela**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Visualize o relatório.  
  
 O novo ponto adicionado aparece como um **Estrela**.  
  
#### <a name="to-add-a-label-for-the-custom-point"></a>Para adicionar um rótulo ao ponto personalizado  
  
1.  Alterne para o modo Design.  
  
2.  Clique com o botão direito do mouse no ponto recém-adicionado e clique em **Propriedades de Ponto Inserido**.  
  
3.  Clique em **Rótulos**.  
  
4.  Em **Texto do rótulo**, digite **Nova Loja**.  
  
5.  Em **Posicionamento**, clique em **Superior**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Visualize o relatório.  
  
 O rótulo aparece acima do local da loja.  
  
##  <a name="CenterView"></a> Centralizar a exibição de mapa  
 Altere o centro do visor do mapa e o nível de zoom.  
  
#### <a name="to-change-the-viewport"></a>Para alterar o visor  
  
1.  Clique com o botão direito do mouse no visor do mapa clique em **Propriedades do Visor**.  
  
2.  Clique em **Centralizar e Aplicar Zoom**.  
  
3.  Verifique se a opção **Definir um centro de exibição e um nível de zoom** está selecionada.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Clique com o botão esquerdo do mouse no visor do mapa e arraste o centro do visor para o local desejado.  
  
6.  Use a roda do mouse para alterar o nível de zoom do visor.  
  
7.  Visualize o relatório.  
  
 No modo Design, o mapa na superfície de exibição e a exibição se baseiam em dados de exemplo. No relatório renderizado, a exibição de mapa é centralizada na exibição especificada.  
  
##  <a name="Title"></a> Adicionar um título de relatório  
  
#### <a name="to-add-a-report-title"></a>Para adicionar um título de relatório  
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas nas Lojas de Nova York** e clique fora da caixa de texto.  
  
 Esse título aparecerá na parte superior do relatório. Os itens na parte superior do corpo do relatório quando não há cabeçalho de página definido são os equivalentes de um cabeçalho de relatório.  
  
##  <a name="Save"></a> Salvar o relatório  
  
#### <a name="to-save-the-report"></a>Para salvar o relatório  
  
1.  Alterne para o modo Design.  
  
2.  No botão Construtor de Relatórios, clique em **Salvar como**.  
  
3.  Em **Nome**, digite **Vendas nas Lojas de Nova York**.  
  
 Clique em **Salvar**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Isso conclui o passo a passo da adição de um mapa ao seu relatório.  
  
 Para obter mais informações, consulte [Maps &#40;construtor de relatórios e SSRS&#41; ](report-design/maps-report-builder-and-ssrs.md) e a entrada de blog [Cartographic Adjustment of Spatial Data para o SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=152771) em blogs.msdn.com.  
  
 Para obter mais tutoriais, consulte [tutoriais &#40;construtor de relatórios&#41;](report-builder-tutorials.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do &#40;construtor de relatórios&#41;](report-builder-tutorials.md)   
 [Construtor de relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)   
 [Assistente de Mapa e Assistente de Camada do Mapa &#40;Construtor de Relatórios e SSRS&#41;](report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
