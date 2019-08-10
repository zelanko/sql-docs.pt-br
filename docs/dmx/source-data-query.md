---
title: '&lt;consulta&gt; de dados de origem | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e523d33da502a971b950e33ec0bd935149ed26f7
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892338"
---
# <a name="ltsource-data-querygt"></a>&lt;consulta de dados de origem&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Para treinar um modelo de data mining e criar previsões de um modelo de mineração, você precisa acessar os dados que são externos ao [!INCLUDE[msCoName](../includes/msconame-md.md)] banco de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dado. Use a \<cláusula > de consulta de dados de origem em DMX (extensões de mineração de dados) para definir esses dados externos. A [inserção no &#40;DMX&#41;](../dmx/insert-into-dmx.md), [selecione do &#60;modelo&#62; de junção &#40;de previsão&#41;DMX](../dmx/select-from-model-prediction-join-dmx.md)e [selecione de instruções de junção de previsão natural](../dmx/select-from-model-prediction-join-dmx.md) todos usam **\<consulta de dados de origem >** .  
  
## <a name="query-types"></a>Tipos de consultas  
 As três modos mais comuns para especificar dados de origem são:  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 Esta instrução consulta dados que são externos a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], usando uma fonte de dados existente.  
  
 Embora **OPENQUERY** seja semelhante na função para **OPENROWSET**, **OPENQUERY** tem os seguintes benefícios:  
  
-   Uma consulta DMX é muito mais fácil de escrever com **OPENQUERY**. Ao invés de criar uma nova cadeia de caracteres de conexão toda vez que você escreve uma consulta, é possível aproveitar a cadeia de caracteres de conexão existente na fonte de dados. O objeto de fonte de dados também pode controlar o acesso de dados para usuários individuais.  
  
-   O administrador tem mais controle sobre como são acessados os dados no servidor. Por exemplo, o administrador pode controlar quais provedores são carregados no servidor e quais dados externos podem ser acessados.  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 Esta instrução consulta dados que são externos a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], usando uma fonte de dados existente.  
  
 [FORMA &#40;DMX&#41;](../dmx/source-data-query-shape.md)  
 Esta instrução consulta múltiplas fontes de dados para criar uma tabela aninhada. Usando **Shape**, você pode combinar dados de várias fontes em uma única tabela hierárquica. Isto permite a você aproveitar a capacidade do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de aninhar tabelas inserindo uma tabela dentro de outra.  
  
 Para especificar os dados de origem, você pode usar também as seguintes opções:  
  
-   Qualquer instrução DMX válida  
  
-   Qualquer instrução MDX válida  
  
-   Uma tabela que retorna um procedimento armazenado  
  
-   Um conjunto de linhas XMLA  
  
-   Um parâmetro de conjunto de linhas  
  
## <a name="see-also"></a>Consulte também  
 [Instruções de manipulação &#40;de&#41; dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução &#40;DMX&#41; de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [Analysis Services de &#40;tabelas aninhadas – mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
  
