---
title: Navegador KPI (guia KPIs, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 41000c78c4ff3a68e1d3acd107ce57c221a16e28
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079497"
---
# <a name="kpi-browser-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Navegador KPI (guia KPIs, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Navegador de KPI** na guia **KPIs** do Designer de Cubo para exibir e testar os resultados dos KPIs (indicadores chave de desempenho). Os KPIs devem ser implantados primeiro em uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] antes da navegação.  
  
> [!NOTE]  
>  Esse painel é exibido apenas na exibição do navegador.  
  
## <a name="options"></a>Opções  
 **Grade de subcubo**  
 Use para definir um subcubo e restringir os resultados dos KPIs a serem exibidos no painel **Resultados** . A grade contém as seguintes colunas:  
  
 **Dimension**  
 Selecione a dimensão à qual esse filtro se aplica.  
  
 **Hierarchy**  
 Selecione a hierarquia à qual esse filtro se aplica.  
  
 **Operador**  
 Selecione o operador que define como a expressão na **Expressão de Filtro** é aplicada à hierarquia selecionada. A tabela a seguir descreve os operadores disponíveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Equal**|Os resultados são restringidos ao conjunto definido na **Expressão de Filtro**.|  
|**Não é igual**|Os resultados são restringidos aos membros excluídos pelo conjunto definido na **Expressão de Filtro**.|  
|**Entrada**|Os resultados são restringidos ao conjunto nomeado escolhido na **Expressão de Filtro**.|  
|**Não está em**|Os resultados são restringidos aos membros excluídos pelo conjunto nomeado escolhido na **Expressão de Filtro**.|  
|**Contém**|Os resultados são restringidos aos membros cujos nomes contêm a sequência de caracteres na **Expressão de Filtro**.|  
|**Começa com**|Os resultados são restringidos aos membros cujos nomes começam com a sequência de caracteres na **Expressão de Filtro**.|  
|**Intervalo (inclusivo)**|Os resultados são restringidos ao intervalo escolhido na **Expressão de Filtro**.|  
|**Intervalo (exclusivo)**|Os resultados são restringidos aos membros excluídos pelo intervalo escolhido na **Expressão de Filtro**.|  
|**MDX**|Os resultados são restringidos à expressão MDX definida na **Expressão de Filtro**.|  
  
 **Expressão de filtro**  
 Digite a expressão a ser avaliada pelo **Operador**que restringe os resultados do KPI a serem procurados.  
  
> [!NOTE]  
>  Este campo é um elemento de entrada de dados dinâmicos que altera a aparência para refletir os tipos de dados necessários para o operador selecionado.  
  
 **Grade de resultados**  
 Exibe o valor avaliado, a meta, o status e a tendência dos KPIs, com base no filtro definido na **Grade de filtro**. A grade contém as seguintes colunas:  
  
 **Exibir estrutura**  
 Exibe os KPIs contidos pelo cubo, organizados hierarquicamente de acordo com os valores da **Pasta de exibição** ou **KPI Pai** de cada KPI.  
  
 **Value**  
 Exibe o valor do KPI.  
  
 **Meta**  
 Exibe o valor da meta do KPI.  
  
 **Status**  
 Exibe o gráfico de status do KPI.  
  
 **Trend**  
 Exibe o gráfico de tendências do KPI.  
  
 **Weight**  
 Exibe o fator de peso do KPI.  
  
 **(Descrição)**  
 Exibirá um ícone de informações se uma descrição for fornecida para um KPI.  
  
 Focalize o mouse sobre o ícone de informações para exibir uma Dica de Ferramenta contendo a descrição do KPI.  
  
> [!NOTE]  
>  Se ocorrer um erro ao calcular um KPI na instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , essa opção exibirá informações associadas ao erro.  
  
## <a name="see-also"></a>Consulte também  
 [KPIs &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
