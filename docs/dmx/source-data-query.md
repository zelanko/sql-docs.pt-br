---
title: '&lt;consulta de dados de origem &gt; | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 15767abbbffd7ede7d7ae252c7e84589abad1a98
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670011"
---
# <a name="ltsource-data-querygt"></a>&lt;consulta de dados de origem&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Para treinar um modelo de data mining e criar previsões de um modelo de mineração, você precisa acessar os dados que são externos ao banco de dado [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Use a \< cláusula> de consulta de dados de origem em DMX (extensões de mineração de dados) para definir esses dados externos. O [&#41;de inserção no &#40;DMX ](../dmx/insert-into-dmx.md), [selecione do modelo de &#60;&#62; junção de previsão &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)e [Selecione em instruções de junção de previsão natural](../dmx/select-from-model-prediction-join-dmx.md) todos usam ** \<>de consulta de dados de origem **.  
  
## <a name="query-types"></a>Tipos de consultas  
 As três modos mais comuns para especificar dados de origem são:  
  
 [&#40;DE&#41;DE OPENQUERY DO DMX](../dmx/source-data-query-openquery.md)  
 Esta instrução consulta dados que são externos a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], usando uma fonte de dados existente.  
  
 Embora **OPENQUERY** seja semelhante na função para **OPENROWSET**, **OPENQUERY** tem os seguintes benefícios:  
  
-   Uma consulta DMX é muito mais fácil de escrever com **OPENQUERY**. Ao invés de criar uma nova cadeia de caracteres de conexão toda vez que você escreve uma consulta, é possível aproveitar a cadeia de caracteres de conexão existente na fonte de dados. O objeto de fonte de dados também pode controlar o acesso de dados para usuários individuais.  
  
-   O administrador tem mais controle sobre como são acessados os dados no servidor. Por exemplo, o administrador pode controlar quais provedores são carregados no servidor e quais dados externos podem ser acessados.  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 Esta instrução consulta dados que são externos a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], usando uma fonte de dados existente.  
  
 [&#41;DE FORMA &#40;DMX](../dmx/source-data-query-shape.md)  
 Esta instrução consulta múltiplas fontes de dados para criar uma tabela aninhada. Usando **Shape**, você pode combinar dados de várias fontes em uma única tabela hierárquica. Isto permite a você aproveitar a capacidade do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de aninhar tabelas inserindo uma tabela dentro de outra.  
  
 Para especificar os dados de origem, você pode usar também as seguintes opções:  
  
-   Qualquer instrução DMX válida  
  
-   Qualquer instrução MDX válida  
  
-   Uma tabela que retorna um procedimento armazenado  
  
-   Um conjunto de linhas XMLA  
  
-   Um parâmetro de conjunto de linhas  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [Tabelas aninhadas &#40;Analysis Services de mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
  
