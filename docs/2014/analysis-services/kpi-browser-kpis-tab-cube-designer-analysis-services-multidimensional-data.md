---
title: Navegador KPI (guia KPIs, designer de cubo) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpibrowserpane.f1
ms.assetid: 2f61bde6-e6ec-4511-8645-c272374014ad
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1b6d15cbb75f3528546c566a72f8b23323df8772
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543704"
---
# <a name="kpi-browser-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Navegador KPI (guia KPIs, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Navegador de KPI** na guia **KPIs** do Designer de Cubo para exibir e testar os resultados dos KPIs (indicadores chave de desempenho). Os KPIs devem primeiro ser implantados em uma [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância antes da navegação.  
  
> [!NOTE]  
>  Esse painel é exibido apenas na exibição do navegador.  
  
## <a name="options"></a>Opções  
 **Grade de subcubo**  
 Use para definir um subcubo e restringir os resultados dos KPIs a serem exibidos no painel **Resultados** . A grade contém as seguintes colunas:  
  
 **Dimensões**  
 Selecione a dimensão à qual esse filtro se aplica.  
  
 **Hierarquia**  
 Selecione a hierarquia à qual esse filtro se aplica.  
  
 **Operador**  
 Selecione o operador que define como a expressão na **Expressão de Filtro** é aplicada à hierarquia selecionada. A tabela a seguir descreve os operadores disponíveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Igual**|Os resultados são restringidos ao conjunto definido na **Expressão de Filtro**.|  
|**Diferente de**|Os resultados são restringidos aos membros excluídos pelo conjunto definido na **Expressão de Filtro**.|  
|**Em**|Os resultados são restringidos ao conjunto nomeado escolhido na **Expressão de Filtro**.|  
|**Não está em**|Os resultados são restringidos aos membros excluídos pelo conjunto nomeado escolhido na **Expressão de Filtro**.|  
|**Terá**|Os resultados são restringidos aos membros cujos nomes contêm a sequência de caracteres na **Expressão de Filtro**.|  
|**Começa Com**|Os resultados são restringidos aos membros cujos nomes começam com a sequência de caracteres na **Expressão de Filtro**.|  
|**Intervalo (Inclusivo)**|Os resultados são restringidos ao intervalo escolhido na **Expressão de Filtro**.|  
|**Intervalo (Exclusivo)**|Os resultados são restringidos aos membros excluídos pelo intervalo escolhido na **Expressão de Filtro**.|  
|**MDX**|Os resultados são restringidos à expressão MDX definida na **Expressão de Filtro**.|  
  
 **Expressão de filtro**  
 Digite a expressão a ser avaliada pelo **Operador**que restringe os resultados do KPI a serem procurados.  
  
> [!NOTE]  
>  Este campo é um elemento de entrada de dados dinâmicos que altera a aparência para refletir os tipos de dados necessários para o operador selecionado.  
  
 **Grade de resultados**  
 Exibe o valor avaliado, a meta, o status e a tendência dos KPIs, com base no filtro definido na **Grade de filtro**. A grade contém as seguintes colunas:  
  
 **Exibir Estrutura**  
 Exibe os KPIs contidos pelo cubo, organizados hierarquicamente de acordo com os valores da **Pasta de exibição** ou **KPI Pai** de cada KPI.  
  
 **Valor**  
 Exibe o valor do KPI.  
  
 **Goal**  
 Exibe o valor da meta do KPI.  
  
 **Status**  
 Exibe o gráfico de status do KPI.  
  
 **Trend**  
 Exibe o gráfico de tendências do KPI.  
  
 **Weight**  
 Exibe o fator de peso do KPI.  
  
 **Ndescrição**  
 Exibirá um ícone de informações se uma descrição for fornecida para um KPI.  
  
 Focalize o mouse sobre o ícone de informações para exibir uma Dica de Ferramenta contendo a descrição do KPI.  
  
> [!NOTE]  
>  Se ocorrer um erro ao calcular um KPI na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , essa opção exibirá informações associadas ao erro.  
  
## <a name="see-also"></a>Consulte Também  
 [KPIs &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
