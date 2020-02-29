---
title: Navegador (Designer de cubo) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.view.f1
ms.assetid: efb5ee1c-de50-4bfc-83ff-08a4f03c3ece
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 902d35dfc20973dbbad5e6608d5934b31245d9d2
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174231"
---
# <a name="browser-cube-designer-analysis-services---multidimensional-data"></a>Navegador (Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use a guia **Navegador** do Designer de Cubo para explorar dimensões, medidas e KPIs em um cubo. No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], o Navegador do Cubo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] foi integrado com o Designer de Consulta MDX e fornece interfaces gráficas do usuário para ajudar a criar consultas MDX, filtrar e fatiar cubos, além de fazer buscas detalhadas em hierarquias.

 A guia **Navegador** em dois modos: o **Modo de Design** e o **Modo de Consulta**. Em qualquer modo, você pode usar os objetos do painel **Metadados** para explorar o cubo ou pode arrastar membros do painel **Metadados** para a área de consulta a fim de criar uma consulta MDX que recupere os dados que você deseja usar.

 **Navegar e consultar usando o modo de design gráfico**

 A figura a seguir mostra a interface do **Navegador** no **Modo de design**gráfico.

 ![Designer de consultas MDX do Analysis Services, modo de exibição de Design](media/rsqd-dsawas-mdx-designmode.gif "Designer de consultas MDX do Analysis Services, modo de exibição de Design")

 Enquanto você estiver trabalhando no modo de design gráfico, se o botão de alternância **executar** automaticamente (![executar a consulta](media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente")automaticamente) na barra de ferramentas estiver selecionado, o **navegador** executará uma consulta cada vez que você soltar um objeto de metadados no painel dados. Você também pode executar manualmente a consulta usando o botão **Executar consulta** (![executar a consulta](media/rsqdicon-run.gif "Executar a consulta")) na barra de ferramentas.

 Para alterar o designer de consultas gráficas para o modo **Consulta** e trabalhar com o texto das instruções MDX, clique no botão **Modo Design** na barra de ferramentas.

 **Navegar e consultar usando o modo de texto MDX**

 Enquanto estiver no modo de design de texto MDX, você pode trabalhar diretamente com o MDX. O painel **Metadados** ainda está disponível, de forma que você pode adicionar objetos à área de design de consulta e pode arrastar e soltar funções e operadores MDX da lista no painel **Funções** .

 A figura a seguir mostra a interface do **Navegador** no modo de Consulta.

 ![Designer de consulta MDX do Analysis Services, exibição de consulta](media/rsqd-dsawas-mdx-querymode.gif "Designer de consulta MDX do Analysis Services, exibição de consulta")

 Você pode começar a trabalhar no modo de Design gráfico, adicionar os objetos necessários, adicionar filtros para fatiar o cubo e depois alternar para o modo de texto a fim de ampliar a consulta MDX padrão que foi gerada, e incluir propriedades de membro e propriedades de célula adicionais.

 O painel **Metadados** exibe as guias para **Metadados** e **Funções**. Na guia **Metadados** , você pode arrastar as dimensões, hierarquias, KPIs e medidas para a área de design de consulta. Na guia **Funções** , você pode arrastar as funções para a área de design de consulta. Quando você executar a consulta, a área de design de consulta exibirá os resultados da consulta MDX. Você também pode clicar em **Analisar no Excel** na **Barra de Ferramentas** para exportar os dados para o Microsoft Office Excel e exibir os resultados da mesma maneira como os usuários fariam, em uma Tabela Dinâmica. As seções a seguir descrevem a barra de ferramentas e todos os painéis para cada modo do **Navegador** com mais detalhes.

 Observe que, enquanto você estiver trabalhando no modo de texto, o botão de alternância **executar** automaticamente (![executar a consulta](media/rsqdicon-autoexecute.gif "Executar a consulta automaticamente")automaticamente) na barra de ferramentas não estará disponível. No entanto, você pode executar consultas manualmente usando o botão **Executar consulta** (![executar a consulta](media/rsqdicon-run.gif "Executar a consulta")) na barra de ferramentas.

## <a name="sections"></a>Seções
 **Barra de ferramentas** A barra de ferramentas contém uma ferramenta que pode ser usada no modo de exibição de design ou de consulta. Para obter mais informações sobre a barra de ferramentas e como usar esses recursos, consulte [Barra de Ferramentas &#40;Guia Navegador, Designer de Cubo&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md).

 **Analisar no Excel** Use o recurso **analisar no Excel** para enviar a seleção atual de dados de cubo para o Excel, para que você possa visualizar os dados em uma tabela dinâmica. A seleção atual de dados é baseada nos itens que você adicionou do painel **Metadados** e todos os filtros que você possa ter definido usando as funções de criação de filtros e consultas. Para obter mais informações, consulte [Analisar no Excel &#40;Guia Navegador, Designer de Cubo&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md).

 **Metadados** do Use o painel **metadados** para exibir objetos contidos pelo cubo, para fazer uma busca detalhada em hierarquias e explorar e usar medidas. Depois de ter selecionado e para exibir os dados associados a eles no painel **Relatório**. Para obter mais informações sobre esse painel, consulte [Metadados &#40;Guia Navegador, Designer de Cubo&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md).

 **Filtrar e consultar** Use essa área da superfície de design para criar consultas MDX, arrastando e soltando objetos do painel de **metadados** e especificando critérios de filtro no cubo ou dimensão de origem. Para obter mais informações, consulte [Consultar e filtrar &#40;Guia Navegador, Designer de Cubo&#41; &#40;Analysis Services – Dados Multidimensionais&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md).

## <a name="see-also"></a>Consulte Também
 [Objetos de cubo &#40;Analysis Services de dados multidimensionais&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md) [cubos no designer de cubo de modelos multidimensionais](multidimensional-models/cubes-in-multidimensional-models.md) [&#40;Analysis Services-dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)


