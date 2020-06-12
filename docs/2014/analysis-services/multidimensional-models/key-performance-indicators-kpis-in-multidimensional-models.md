---
title: KPIs (indicadores chave de desempenho) em modelos multidimensionais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- viewing Key Performance Indicators
- Key Performance Indicators [Analysis Services]
- KPIs [Analysis Services]
- OLAP objects [Analysis Services], performance indicators
- weights [Analysis Services]
- displaying Key Performance Indicators
- parent KPIs [Analysis Services]
- child KPIs
ms.assetid: 73aee2da-da30-44f1-829c-0a4c078a7768
author: minewiskan
ms.author: owend
ms.openlocfilehash: c6ae3a34da62ed24d1971540e825f9f8347f413f
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546628"
---
# <a name="key-performance-indicators-kpis-in-multidimensional-models"></a>KPIs (indicadores chave de desempenho) em modelos multidimensionais
  Na terminologia empresarial, um KPI (indicador chave de desempenho) é uma medida quantificável para medir o sucesso empresarial.  
  
 No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], um KPI é uma coleção de cálculos associada a um grupo de medidas em um cubo usado para avaliar o sucesso nos negócios. Normalmente, esses cálculos são uma combinação de MDX ou membros calculados. Os KPIs também contêm metadados adicionais que fornecem informações sobre como os aplicativos cliente devem exibir os resultados de cálculos de KPIs.  
  
 Um KPI processa informações sobre um conjunto de metas, a fórmula real do desempenho registrado em cubos e a medida para mostrar a tendência e o status do desempenho. O AMO é usado para definir as fórmulas e outras definições sobre os valores de um KPI. Uma interface de consulta, como ADOMD.NET, é usada pelo aplicativo cliente para recuperar e expor os valores de KPI ao usuário final. Para obter mais informações, consulte [Desenvolvendo com ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net).  
  
 Um simples objeto <xref:Microsoft.AnalysisServices.Kpi> é composto de: informações básicas, a meta, o valor real atingido, o valor de status, o valor de tendência e a pasta na qual o KPI é exibido. As informações básicas incluem o nome e a descrição do KPI. A meta é uma expressão MDX que avalia a um número. O valor real é uma expressão MDX que avalia a um número. O status e valor de tendência são expressões MDX que avaliam a um número. A pasta é um local sugerido para o KPI para ser apresentado ao cliente.  
  
 Na terminologia empresarial, um KPI (indicador chave de desempenho) é uma medida quantificável para medir o sucesso empresarial. Um KPI é avaliado, frequentemente, ao longo do tempo. Por exemplo, o departamento de vendas de uma organização pode usar o lucro bruto mensal como um KPI, mas o departamento de recursos humanos da mesma organização pode usar a rotatividade de funcionários trimestral. Cada um é um exemplo de KPI. Os executivos frequentemente usam KPIs agrupados em um scorecard empresarial para obter um resumo histórico rápido e preciso do sucesso da empresa.  
  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , um KPI é uma coleção de cálculos, que são associados a um grupo de medidas em um cubo, que são usados para avaliar o sucesso do negócio. Normalmente, esses cálculos são uma combinação de MDX e membros calculados. Os KPIs também contêm metadados adicionais que fornecem informações sobre como os aplicativos cliente devem exibir os resultados de um cálculo de KPIs.  
  
 Uma vantagem importante dos KPIs no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é que eles são KPIs baseados em servidores consumíveis por diferentes aplicativos cliente. Um KPI com base em servidor apresenta uma única versão de autenticidade, comparado com as versões separadas de autenticidade dos aplicativos cliente separados. Além disso, executando algumas vezes os cálculos complexos no servidor, em vez de em cada computador cliente, poderá trazer benefícios de desempenho.  
  
## <a name="common-kpi-terms"></a>Termos comuns de KPI  
 A tabela a seguir fornece definições para termos de KPI comuns no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Termo|Definição|  
|----------|----------------|  
|Goal|Uma expressão numérica MDX ou um cálculo que retorna o valor alvo do KPI.|  
|Valor|Uma expressão numérica MDX que retorna o valor real do KPI.|  
|Status|Uma expressão MDX que representa o estado do KPI em um point-in-time.<br /><br /> O status da expressão MDX deve retornar um valor normalizado entre -1 e 1. Valores iguais ou menores que -1 serão interpretados como "ruim" ou "baixo". Um valor de zero (0) será interpretado como "aceitável" ou "médio". Os valores iguais ou maiores que 1 serão interpretados como "bom" ou "alto".<br /><br /> Um número ilimitado de valores intermediários pode ser opcionalmente retornado e pode ser usado para exibir qualquer número de estados adicionais, caso tenham suporte pelo aplicativo cliente.|  
|Tendência|Uma expressão MDX que avalia o valor do KPI ao longo do tempo. A tendência pode ser qualquer critério com base no tempo e que seja útil em um contexto empresarial específico.<br /><br /> A expressão MDX de tendência permite que um usuário empresarial determine se o KPI está melhorando ou piorando ao longo do tempo.|  
|Indicador de status|Um elemento visual que fornece uma indicação rápida do status de um KPI. A exibição do elemento é determinada pelo valor da expressão MDX que avalia o status.|  
|Indicador de tendência|Um elemento visual que fornece uma indicação rápida da tendência de um KPI. A exibição do elemento é determinada pelo valor da expressão MDX que avalia a tendência.|  
|Pasta de exibição|A pasta na qual o KPI aparecerá quando um usuário estiver navegando no cubo.|  
|KPI Pai|Uma referência a um KPI existente que usa o valor do KPI filho como parte da computação do KPI pai. Às vezes, um único KPI será uma computação que consiste nos valores de outros KPIs. Essa propriedade facilita a exibição correta dos KPIs filhos sob o KPI pai em aplicativos cliente.|  
|Membro da hora atual|Uma expressão MDX que retorna o membro que identifica o contexto temporal do KPI.|  
|Peso|Uma expressão numérica MDX que atribui uma importância relativa a um KPI. Se o KPI estiver atribuído a um KPI pai, o peso será usado para ajustar proporcionalmente os resultados do valor do KPI filho ao calcular o valor do KPI pai.|  
  
## <a name="parent-kpis"></a>KPIs Pai  
 Uma organização pode rastrear diferentes métricas empresariais em diferentes níveis. Por exemplo, apenas dois ou três KPIs podem ser usados para medir o sucesso de toda a empresa, mas esses KPIs gerais podem ser usados em três ou quatro outros KPIs rastreados pelas unidades de negócios ao longo da empresa. Além disso, as unidades de negócio em uma empresa podem usar estatísticas diferentes para calcular o mesmo KPI, esses resultados são acumulados para o KPI geral.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite definir uma relação pai-filho entre KPIs. Essa relação pai-filho permite que os resultados do KPI filho seja usada para calcular os resultados do KPI pai. Os aplicativos cliente também podem usar essa relação para exibir os KPIs pai e filho adequadamente.  
  
## <a name="weights"></a>Pesos  
 Os pesos também podem ser atribuídos à KPIs filho. Os pesos permitem que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ajuste proporcionalmente os resultados do KPI filho ao calcular o valor do KPI pai.  
  
## <a name="retrieving-and-displaying-kpis"></a>Recuperando e exibindo KPIs  
 A exibição dos KPIs depende da implementação do aplicativo cliente. Por exemplo, selecionar **Exibição de Navegador** na barra de ferramentas na guia **KPIs** do Designer de Cubo, demonstra uma possível implementação do cliente, com gráficos usados para exibir os indicadores de status e tendência, exibir pastas usadas para agrupar KPIs e KPIs filho exibidos sob KPIs pai.  
  
 Você pode usar as funções MDX para recuperar as seções individuais do KPI, como o valor ou meta, para usar em expressões MDX, instruções e scripts.  
  
  
