---
title: "Relatórios móveis do SQL Server: Passo a passo completo | Microsoft Docs"
ms.custom: 
ms.date: 11/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e198575e-b154-4342-b944-2bf19ec49bfd
caps.latest.revision: 
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 3233c1433d1e09038d66af3db7e84a732e81926a
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="sql-server-mobile-reports-end-to-end-walk-through"></a>Relatórios móveis do SQL Server: Passo a passo completo
Realize a criação de relatórios móveis para qualquer tamanho de tela com o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] no portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , e exiba-os nos aplicativos móveis do Power BI.

Crie relatórios móveis em uma superfície de design com linhas de grade e colunas ajustáveis e elementos flexíveis de relatório móvel. Conectar-se a várias fontes de dados locais ou carregar pastas de trabalho do Excel para criar relatórios móveis. Salve seus relatórios em um portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] e exiba-os em um navegador ou em aplicativos móveis do Power BI.  
  
Este artigo orienta você pela:   
  
- Criação de uma fonte de dados e conjunto de dados compartilhados no portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] , usando o banco de dados AdventureWorks como uma fonte de dados de exemplo.  
- Criar um relatório móvel do Reporting Services no [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]  
- Publicação do relatório móvel no portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] .  
- Exibição do relatório móvel no aplicativo móvel do Power BI.  
  
## <a name="before-we-start"></a>Antes de começar  
Para acompanhar, você precisa destes produtos:  
  
* Para criar fontes de dados e KPIs e publicar relatórios móveis e conjuntos de dados, você precisa ter acesso a um [!INCLUDE[ssRSCurrent_md](../install-windows/install-reporting-services-native-mode-report-server.md).  
* Para [criar conjuntos de dados compartilhados](../install-windows/install-report-builder.md).  
* Para criar relatórios móveis, [instale o Publicador de Relatórios Móveis do SQL Server](http://go.microsoft.com/fwlink/?LinkId=717766).  
* [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
*  OU: banco de dados de exemplo do World Wide Importers, disponível na página [Amostras do Microsoft SQL Server](../../sample/microsoft-sql-server-samples.md).
* Para exibir o resultado: 
  *   [Inscreva-se no serviço do Power BI](http://go.microsoft.com/fwlink/?LinkID=513879) e
  *  [Baixe o aplicativo móvel do Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) em seu dispositivo móvel: iOS, telefone com Android ou dispositivo com Windows 10.  

  
## <a name="create-a-shared-data-source"></a>Criar uma fonte de dados compartilhados  
  
Você pode criar uma fonte de dados compartilhada para seus relatórios móveis a partir de qualquer uma das fontes de dados com suporte do Reporting Services. Consulte a [lista de fontes de dados com suporte](../report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
1. De seu portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] , clique em **Nova** > **Fonte de Dados**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
3. Insira as informações da fonte de dados > **OK**.  
  
    Por padrão, as fontes de dados não são exibidas no portal.    
   
5. Para exibir as fontes de dados, clique em **Exibir** > **Fonte de Dados**.  
  
   ![PBI_SSMRP_DisplayDataSources](../../reporting-services/mobile-reports/media/pbi-ssmrp-displaydatasources.png)  
   
6. Agora você vê a fonte de dados no portal do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] .  
  
   ![PBI_SSMRP_PortlDataSource](../../reporting-services/mobile-reports/media/pbi-ssmrp-portldatasource.png)  
  
Leia mais sobre as [fontes de dados compartilhadas no Reporting Services](../report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
   
## <a name="shared-dataset">Criar um conjunto de dados compartilhado</a>  
  
Use uma ferramenta de cliente existente do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] , como o Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull_md](../../includes/ssbidevstudiofull-md.md)], para criar o conjunto de dados compartilhado.  Este passo a passo usa [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)]. [Instale o Construtor de Relatórios](https://msdn.microsoft.com/library/ff519551.aspx)ou o inicie em seu portal na Web. Você criará três conjuntos de dados, um para: o valor do KPI, a tendência do KPI e outro com mais campos para o relatório móvel do Reporting Services.     
  
1. De seu portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] , clique em **Novo** > **Relatório Paginado** para começar [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)].  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)   
2. Clique em **Novo Conjunto de Dados**.  
  
   ![PBI_SSMRP_RBNewDataset](../../reporting-services/mobile-reports/media/pbi-ssmrp-rbnewdataset.png)  
   
3. Clique em **Procurar outras fontes de dados**.  
   
4. No campo Nome, digite o nome do servidor onde você salvou a fonte de dados, neste formato:   
   
   Nome: http://*localhost*/ReportServer  
   Itens do tipo: Fontes de dados (*.rsds)  
   
5. Clique em **Abrir**e navegue até a fonte de dados que você criou no servidor.  
   
6. Selecione a fonte de dados e clique em **Abrir** novamente.    
  
7. Crie o conjunto de dados em [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)].  
  
   ![PBI_SSMRP_RB_QueryDesignr600](../../reporting-services/mobile-reports/media/pbi-ssmrp-rb-querydesignr600.png)  
   
8. Ao concluir, salve o conjunto de dados no servidor de relatório do [!INCLUDE[PRODUCT_NAME](../../includes/ssrs.md)] .    
   
Agora você pode usar o conjunto de dados como base para seus relatórios móveis e KPIs.  Você pode criar vários conjuntos de dados com base na mesma fonte de dados. E pode criar vários relatórios móveis e KPIs com base nesses conjuntos de dados compartilhados.   
  
## <a name="create-KPI">Criar um KPI</a>  
Crie KPIs direitamente no portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] .    
  
1. No canto superior direito do portal da Web, clique em **Novo** > **Novo KPI**.   
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
      
   Na tela de criação do KPI, você pode inserir manualmente os valores ou usar um conjunto de dados compartilhado.    
2. Altere **Valor** de **Definido manualmente** para **Campo de conjunto de dados**.  
   
   ![PBI_SSMRP_KPI_DatasetField](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpi-datasetfield.png)  
   
3. Clique nas reticências (**...**) na caixa **Selecionar campo de conjunto de dados** e selecione um conjunto de dados da etapa anterior.  
   
   ![PBI_SSMRP_KPIPickDataset](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipickdataset.png)  
   
4. Escolha o campo no conjunto de dados.    
   
   ![PBI_SSMRP_KPIPickField](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipickfield.png)  
     
5. Escolha a agregação desejada. Os KPIs só podem exibir um número, para que o campo seja agregado e mostre esse número.

   ![reporting-services-kpi-pick-aggregation](../../reporting-services/mobile-reports/media/reporting-services-kpi-pick-aggregation.png)

6. Clique em **OK**.

7. Na caixa **Conjunto de tendências** clique em **Tendência de conjunto de dados**.  
  
6. Na caixa **Selecionar tendência do conjunto de dados** clique no botão de reticências (**...**)  
   
7. Selecione um campo e clique em **OK**.  

   ![PBI_SSMRP_KPIPickTrend](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipicktrend.png)  
  
8. Nomeie o KPI e escolha um tipo de visualização e clique em **Criar**.   
  
   O KPI será exibido no portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] .  
   
    ![PBI_SSMRP_NewKPI](../../reporting-services/mobile-reports/media/pbi-ssmrp-newkpi.png)  
    
## <a name="create-mobile-report">Criar um relatório móvel do Reporting Services</a>  
   
Para criar um relatório móvel do Reporting Services, [instale o Publicador de Relatório do SQL Server Mobile](http://go.microsoft.com/fwlink/?LinkId=717766)ou o inicie no portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . 

Ao abrir pela primeira vez o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)], você vê uma tela em branco na qual é possível criar relatórios móveis. Você pode começar criando primeiro os elementos visuais ou começar com seus dados. Se você criar os elementos visuais primeiro, o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] gerará automaticamente os dados simulados que estão vinculados ao relatório e será alterado dinamicamente à medida que você altera suas seleções visuais. Tente isso.   
  
## <a name="start-with-the-visuals"></a>Começar com os elementos visuais  
  
1. De seu portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] , clique em **Novo** > **Relatório Móvel** para começar [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)

   [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] é aberto na grade de layout mestre.  
  
2. Na guia **Layout** , role para baixo até a seção Gráficos.  
  
   ![PBI_SSMRP_LayoutTabCharts2](../../reporting-services/mobile-reports/media/pbi-ssmrp-layouttabcharts2.png)  
  
2. Arraste o **Tree Map** para a grade e arraste o canto inferior direito canto para deixá-lo com três colunas e três linhas.  
  
   ![PBI_SSMRP_TreeMap](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemap.png)  
  
3. Você pode ver suas propriedades visuais na parte inferior. Talvez seja necessário rolar lateralmente para ver todas elas.   
  
   ![PBI_SSMRP_TreeMapVisProps](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemapvisprops.png)  
  
4. Com o visual de mapa de árvore selecionado, selecione a guia **Dados** no canto superior esquerdo.   
  
   Agora você pode ver os campos e valores simulados que o [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] gerou, e pode ver o que representam o tamanho e a cor no mapa de árvore.  
  
   ![PBI_SSMRP_TreeMapDataProps](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemapdataprops.png)  
  
6. Clique na guia **Layout** .  
  
7. Clique na engrenagem de Opções ![PBI_SSMRP_Cog](../../reporting-services/mobile-reports/media/pbi-ssmrp-cog.png) no canto superior direito do mapa de árvore para ver o menu que ela contém.   
  
   ![PBI_SSMRP_OptionsWheel](../../reporting-services/mobile-reports/media/pbi-ssmrp-optionswheel.png)  
  
8. Clique na seta no centro da roda para fechá-la.  
  
## <a name="add-your-own-data"></a>Adicionar seus próprios dados  
  
1. Alterne para a guia **Dados** .    
   
2. Para adicionar seus próprios dados, clique em **Adicionar Dados** no canto superior direito e navegue até seus dados.    
  
3. Você pode usar os dados de uma pasta de trabalho do Excel local, mas, neste caso, eles são do conjunto de dados compartilhado no portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] . Você verá uma mensagem de "Servidor adicionado".  
  
4. Selecione o servidor e selecione o conjunto de dados que você criou.  
   
3. Novamente na guia **Dados** , no painel **Propriedades de Dados** , altere **Tamanho Representa**, **Cor Representa**e outras propriedades para os campos em seus próprios dados. 
   
   *  **Tamanho Representa**, **Cor Representa**e **Valor Central Personalizado** precisam ser campos com valores numéricos. 
   *  **Agrupar por** é uma categoria, portanto, é um campo de texto.
   
   ![ssrs-mobile-report-data-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-data-properties.png)
   
6. Selecione **Visualizar** para ver o mapa de árvore atualizado com seus dados.  

## <a name="add-a-gauge-to-your-mobile-report"></a>Adicionar um medidor ao seu relatório móvel

Vamos adicionar um medidor para ver como as vendas anuais até o momento se comparam com as vendas do ano passado, usando o mesmo conjunto de dados.

1. Na guia Layout, arraste um metade da rosca até a tela. Coloque-a sob o mapa de árvore e arraste o canto inferior direito para deixá-lo com três quadrados de largura por dois quadrados de altura. 

2. Novamente, ela começa com dados simulados. 

   Observe que em **Propriedades visuais**, por padrão **Valores maiores são melhores**e o **Rótulo delta** é uma **Porcentagem de destino**. Há **Paradas de intervalo** que você pode alterar, mas por enquanto elas estão certas.

   ![ssrs-mobile-report-donut-visual-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-visual-properties.png)
   
3. Na guia **Dados** , selecione a tabela com os dados e selecione o campo **Valor Principal** e o campo ao qual você deseja compará-lo em **Valor de Comparação**.

4. Você pode escolher agregações diferentes para obter um número para o **Valor Principal** e outro para o **Valor de Comparação**. Por padrão, é uma soma.

   ![ssrs-mobile-report-donut-sum](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-sum.png)

5. Selecione **Visualizar** para ver a aparência. 

   ![ssrs-mobile-report-donut-preview](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-preview.png)

## <a name="add-a-selection-list-as-a-filter"></a>Adicionar uma lista de seleção como um filtro

As listas de seleção atuam como segmentações de dados no Power BI e Excel. Podemos adicionar uma para filtrar os outros elementos visuais no relatório móvel.

1. Na guia **Layout** , arraste uma lista de seleção à direita do mapa de árvore e arraste o canto inferior direito para deixá-lo com dois quadrados de largura e com a altura da tela, de cinco quadrados. 

   ![ssrs-mobile-report-selection-list](../../reporting-services/mobile-reports/media/ssrs-mobile-report-selection-list.png)

2. Na guia **Dados** , **Propriedades de dados**, defina **Chaves** e **Rótulos** para um campo em que você deseja filtrar seus dados.

   ![ssrs-mobile-report-selection-list-data-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-selection-list-data-properties.png)
   
## <a name="create-a-mobile-report-for-phones"></a>Criar um relatório móvel para telefones  
  
Agora que você criou elementos visuais no layout mestre, poderá criar um relatório móvel com um layout otimizado especificamente para os usuários de telefones.    
  
1. No canto superior direito, clique no ícone da tela > **Telefone**.  
  
2. Na guia Layout, em **Instâncias de Controle**, veja os dois gráficos que você criou.   
  
3. Arraste o mapa de árvore até a tela do telefone e deixe-o com quatro colunas de largura e com três linhas de altura.  
  

## <a name="save-your-mobile-report"></a>Salvar o relatório móvel  
Você pode salvar o relatório localmente ou em um portal da Web do [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] . Se você o salvar localmente, ele será salvo pelo [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] com dados em cache, para que você possa abri-lo e continuar trabalhando nele. Mas não é possível exibi-lo em um dispositivo móvel.   
  
1. Clique no ícone Salvar no canto superior esquerdo.   
   
2. Para compartilhá-lo com outras pessoas e exibi-lo em um dispositivo móvel, clique em **Salvar no Servidor**.  
  
3. No servidor, procure a pasta onde deseja salvar o relatório móvel.  
  
4. Clique em **Escolher Pasta** > **Salvar**.  
  
   Você receberá uma mensagem confirmando que o relatório foi salvo.  
    
   Depois de salvar, você pode retornar ao portal e ver a miniatura do relatório móvel.   
    
5. Toque na miniatura para ver o relatório no portal da Web.  
  
## <a name="view-your-report-on-the-web-portal"></a>Exibir o relatório no portal da Web

  
## <a name="view-your-report-on-a-mobile-device"></a>Exibir o relatório em um dispositivo móvel   
  
Para exibir seu relatório do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , primeiro você precisa:

*  [Inscrever-se no serviço do Power BI](http://go.microsoft.com/fwlink/?LinkID=513879), caso você ainda não tenha uma conta.
*  [Baixar o aplicativo móvel do Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) em seu dispositivo móvel.  

### <a name="view-your-mobile-report"></a>Exibir o relatório móvel
  
1.  Abra e entre no aplicativo do Power BI em seu dispositivo móvel.  
    
2.  Para exibir seus KPIs e relatórios móveis do Reporting Services, toque em **Reporting Services**.  
![PBI_iPad_GetStartedSm](../../reporting-services/mobile-reports/media/pbi-ipad-getstartedsm.png)  
  
3. Toque no ícone de opções ![PBI_iPad_OptionsIcon](../../reporting-services/mobile-reports/media/pbi-ipad-optionsicon.png) no canto superior esquerdo e toque em **Conectar-se ao Servidor**.  
  
   ![PBI_iPad_SSMRP_ConnectCrop](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-connectcrop.png)  
  
4. Dê um nome ao servidor e preencha o endereço do servidor, além de seu endereço de email e sua senha, neste formato:  
  
   ![PBI_iPad_SSMRP_ConnectContoso](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-connectcontoso.png)   
  
5.  Agora você pode ver o servidor na barra de navegação à esquerda.  
  
    ![PBI_iPad_SSMRP_LeftNavBiggr](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-leftnavbiggr.png)  
      
>**Dica**: toque no ícone de opções ![PBI_iPad_OptionsIcon](../../reporting-services/mobile-reports/media/pbi-ipad-optionsicon.png) a qualquer momento para alternar entre seus relatórios do Reporting Services no portal da Web do Reporting Services e seus painéis no serviço do Power BI.   
  
## <a name="view-kpis-and-mobile-reports-in-the-power-bi-app"></a>Exibir relatórios móveis e KPIs no aplicativo do Power BI  
  
Toque na guia **KPIs** ou **Relatórios Móveis** .   
  
![PBI_iPad_SSMRP_Portal](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-portal.png)  
  
- Toque em um KPI para vê-lo no modo de foco.  
  
    ![PBI_iPad_SSMRP_Tile](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-tile.png)  
  
- Toque em um relatório móvel para abrir e interagir com ele no aplicativo do Power BI.  
  
Os KPIs e os relatórios móveis são exibidos nas mesmas pastas que estão no portal da Web do Reporting Services.   
  
### <a name="see-also"></a>Consulte também  
 
-  Exibir [KPIs e relatórios móveis do Reporting Services no aplicativo de iPad](https://powerbi.microsoft.com/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI para iOS)  
-  Exibir [KPIs e relatórios móveis do Reporting Services no aplicativo de iPhone](https://powerbi.microsoft.com/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI para iOS)  
-  Exibir [KPIs e relatórios móveis do Reporting Services no aplicativo do Power BI para telefones Android](https://powerbi.microsoft.com/documentation/powerbi-mobile-android-kpis-mobile-reports)
-  Exibir [KPIs e relatórios móveis do Reporting Services no aplicativo do Power BI para dispositivos Windows 10](https://powerbi.microsoft.com/documentation/powerbi-mobile-win10-kpis-mobile-reports/)    
  
   

