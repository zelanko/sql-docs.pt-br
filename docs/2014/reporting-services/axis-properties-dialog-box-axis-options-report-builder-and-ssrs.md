---
title: Caixa de diálogo de propriedades do eixo, opções de eixo (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.axisproperties.axisoptions.f1
- "10138"
ms.assetid: b276e210-7a12-48ae-971b-7dabae51df11
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 690f092b98a76ddd9ccc18d15f4250e7e856efa0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030638"
---
# <a name="axis-properties-dialog-box-axis-options-report-builder-and-ssrs"></a>Caixa de diálogo Propriedades do Eixo, Opções do Eixo (Construtor de Relatórios e SSRS)
  Selecione **opções de eixo** sobre o **Horizontal** ou **propriedades VerticalAxis** caixa de diálogo para definir a aparência do eixo do gráfico especificado. Em versões anteriores do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], o gráfico exibia todos os rótulos no eixo x por padrão. No entanto, no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2008, o gráfico descarta os rótulos para produzir uma imagem mais limpa no gráfico e evitar colisões de rótulos. Para obter mais informações, consulte [Formatação de rótulos de eixos em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opções  
 **Habilitar quebras de escala**  
 Selecione esta opção para habilitar o gráfico para desenhar quebras de escala quando for necessário. Quando está opção é habilitada, o gráfica calcula automaticamente se há diferença suficiente entre os pontos altos e baixos no conjunto de dados para desenhar uma quebra de escala.  
  
 **Direção inversa**  
 Selecione esta opção para inverter a direção do gráfico. Por exemplo, por padrão, um gráfico de colunas exibe o eixo y no lado esquerdo e as categorias da esquerda para a direita. Quando essa opção é selecionada, o gráfico exibe o eixo y no lado direito e as categorias da direita para a esquerda.  
  
 **Usar cor de entrelaçamento**  
 Selecione essa opção para adicionar linhas distribuídas ao gráfico e depois selecione uma cor ou digite uma expressão. As linhas distribuídas são faixas sombreadas na área do gráfico que dão um efeito de alternar áreas claras e escuras entre as linhas de grade. Essas linhas distribuídas são úteis para destacar padrões repetidos em um eixo.  
  
 **Sempre incluir zero**  
 Selecione essa opção para sempre incluir zero na escala de eixo. Se esta opção não for habilitada, o gráfico não rotulará o valor zero no eixo. Incluindo os valores zero é útil quando o conjunto de dados tiver valores negativos ou zero.  
  
 **Eixo escalar**  
 Selecione esta opção para exibir um conjunto de valores de eixo em uma escala contínua. Por exemplo, se o conjunto de dados contém dados para janeiro, março e novembro, um eixo não escalar exibe apenas esses meses, enquanto que um eixo escalar exibe todos os meses do ano.  
  
 **Usar escala logarítmica**  
 Selecione esta opção para indicar que a escala do eixo é logarítmica. Essa opção só estará disponível no eixo y se o eixo contiver valores numéricos positivos.  
  
 Na caixa, digite a base logarítmica a ser usada quando o eixo é definido para usar uma escala logarítmica. Por padrão, o gráfico usa uma base de 10 para a escala logarítmica de um eixo. Esta opção só estará disponível no eixo y se o eixo for numérico.  
  
 **Mínimo**  
 Digite uma expressão ou um valor para obter o valor mínimo para o eixo x. Se omitido, o valor mínimo será determinado pelos dados retornados pelo conjunto de dados.  
  
 **Máximo**  
 Digite uma expressão ou um valor para obter o valor máximo para o eixo x. Se omitido, o valor máximo será determinado pelos dados retornados pelo conjunto de dados.  
  
 **intervalo**  
 Digite uma expressão ou um valor para o intervalo entre os rótulos do eixo. Por exemplo, digite 1 para exibir cada rótulo de categoria no eixo. Digite 2 para exibir qualquer outro rótulo de categoria. Se omitido, os rótulos serão calculados automaticamente com base nos valores do conjunto de dados.  
  
 **Tipo de intervalo**  
 Digite uma expressão ou um valor para o tipo de intervalo do intervalo especificado. Por exemplo, se quiser que o intervalo seja de dois dias, especifique **2** para o intervalo e **Days** para o tipo de intervalo.  
  
 **Margens laterais**  
 Digite uma expressão ou selecione um valor para adicionar ou remover uma margem entre os elementos do gráfico e as laterais do gráfico. Se essa opção for definida como **Auto**, as margens laterais serão adicionadas.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando rótulos dos eixos de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Especificar um intervalo do eixo &#40;Construtor de Relatórios e SSRS&#41;](report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Formatar rótulos de eixo como datas ou moedas &#40;Construtor de Relatórios e SSRS&#41;](report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Plotar dados em um eixo secundário &#40;relatórios e SSRS&#41;](report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)   
 [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Adicionar ou remover margens de um gráfico &#40;Construtor de Relatórios e SSRS&#41;](report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
  
