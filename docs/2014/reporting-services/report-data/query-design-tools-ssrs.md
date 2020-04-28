---
title: Ferramentas de design de consulta no SQL Server Data Tools Report Designer (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- graphical query designer [Reporting Services]
- MDX query designer [Reporting Services]
- text-based query designer [Reporting Services]
- DMX [Reporting Services]
- query designers [Reporting Services]
- generic query designer See text-based query designer
- Reporting Services, query designers
- semantic queries [Reporting Services]
- Report Model Query Designer
ms.assetid: a8139a9d-4aeb-4e64-96f3-564edf60479f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1179f4e5a6c8be90b5bc52b814ae49c96a3a39aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388629"
---
# <a name="query-design-tools-in-report-designer-sql-server-data-tools-ssrs"></a>Ferramentas de design de consulta nas Ferramentas de Dados do SQL Server do Designer de Relatórios (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece várias ferramentas de design de consulta que podem ser usadas para criar consultas de conjunto de dados no Designer de Relatórios. O tipo de fonte de dados com a qual você está trabalhando determina a disponibilidade de um designer de consulta específico. Além disso, alguns designers de consulta fornecem modos alternativos para que você possa escolher se deseja trabalhar no modo visual ou diretamente na linguagem da consulta. Este tópico apresenta cada ferramenta e descreve o tipo de fonte de dados que cada uma suporta. As seguintes ferramentas são descritas neste tópico:

-   [Designer de consulta baseado em texto](#Textbased)

-   [Designer de Consultas Gráficas](#Graphical)

-   [Designer de Consulta do Modelo de Relatório](#Model)

-   [Designer de Consulta MDX](#MDX)

-   [Designer de Consulta DMX](#DMX)

-   [Designer de Consulta BI SapNetWeaver](#SAPBW)

-   [Designer de Consulta do Hyperion Essbase](#Hyperion)

 Todas as ferramentas de design de consulta são executadas no ambiente de design de dados do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] quando você trabalha com um modelo de projeto de Servidor de Relatório ou de Assistente de Servidor de Relatório. Para obter mais informações sobre designers de consulta, consulte [Designers de Consulta do Reporting Services](../reporting-services-query-designers.md).

##  <a name="text-based-query-designer"></a><a name="Textbased"></a> Designer de Consulta baseado em texto
 O designer de consulta baseado em texto é a ferramenta de criação de consulta padrão para a maioria das fontes de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]dados relacionais com suporte, incluindo, Oracle, Teradata, OLE DB, XML e ODBC. Em comparação com o designer de consultas gráficas, essa ferramenta de design de consulta não valida a sintaxe de consulta durante o design da consulta. A imagem a seguir fornece uma ilustração do designer de consulta com base no texto.

 ![Designer de consultas genérico para consulta de dados relacionais](../../analysis-services/media/rsqd-dsaw-sql-generic.gif "Designer de consultas genérico para consulta de dados relacionais")

 O designer de consulta com base no texto é recomendado para criar consultas complexas, com o uso de procedimentos armazenados, consultando dados XML, e para escrever consultas dinâmicas. Dependendo da fonte de dados, talvez você possa alternar o botão **Editar como Texto** na barra de ferramentas para alternar entre o designer de consultas gráficas e o designer de consulta com base no texto. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas baseado em texto](../text-based-query-designer-user-interface.md).

##  <a name="graphical-query-designer"></a><a name="Graphical"></a>Designer de consultas gráficas
 O designer de consultas gráficas é usado criar ou modificar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em um banco de dados relacional. Essa ferramenta de design de consulta é usada em vários produtos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e em outros componentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Dependendo do tipo de fonte de dados, ele dá suporte aos modos de Texto, StoredProcedure e TableDirect. A imagem a seguir fornece uma ilustração do designer de consultas gráficas.

 ![Designer de consultas gráficas para consulta SQL](../media/rsqd-dsaw-sql.gif "Designer de consultas gráficas para consulta SQL")

 Você pode alternar o botão **Editar como Texto** na barra de ferramentas para alternar entre o designer de consultas gráficas e o designer de consulta com base no texto. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Gráficas](graphical-query-designer-user-interface.md).

##  <a name="report-model-query-designer"></a><a name="Model"></a>Designer de consulta de modelo de relatório
 O designer de consulta de Modelo de Relatório é usado para criar ou modificar consultas executadas em um modelo de relatório SMDL publicado em um servidor de relatório. Relatórios executados em modelos têm suporte para exploração de dados de clickthrough. A consulta determina o caminho da exploração de dados em tempo de execução. A imagem a seguir fornece uma ilustração do designer de consulta de Modelo de Relatório.

 ![Interface do usuário do Designer de Consultas do Modelo Semântico](../media/rsqd-dsawmodel-smql.gif "Interface do usuário do Designer de Consultas do Modelo Semântico")

 Para usar o designer de consulta do Modelo de Relatório, você deve definir uma fonte de dados que aponte para um modelo publicado. Quando você define um conjunto de dados para a fonte de dados, pode abrir a consulta de conjunto de dados no designer de consulta do Modelo de Relatório. O designer de consulta do Modelo de Relatório pode ser usado em modos gráficos ou com base no texto. Você pode alternar o botão **Editar como Texto** na barra de ferramentas para alternar entre o designer de consultas gráficas e o designer de consulta com base no texto. Para obter mais informações, consulte [Interface do usuário do Designer de Consulta do modelo de relatório](report-model-query-designer-user-interface.md).

##  <a name="mdx-query-designer"></a><a name="MDX"></a>Designer de consulta MDX
 O designer de consulta MDX é usado para criar ou modificar consultas executadas em uma fonte de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] com cubos multidimensionais. A imagem a seguir fornece uma ilustração do designer de consulta MDX após a definição da consulta e do filtro.

 ![Designer de consultas MDX do Analysis Services, exibição de design](../../analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Designer de consultas MDX do Analysis Services, exibição de design")

 Para usar o designer de consulta MDX, você deve definir uma fonte de dados que tenha um cubo do Analysis Services disponível, válido e que tenha sido processado. Quando você define um conjunto de dados para a fonte de dados, pode abrir a consulta no designer de consulta MDX. Se necessário, use os botões MDX e DMX na barra de ferramentas para alternar entre os modos MDX e DMX. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas MDX do Analysis Services](analysis-services-mdx-query-designer-user-interface.md).

##  <a name="dmx-query-designer"></a><a name="DMX"></a>Designer de consulta DMX
 O designer de consulta DMX é usado para criar ou modificar consultas executadas em uma fonte de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] com modelos de mineração. A imagem a seguir fornece uma ilustração do designer de consulta DMX após a seleção do modelo e das tabelas de entrada.

 ![Designer de consultas DMX do Analysis Services, modo de exibição de Design](../media/rsqd-dsawas-dmx-designmode.gif "Designer de consultas DMX do Analysis Services, modo de exibição de Design")

 Para usar o designer de consulta DMX, você deve definir uma fonte de dados que tenha um modelo de mineração de dados válido disponível. Quando você define um conjunto de dados para a fonte de dados, pode abrir a consulta no designer de consulta DMX. Se necessário, use os botões MDX e DMX na barra de ferramentas para alternar entre os modos MDX e DMX. Após selecionar o modelo, você pode criar consultas de previsão de mineração de dados que fornecem dados a um relatório. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas DMX do Analysis Services](analysis-services-dmx-query-designer-user-interface.md).

##  <a name="sap-netweaver-bi-query-designer"></a><a name="SAPBW"></a>Designer de consulta do SAP NetWeaver BI
 O designer de consulta do [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] é usado para recuperar dados de um banco de dados do [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] . Para usar esse designer de consulta, você deve ter uma fonte de dados do [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] que tenha pelo menos uma consulta InfoCube, MultiProvider, ou habilitada para Web definida. A imagem a seguir fornece uma ilustração do designer de consulta [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] .

 ![Designer de consultas usando MDX no Modo Design](../media/rsqd-dssapbw-mdx-designmode.gif "Designer de consultas usando MDX no Modo Design")

##  <a name="hyperion-essbase-query-designer"></a><a name="Hyperion"></a>Designer de consulta do Hyperion Essbase
 O designer de consulta [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] é usado para recuperar dados de bancos de dados e aplicativos [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] . A imagem a seguir fornece uma ilustração do designer de consulta [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] .

 ![Designer de consultas da fonte de dados do Hyperion Essbase](../media/rsqd-dshyperionessbase-mdx-designmode.gif "Designer de consultas da fonte de dados do Hyperion Essbase")

 Para usar este designer de consulta, você deve ter uma fonte de dados [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] que tenha pelo menos um banco de dados. Para obter mais informações, consulte [Interface do usuário do Designer de Consulta do SAP NetWeaver BI](sap-netweaver-bi-query-designer-user-interface.md).

## <a name="see-also"></a>Consulte Também
 [As ferramentas de Reporting Services](../tools/reporting-services-tools.md) [adicionam dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-datasets-ssrs.md) [conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) [Reporting Services tutoriais &#40;](../reporting-services-tutorials-ssrs.md) as fontes de dados do ssrs&#41;[com suporte do Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) [criar uma fonte de dados inserida ou compartilhada &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)


