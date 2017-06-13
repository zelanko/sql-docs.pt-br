---
title: "Tutorial: Mapear relatórios (construtor de relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: efe91a2e1e8ca7b0744639ed718d63b70e3adc5c
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="tutorial-map-report-report-builder"></a>Tutorial: Relatório de mapa (construtor de relatórios)
Neste tutorial do [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion-md.md)] , você aprenderá sobre os recursos de mapa que podem ser usados para exibir dados em uma tela de fundo geográfica de um relatório paginado do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . 
  
Os mapas se baseiam em dados espaciais que geralmente consistem em pontos, linhas e polígonos. Por exemplo, um polígono pode representar a estrutura de tópicos de um município, uma linha pode representar uma estrada e um ponto pode representar o local de uma cidade. Cada tipo de dados espaciais é exibido em uma camada do mapa separada como um conjunto de elementos de mapa.  
  
Para variar a aparência de elementos de mapas, especifique um campo com valores que correspondem aos elementos de mapas com dados analíticos de um conjunto de dados. Também é possível definir regras que variam em cor, tamanho ou outras propriedades com base em intervalos de dados.  

![report-builder-map-final-map-only](../reporting-services/media/report-builder-map-final-map-only.png)
  
Neste tutorial, você cria um relatório de mapa que exibe a localização de lojas em condados estatais de Nova York.  
   
> [!NOTE]  
> Neste tutorial, as etapas do assistente são consolidadas em dois procedimentos: um para criar o conjunto de dados e um para criar uma tabela. Para obter instruções passo a passo sobre como procurar um servidor de relatório, escolher uma fonte de dados, criar um conjunto de dados e executar o assistente, consulte o primeiro tutorial desta série: [Tutorial: Criando um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo estimado para concluir este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para este tutorial, o servidor de relatório deve ser configurado para dar suporte ao Bing Mapas como tela de fundo. Para obter mais informações, consulte [Planejar suporte ao relatório de mapa](http://msdn.microsoft.com/en-us/5ddc97a7-7ee5-475d-bc49-3b814dce7e19). 

Para obter informações sobre outros requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Map"></a>1. Criar um mapa com uma camada de polígono usando o Assistente de Mapas  
Nesta seção, você adiciona um mapa ao relatório na galeria de mapas. O mapa tem uma camada que exibe os municípios do estado de Nova York. A forma de cada município é um polígono com base em dados espaciais inseridos no mapa a partir da galeria de mapas.  
  
### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>Para adicionar um mapa com o assistente de mapa em um novo relatório  
  
1.  [Inicie o Construtor de Relatórios](../reporting-services/report-builder/start-report-builder.md) no computador, no portal da Web do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] ou no modo integrado do SharePoint.  
  
    A caixa de diálogo **Novo Relatório ou Conjunto de Dados** será aberta.  
  
    Se a caixa de diálogo **Novo Relatório ou Conjunto de Dados** não estiver visível, no menu **Arquivo** > **Novo**.  
  
2.  No painel esquerdo, verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Assistente de Mapa**.  
  
4.  Na página **Escolher uma fonte de dados espaciais** , verifique se a **Galeria de mapas** está selecionada.  
  
6.  Na caixa Galeria de Mapas, expanda **Estados por País** em **EUA**e clique em **Nova York**.  
  
    O painel de Visualização de Mapa exibe o mapa do município de Nova York.  
    
    ![report-builder-map-ny-counties](../reporting-services/media/report-builder-map-ny-counties.png)
  
7.  Clique em **Avançar**.  
  
8.  Na página **Escolher as opções de dados espaciais e de exibição de mapa** , aceite os padrões e clique em **Avançar**. 
 
    Por padrão, os elementos do mapa de uma galeria de mapas são inseridos automaticamente na definição do relatório.  
  
9. Na página **Escolher visualização do mapa** , verifique se **Mapa Básico** está selecionado e clique em **Avançar**.  
  
11. Na página **Escolher o tema da cor e a visualização dos dados** , selecione a opção **Exibir rótulos** .  
  
12. Se estiver selecionada, desmarque a opção **Mapa de cor única** .  
  
13. Na lista suspensa **Campo de dados** , clique em **#COUNTYNAME**. O painel Visualização de Mapa no assistente exibe os seguintes itens:  
  
    -   Um título com o texto **Título do Mapa**.  
  
    -   Um mapa que exibe os municípios em Nova York onde cada município é uma cor diferente e o nome do município aparece onde possível na área do município.  
  
    -   Uma legenda que contém um título e uma lista de itens de 1 a 5.  
  
    -   Uma escala de cores que contém valores de 0 a 160 e nenhuma cor.  
  
    -   Uma escala de distância que exibe quilômetros (km) e milhas (mi).  
    
    ![report-builder-map-choose-color-theme](../reporting-services/media/report-builder-map-choose-color-theme.png)
  
14. Clique em **Concluir**.  
  
    O mapa é adicionado à superfície de design.  
  
13. Selecione o texto “Título do Mapa” e digite **Vendas por Loja** > ENTER.  

15. Clique duas vezes no mapa para exibir o **Painel Camadas do Mapa**. O **Painel Camadas do Mapa** mostra uma camada de polígono, PolygonLayer1, do tipo de camada **Inserido**. Cada região é um elemento do mapa inserido nessa camada.  
  
    > [!NOTE]  
    > Se o painel **Camadas do Mapa** não estiver visível, talvez ele esteja fora da exibição atual. Use a barra de rolagem na parte inferior da janela do modo Design para alterar sua exibição. Como alternativa, na guia **Exibir**, desmarque a opção **Dados do Relatório** para fornecer mais área de superfície de design.   

15. Selecione a seta ao lado de PolygonLayer1 > **Propriedades do polígono**.

16. Na guia **Fonte**, altere a cor para **Cinza-claro**.

17. Na guia **Início** > **Executar** para visualizar o relatório.  
  
    ![report-builder-map-first-preview](../reporting-services/media/report-builder-map-first-preview.png)
  
O relatório renderizado exibe o título do mapa, o mapa e a escala de distância. Os municípios estão em uma camada do polígono de mapas. Cada município é um polígono que varia por cor de uma paleta de cores, mas as cores não estão associadas a nenhum dado. A escala de distância exibe distâncias em quilômetros e em milhas.  
  
A legenda de mapa e a escala de cores ainda não são exibidos porque não há dados analíticos associados a cada município. Você adicionará dados analíticos posteriormente neste tutorial.  
  
## <a name="PointLayer"></a>2. Adicionar uma camada de ponto de mapa para exibir locais de loja  
Nesta seção, você usa o assistente de camadas do mapa para adicionar uma camada de pontos que exibe a localização das lojas.  
  
> [!NOTE]  
> Neste tutorial, a consulta contém os valores de dados e, portanto, ela não precisa de uma fonte de dados externa. Isso torna a consulta bastante longa. Em um ambiente empresarial, uma consulta não conteria os dados. Isso é apenas para fins de aprendizado.  
  
### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>Para adicionar uma camada de ponto com base em uma consulta espacial do SQL Server  
  
1.  Na guia **Executar** > **Design** para mudar de volta para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camadas do Mapa** . Na barra de ferramentas, clique o **Assistente de nova camada** botão ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard"). 

    ![report-builder-map-new-layer-wizard-icon](../reporting-services/media/report-builder-map-new-layer-wizard-icon.png) 
  
3.  Na página **Escolher uma fonte de dados espaciais** , selecione **Consulta espacial do SQL Server**e clique em **Avançar**.  
  
4.  Na página **Escolher um conjunto de dados com dados espaciais do SQL Server** , clique em **Adicionar um novo conjunto de dados com dados espaciais do SQL Server** > **Avançar**.  
  
5.  Na página **Escolha uma conexão com uma fonte de dados espaciais do SQL Server** , selecione uma fonte de dados existente ou navegue até o servidor de relatório e selecione uma fonte de dados.  

    > [!NOTE]  
    > A fonte de dados escolhida não tem importância, contanto que você tenha permissões suficientes. Você não obterá dados da fonte de dados. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Clique em **Avançar**.  
  
7.  Na página **Crie uma Consulta** , clique em **Editar como Texto**.  
  
8.  Copie o seguinte texto e cole-o no painel de consulta:  
  
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
    UNION ALL Select 124 as StoreKey, 'Contoso Buffalo Store' as StoreName, 700 as SellingArea, 'Buffalo' as City, 'Erie' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-78.8784 42.8864)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. Na barra de ferramentas do designer de consultas, clique em **Executar** (**!**).  
  
    O conjunto de resultados contém sete colunas que representam um conjunto de lojas no estado de Nova York que vendem bens de consumo. Aqui está uma lista, com explicações para aquelas que podem não ser óbvias: 
    *   **StoreKey**: um identificador de repositório.  
    *   **StoreName**.
    *   **SellingArea**: a área disponível para exibição do produto, que varia de 455 pés quadrados a 1.125 pés quadrados.
    *   **City**.
    *   **County**.
    *   **Sales**: Total de vendas. 
    *   **SpatialLocation**: local em longitude e latitude. 

    ![report-builder-map-design-query](../reporting-services/media/report-builder-map-design-query.png) 
  
10. Clique em **Avançar**.  
  
    O conjunto de dados de relatório chamado DataSet1 é criado para você. Após a conclusão do assistente, você poderá ver sua coleção de campos no painel Dados do Relatório.  
  
11. Na página **Escolher as opções de dados espaciais e de exibição de mapa** , verifique se o **Campo espacial** é **SpatialLocation** e se o **Tipo de camada** é **Ponto**. Aceite os outros padrões nesta página.  
  
    A exibição de mapa mostra círculos para marcar a localização de cada loja.  
  
12. Clique em **Avançar**.  
  
13. Na página Escolher visualização de mapa, clique em **Mapa de bolha** para obter um tipo de mapa que exibe marcadores que variam em tamanho, de acordo com os dados. Clique em **Avançar**.  
  
14. Na página **Escolher o conjunto de dados analíticos** , clique em DataSet1 e em **Avançar**. Esse conjunto de dados contém dados analíticos e dados espaciais que serão exibidos na nova camada de ponto.   
  
16. Na página **Escolher tema de cor e dados de visualização** , selecione **Usar tamanhos de bolha para visualizar dados**.  
  
17. Em **Campo de dados**, selecione `[Sum(SellingArea)]` para variar o tamanho da bolha conforme o tamanho da área que uma loja reserva para exibir os produtos.  
  
18. Selecione **Exibir rótulos**e, em **Campo de dados**, selecione `[City]`.

18. Clique em **Concluir**.  
  
    A camada do mapa é adicionada ao relatório. A legenda exibe os tamanhos da bolha com base nos valores de SellingArea.  
  
 19. Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . O painel **Camada do Mapa** exibe uma nova camada, PointLayer1, com o tipo de fonte de dados espaciais **DataRegion**.  
  
19. Adicione um título à legenda. Na legenda, selecione o texto **Título**, digite **Área de exibição (pés quadrados)** e pressione ENTER.  
  
21. No **Painel de Camadas do Mapa**, clique na seta ao lado de PointLayer1 e clique em **Propriedades do Ponto**.  

    ![report-builder-map-point-properties](../reporting-services/media/report-builder-map-point-properties.png)
  
22. Na guia **Fonte** , escolha o estilo **Negrito** e o tamanho **10 pt**.

    ![report-builder-map-point-properties-font](../reporting-services/media/report-builder-map-point-properties-font.png)
  
23. Na guia **Geral** , selecione **Inferior** para **Posicionamento**.

24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. Clique em **Executar** para visualizar o relatório.  

    ![report-builder-map-city-names](../reporting-services/media/report-builder-map-city-names.png)
  
    O mapa exibe os locais de lojas no estado de Nova York. O tamanho do marcador para cada loja se baseia na área de exibição. Foram calculados cinco intervalos de área de exibição automaticamente para você.


  
## <a name="LineLayer"></a>3. Adicionar uma camada de linha de mapa para exibir uma rota  
Use o assistente de camada do mapa para adicionar uma camada do mapa que exibe uma rota entre duas lojas. Neste tutorial, o caminho é criado de três locais de loja. Em um aplicativo comercial, o caminho pode ser a melhor rota entre lojas.  
  
### <a name="to-add-a-line-layer-to-map"></a>Para adicionar uma camada de linha ao mapa  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . Na barra de ferramentas, clique o **Assistente de nova camada** botão ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard").  
  
3.  Na página **Escolher uma fonte de dados espaciais** , selecione **Consulta espacial do SQL Server** e clique em **Avançar**.  
  
4.  Na página **Escolher um conjunto de dados com dados espaciais do SQL Server** , clique em **Adicionar um novo conjunto de dados com dados espaciais do SQL Server** e clique em **Avançar**.  
  
5.  Em **Escolher uma conexão com uma fonte de dados espaciais do SQL Server**, selecione a fonte de dados que você usou no primeiro procedimento.  
  
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

    ![report-builder-map-line](../reporting-services/media/report-builder-map-line.png)
  
     O mapa exibe uma nova camada de linha com o tipo de fonte de dados espaciais **DataRegion**. Neste exemplo, os dados espaciais vêm de um conjunto de dados, mas nenhum dado analítico é associado à linha.  

## <a name="adjust-the-zoom"></a>Ajustar o zoom
1. Se não conseguir ver o estado de Nova York inteira, você poderá ajustar o zoom. Com o mapa selecionado, no painel Propriedades, consulte as propriedades de **MapViewport** . 

15. Expanda a seção **Exibir** e expanda **Exibir** para que você possa ver a propriedade **Zoom** . Defina-o como **125**. 

    ![report-builder-map-zoom](../reporting-services/media/report-builder-map-zoom.png)

      Este é o percentual de zoom. Em 125%, você deverá ver o estado inteiro.
  
## <a name="TileLayer"></a>4. Adicionar um plano de fundo lado a lado do Bing Maps  
Nesta seção, você adiciona uma camada do mapa que exibe uma tela de fundo do bloco do Bing Mapas.  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . Na barra de ferramentas, clique em **Adicionar camada** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer").  
  
3.  Na lista suspensa, clique em **Camada do Bloco**.  
  
    A última camada no painel **Camada do Mapa** é TileLayer1. Por padrão, a camada lado a lado exibe o estilo de mapa rodoviário.  
  
    > [!NOTE]  
    > No assistente, você também pode adicionar uma camada lado a lado na página **Escolher as opções de dados espaciais e de exibição do mapa** . Para fazer isso, selecione **Adicionar um plano de fundo do Bing Maps a esta exibição de mapa**. Em um relatório renderizado, o plano de fundo lado a lado exibirá itens lado a lado do Bing Maps para o visor e o nível de zoom do mapa atual.  
  
4.  Clique na seta ao lado de TileLayer1 > **Propriedades do Bloco**.  
  
5.  Na guia **Geral**, em **Tipo**, selecione **Aéreo**. A vista aérea não contém texto.  

    ![report-builder-map-bing-aerial](../reporting-services/media/report-builder-map-bing-aerial.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Transparent"></a>5. Tornar uma camada transparente  
Nesta seção, para permitir que os itens em uma camada sejam exibidos por meio de outra camada, você ajusta a ordem e a transparência das camadas para o efeito desejado. Você começa com a primeira camada criada, PolygonLayer1. 
  
1.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa**.  
  
3.  Clique na seta ao lado de PolygonLayer1 > **Dados da Camada**. A caixa de diálogo **Mapear Propriedades de Camada do Polígono** aparece.  
  
4.  Na guia **Visibilidade** , em **Transparência (percentual)**, digite **30**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     A superfície de design exibe os municípios como semitransparentes.  

    ![report-builder-map-transparency](../reporting-services/media/report-builder-map-transparency.png)
  
## <a name="Vary"></a>6. Variar as cores de municípios com base em vendas  
Cada município na camada do polígono tem uma cor diferente porque o processador de relatório atribui um valor de cor automaticamente da paleta de cores com base no tema que você escolheu na última página do assistente de mapa.  
  
Nesta seção, você especifica uma regra de cor para associar cores específicas a um intervalo de vendas de lojas de cada condado. As cores vermelho-amarelo-verde indicam vendas altas-médias-baixas relativas. Formate a escala de cores para mostrar a moeda. Exiba os intervalos de vendas anuais em uma nova legenda. Para municípios que não contêm lojas, não use nenhuma cor para mostrar que não há dados associados.  
  
### <a name="Relationship"></a>6a. Criar um relacionamento entre dados espaciais e analíticos  
Para variar as formas do condado por cor, com base em dados analíticos, primeiro você precisa associar os dados analíticos aos dados espaciais. Neste tutorial, você usará o nome do município para correspondência. 
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camadas do Mapa** .  
  
3.  Clique na seta ao lado de PolygonLayer1 e clique em **Dados da Camada**. A caixa de diálogo **Mapear Propriedades de Camada do Polígono** aparece.  
  
4.  Na guia **Dados analíticos** , em **Conjunto de dados analíticos**, selecione DataSet1. Esse conjunto de dados foi criado pelo assistente quando você criou a consulta de dados espaciais para os condados.  
  
6.  Em **Campos a serem associados**, clique em **Adicionar**. Uma nova linha será adicionada.  
  
7.  Em **De conjunto de dados espaciais**, clique em COUNTYNAME.  
  
8.  Em **De conjunto de dados analíticos**, clique em [County].  

    ![report-builder-map-county-colors](../reporting-services/media/report-builder-map-county-colors.png)
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Visualize o relatório.  

    ![report-builder-map-county-highlight](../reporting-services/media/report-builder-map-county-highlight.png)
  
Ao especificar um campo de correspondência com base na fonte de dados espaciais e no conjunto de dados analítico, você permite que o processador de relatório agrupe dados analíticos com base nos elementos do mapa. Um elemento de mapa com ligação de dados tem uma correspondência para os valores especificados.  
  
Cada município que contém uma loja tem uma cor baseada na paleta de cores para o estilo escolhido no assistente. Os outros condados são cinza.  
  
### <a name="ColorRules"></a>6b. Especificar as regras de cores para polígonos  
Para criar uma regra que varia a cor de cada município baseada em vendas da loja, você deve especificar os valores de intervalo, o número de divisões dentro daquele intervalo que você deseja exibir, e as cores a serem usadas.  
  
#### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>Para especificar regras de cores para todos os polígonos com dados associados  
  
1.  Alterne para o modo Design.  
  
2.  Clique na seta ao lado de PolygonLayer1 e clique em **Regra de Cor do Polígono**. A caixa de diálogo **Mapear Propriedades de Regras de Cor** é aberta. Observe que a opção de regra de cor **Visualizar dados usando a paleta de cores** está selecionada. Esta opção foi definida no assistente.  
  
3.  Selecione **Visualizar dados usando intervalos de cores**. A opção da paleta é substituída pelas opções de cor inicial, cor intermediária e cor final.  
  
4.  Defina valores de intervalo para vendas por município. Em **Campo de dados**, na lista suspensa, selecione `[Sum(Sales)]`.  
  
5.  Para alterar o formato para exibir moeda em milhares, altere a expressão para o seguinte: `=Sum(Fields!Sales.Value)/1000`  
  
6.  Altere **Cor inicial** para **Vermelho**.  
  
7.  Altere **Cor final** para **Verde**.  
  
    **Vermelho** representa baixos valores de vendas, **Amarelo** representa valores de vendas intermediários e **Verde** representa valores de vendas altos. O processador de relatório calcula um intervalo de cores com base nesses valores e as opções que você escolhe na página **Distribuição** .  
    
    ![report-builder-map-county-color-rules](../reporting-services/media/report-builder-map-county-color-rules.png)
  
8.  Clique em **Distribuição**.  
  
9. Verifique se o tipo de distribuição é **Ideal**. Para a expressão da etapa 5, a distribuição ideal divide os valores em subintervalos que equilibram o número de itens em cada intervalo e abrangem cada intervalo.  
  
10. Aceite os valores padrão para outras opções nesta página. Quando você selecionar o tipo de distribuição ideal, o número de subintervalos será calculado quando o relatório for executado.  
  
11. Clique em **Legenda**.  
  
12. Em **Opções de escala de cores**, verifique se a opção **Mostrar em escala de cores** está selecionada.  
  
13. Em **Mostrar nesta legenda**, selecione a linha em branco na lista suspensa. Por enquanto, você mostrará apenas os intervalos de cores na escala de cores.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

15. Visualize o relatório.

    ![report-builder-map-county-color-rule-preview](../reporting-services/media/report-builder-map-county-color-rule-preview.png)
  
    A escala de cores exibe quatro cores: vermelho, laranja, amarelo e verde. Cada cor representa um intervalo de vendas que é calculado automaticamente com base nas vendas por município.  
  
### <a name="ColorScale"></a>6c. Formatar os dados na escala de cores como moeda  
Por padrão, os dados têm um formato geral. Nesta seção, você aplica formatos personalizados.  
  
1. Alterne para o modo Design.  

2. Selecione a escala de cores. Na guia **Início** > seção **Número**, clique em **Moeda**.  
  
4.  Ainda na seção **Número**, clique no botão **Diminuir Decimal** duas vezes.  
  
    A escala de cores exibe as vendas anuais no formato de moeda para cada intervalo.  
  
### <a name="NewLegend"></a>6d. Adicionar um título à legenda   
  
1.  Com a escala de cores ainda selecionada, no painel Propriedades, você vê as propriedades de **MapColorScale**. 
  
2. Expanda a seção Título e, na propriedade Legenda, digite **Vendas (Milhares)**.

3. Altere a propriedade TextColor para **Branco**.  

    ![report-builder-map-color-scale-title](../reporting-services/media/report-builder-map-color-scale-title.png)
  
8.  Visualize o relatório.  
  
Os municípios que têm lojas e vendas associadas são exibidos de acordo com as regras de cores. Municípios que não têm nenhuma venda não têm cores.  
  
### <a name="NoData"></a>6f. Alterar a cor dos municípios para os quais não há dados  
Você pode definir as opções de exibição padrão para todos os elementos de mapas em uma camada. As regras de cores têm precedência sobre essas opções de exibição.  
  
#### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>Para definir as propriedades de exibição para todos os elementos em uma camada  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** .  
  
3.  Clique na seta para baixo em PolygonLayer1 e clique em **Propriedades do Polígono**. 

     ![report-builder-map-polygon-layer-properties](../reporting-services/media/report-builder-map-polygon-layer-properties.png)

     A caixa de diálogo **Mapear Propriedades do Polígono** aparece. As opções de exibição definidas nesta caixa de diálogo se aplicam a todos os polígonos na camada antes de as opções de exibição baseadas em regras serem aplicadas.  
  
4.  Na guia **Preenchimento** , verifique se o estilo de preenchimento é **Sólido.** Gradações e padrões se aplicam a todas as cores.  
  
6.  Em **Cor**, selecione **Azul-metálico-claro**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Visualize o relatório.  
  
Condados sem dados associados são exibidos em azul acinzentado. Somente os condados com dados analíticos associados têm as cores **Vermelho** a **Verde** nas regras de cores especificadas.  
  
## <a name="CustomPoint"></a>7. Adicionar um ponto personalizado  
Para representar uma nova loja que ainda não foi construída, nesta seção, você especifica um ponto com o tipo de marcador **Estrela**.  
  
1.  Alterne para o modo Design.  
  
2.  Clique duas vezes no mapa para exibir o painel **Camada do Mapa** . Na barra de ferramentas, clique em **Adicionar camada**![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer"), em seguida, clique em **camada de ponto**.    
  
    Uma nova camada de ponto é adicionada ao mapa. Por padrão, a camada de ponto tem o tipo de dados espacial **Inserido**.  
  
3.  Clique na seta em PointLayer2 > **Adicionar Ponto**.  
  
4.  Mova o ponteiro sobre o visor do mapa. O cursor se transforma em uma cruz.  
  
5.  Clique no local no mapa em que você deseja adicionar um ponto. Neste tutorial, clique em um local no condado de Oneida. Um ponto marcado por um círculo é adicionado à camada no local em que você clicou. Por padrão, o ponto é selecionado.  

    ![report-builder-map-custom-point](../reporting-services/media/report-builder-map-custom-point.png)
  
6.  Clique com o botão direito do mouse no ponto adicionado e clique em **Propriedades de Ponto Inserido**.  
  
7.  Selecione **Substituir opções de ponto para esta camada**. Páginas adicionais aparecem na caixa de diálogo. Os valores que você definiu aqui têm precedência sobre as opções de exibição da camada ou para regras de cores.  

    ![report-builder-map-custom-point-general](../reporting-services/media/report-builder-map-custom-point-general.png)
  
8.  Na guia **Marcador** , em **Tipo de marcador**, selecione **Estrela**.  

10. Altere **Tamanho de marcador** para **18 pt**.
  
3.  Na guia **Rótulos** , em **Texto de rótulo**, digite **Nova Loja**.  
  
5.  Em **Posicionamento**, clique em **Superior**.  

13. Na guia **Fonte** , escolha o tamanho da fonte **10 pt** e **Negrito**.

    ![report-builder-map-custom-point-font](../reporting-services/media/report-builder-map-custom-point-font.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Visualize o relatório.  
  
O rótulo aparece acima do local da loja.  

![report-builder-map-custom-point-new-store](../reporting-services/media/report-builder-map-custom-point-new-store.png)
  
## <a name="CenterView"></a>8. Centralizar e redimensionar o mapa   
Nesta seção, você aprende a alterar o centro do mapa e outra maneira de alterar o nível de zoom.  
 
1.  Alterne para o modo Design.  

1.  Selecione o mapa, clique com o botão direito do mouse e clique em **Propriedades do Visor**.  
  
2.  Na guia **Centralizar e Aplicar Zoom** , verifique se a opção **Definir um centro de exibição e um nível de zoom** está selecionada.  

4. Defina **Nível de zoom (percentual)** como **125**.
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Clique no mapa e arraste para centralizá-lo no local desejado.  
  
6.  Você também pode usar a roda do mouse para alterar o nível de zoom.  
  
7.  Visualize o relatório.  
  
No modo Design, o mapa na superfície de exibição e a exibição se baseiam em dados de exemplo. No relatório renderizado, a exibição de mapa é centralizada na exibição especificada.  
  
## <a name="Title"></a>9. Adicionar um título de relatório  
  
1.  Alterne para o modo Design.
  
1.  Na superfície de design, clique em **Clique para adicionar título**.  
  
2.  Digite **Vendas nas Lojas de Nova York** e clique fora da caixa de texto.  
  
Esse título aparecerá na parte superior do relatório. Os itens na parte superior do corpo do relatório quando não há cabeçalho de página definido são os equivalentes de um cabeçalho de relatório.  
  
## <a name="Save"></a>10. Salvar o relatório  
  
1.  No modo Design ou Visualização, no menu **Arquivo** > **Salvar Como**.
 
3.  Em **Nome**, digite **Vendas nas Lojas de Nova York**.  

3. Salve-o no computador local ou em um servidor do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .
  
4. Clique em **Salvar**. 

Se você salvá-lo em um servidor de relatório, poderá exibi-lo nele.

![report-builder-map-in-portal](../reporting-services/media/report-builder-map-in-portal.png) 
  
## <a name="next-steps"></a>Próximas etapas  
Isso conclui o passo a passo da adição de um mapa ao seu relatório.  
  
Para obter mais informações, consulte [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
[Tutoriais do Construtor de Relatórios](../reporting-services/report-builder-tutorials.md)  
[Construtor de Relatórios no SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
[Assistente de Mapa e Assistente de Camada do Mapa &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
[Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  


