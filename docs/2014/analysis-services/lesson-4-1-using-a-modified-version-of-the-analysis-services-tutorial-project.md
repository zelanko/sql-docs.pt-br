---
title: Usando uma versão modificada da análise de projeto do Tutorial de serviços | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 685aa217-de1b-4df2-bf22-095228c40775
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 763b1170ad0201c737e06e19c3dac8d58c6712ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729106"
---
# <a name="using-a-modified-version-of-the-analysis-services-tutorial-project"></a>Usando uma versão modificada do projeto do Tutorial do Analysis Services
  As demais lições neste tutorial tem como base uma versão aprimorada do projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você concluiu nas três primeiras lições. Foram adicionadas outras tabelas e cálculos nomeados à exibição da fonte de dados **Adventure Works DW 2012** e outras dimensões ao projeto. Essas novas dimensões foram adicionadas ao cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Além disso, um segundo grupo de medidas foi adicionado; ele contém medidas de uma segunda tabela de fatos. Esse projeto aprimorado permitirá que você continue a aprender como adicionar funcionalidades ao seu aplicativo de inteligência empresarial sem ter que repetir as ações já aprendidas.  
  
 Antes de continuar com o tutorial, você deve baixar, extrair, carregar e processar a versão aprimorada do projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  Use as instruções nesta lição para verificar se você realizou todas as etapas.  
  
## <a name="downloading-and-extracting-the-project-file"></a>Baixando e extraindo o Arquivo do Projeto  
  
1.  [Clique aqui](https://go.microsoft.com/fwlink/?LinkID=221866) para ir para a página de download que fornece os projetos de exemplo fornecidos neste tutorial. Os projetos do tutorial estão incluídos no download do **Tutorial do Analysis Services do SQL Server 2012** .  
  
2.  Clique em **Tutorial do Analysis Services do SQL Server 2012** para baixar o pacote que contém os projetos para este tutorial.  
  
     Por padrão, um arquivo .zip é salvo na pasta de Downloads. Você deve mover o arquivo .zip para um local que tem um caminho mais curto (por exemplo, crie uma pasta C:\Tutoriais para armazenar os arquivos).  Você pode então extrair os arquivos contidos no arquivo .zip. Se você tentar descompactar os arquivos da pasta de Downloads, que tem um caminho mais longo, só obterá a Lição 1.  
  
3.  Crie uma subpasta na unidade de raiz ou perto dela, por exemplo, C:\Tutorial.  
  
4.  Mova o arquivo **Analysis Services Tutorial SQL Server 2012.zip** para a subpasta.  
  
5.  Clique com o botão direito do mouse no arquivo e selecione **Extrair Tudo**.  
  
6.  Navegue até a pasta **Início da Lição 4** para localizar o arquivo **Analysis Services Tutorial.sln** .  
  
## <a name="loading-and-processing-the-enhanced-project"></a>Carregando e processando o projeto aprimorado  
  
1.  Na [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]diante a **arquivo** menu, clique em **fechar solução** para fechar os arquivos que não serão usados.  
  
2.  No menu **Arquivo** , aponte para **Abrir**e clique em **Projeto/Solução**.  
  
3.  Navegue até o local onde você extraiu os arquivos de projeto do tutorial.  
  
     Localize a pasta chamada **Início da Lição 4**e clique duas vezes em Analysis Services Tutorial.sln.  
  
4.  Implante a versão aprimorada do projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na instância local do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]ou em outra instância, e verifique se o processamento é concluído com êxito.  
  
## <a name="understanding-the-enhancements-to-the-project"></a>Entendendo os aprimoramentos do projeto  
 A versão aprimorada do projeto é diferente da versão do projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você concluiu nas três primeiras lições. As diferenças são descritas nas seções a seguir. Revise estas informações antes de continuar com as demais lições do tutorial.  
  
### <a name="data-source-view"></a>Exibição da Fonte de Dados  
 A exibição da fonte de dados no projeto aprimorado contém uma tabela de fatos adicional e quatro tabelas de dimensão adicionais do banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
 Observe que com dez tabelas nos dados de exibição da fonte de \<todas as tabelas > diagrama está ficando muito cheio. Isso dificulta a compreensão das relações entre as tabelas e a localização de tabelas específicas. Para solucionar esse problema, as tabelas são organizadas em dois diagramas lógicos: **Vendas pela Internet** e **Vendas do Revendedor** . Esses diagramas são organizados com base em uma única tabela de fato. Criar diagramas lógicos permite que você exiba e trabalhe com um subconjunto específico de tabelas em uma exibição de fonte de dado em vez de ter que exibir sempre todas as tabelas e suas relações em um único diagrama.  
  
#### <a name="internet-sales-diagram"></a>Diagrama Vendas pela Internet  
 O diagrama **Vendas pela Internet** contém as tabelas relacionadas à venda de produtos do [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] diretamente aos clientes pela Internet. As tabelas do diagrama são as quatro tabelas de dimensão e a tabela de fatos que você adicionou à exibição da fonte de dados **Adventure Works DW 2012** na Lição 1. Essas tabelas são as seguintes:  
  
-   **Geography**  
  
-   **Cliente**  
  
-   **Data**  
  
-   **Product**  
  
-   **InternetSales**  
  
#### <a name="reseller-sales-diagram"></a>Reseller Sales Diagram  
 O diagrama **Vendas do Revendedor** contém as tabelas relacionadas à venda de produtos do [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] por revendedores. Esse diagrama contém as sete tabelas de dimensão e uma tabela de fatos do banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] :  
  
-   **Reseller**  
  
-   **Promoção**  
  
-   **SalesTerritory**  
  
-   **Geografia**  
  
-   **Data**  
  
-   **Product**  
  
-   **Employee**  
  
-   **ResellerSales**  
  
 Observe que as tabelas **DimGeography**, **DimDate**e **DimProduct** são usadas nos diagramas **Vendas pela Internet** e **Vendas do Revendedor** . As tabelas de dimensão podem ser vinculadas a várias tabelas de fatos.  
  
### <a name="database-and-cube-dimensions"></a>Banco de dados e dimensões de cubo  
 O projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] contém cinco novas dimensões de bancos de dados, e o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] contém as mesmas cinco dimensões como dimensões de cubo. Essas dimensões foram definidas para terem hierarquias de usuário e atributos que foram modificados usando cálculos nomeados, chaves de membros de composição e pastas de exibição. As novas dimensões são descritas na lista a seguir.  
  
 Dimensão Revendedor  
 A dimensão Revendedor tem como base a tabela **Revendedor** da exibição da fonte de dados **Adventure Works DW 2012** .  
  
 Dimensão Promoção  
 A dimensão Promoção tem como base a tabela **Promoção** da exibição da fonte de dados **Adventure Works DW 2012** .  
  
 Dimensão Região de Vendas  
 A dimensão Região de Vendas tem como base a tabela **SalesTerritory** da exibição da fonte de dados **Adventure Works DW 2012** .  
  
 Dimensão Funcionário  
 A dimensão Funcionário tem como base a tabela **Funcionário** da exibição da fonte de dados do **Adventure Works DW 2012** .  
  
 Dimensão Geografia  
 A dimensão Geografia tem como base a tabela **Geografia** da exibição da fonte de dados **Adventure Works DW 2012** .  
  
#### <a name="analysis-services-cube"></a>Cubo do Analysis Services  
 O cubo **Tutorial do Analysis Services** agora tem dois grupos de medidas: o grupo de medidas original, baseado na tabela **InternetSales** , e um segundo grupo de medidas, baseado na tabela **ResellerSales** da exibição da fonte de dados **Adventure Works DW 2012** .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Definindo propriedades de atributo pai em uma hierarquia pai-filho](lesson-4-2-defining-parent-attribute-properties-in-a-parent-child-hierarchy.md) 
  
## <a name="see-also"></a>Consulte também  
 [Implantando um projeto do Analysis Services](../analysis-services/lesson-2-5-deploying-an-analysis-services-project.md)  
  
  
