---
title: '&lt;consulta de fonte de dados&gt; | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fdd0a3091440295e393d969f1b8161b83fb58d95
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38063956"
---
# <a name="ltsource-data-querygt"></a>&lt;consulta de fonte de dados&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Para treinar um modelo de mineração de dados e criar previsões a partir de um modelo de mineração, você tem que acessar dados externos para o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados. Você usa o \<consulta de fonte de dados > cláusula em extensões DMX (Data Mining) para definir estes dados externos. O [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md), [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), e [SELECT FROM NATURAL PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) usam todas as instruções  **\<consulta de fonte de dados >**.  
  
## <a name="query-types"></a>Tipos de consultas  
 As três modos mais comuns para especificar dados de origem são:  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 Esta instrução consulta dados que são externos a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], usando uma fonte de dados existente.  
  
 Embora **OPENQUERY** é semelhante à função para **OPENROWSET**, **OPENQUERY** tem os seguintes benefícios:  
  
-   Uma consulta DMX é muito mais fácil escrever com **OPENQUERY**. Ao invés de criar uma nova cadeia de caracteres de conexão toda vez que você escreve uma consulta, é possível aproveitar a cadeia de caracteres de conexão existente na fonte de dados. O objeto de fonte de dados também pode controlar o acesso de dados para usuários individuais.  
  
-   O administrador tem mais controle sobre como são acessados os dados no servidor. Por exemplo, o administrador pode controlar quais provedores são carregados no servidor e quais dados externos podem ser acessados.  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 Esta instrução consulta dados que são externos a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], usando uma fonte de dados existente.  
  
 [FORMA &#40;DMX&#41;](../dmx/source-data-query-shape.md)  
 Esta instrução consulta múltiplas fontes de dados para criar uma tabela aninhada. Usando **forma**, você pode combinar dados de várias fontes em uma única tabela hierárquica. Isto permite a você aproveitar a capacidade do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de aninhar tabelas inserindo uma tabela dentro de outra.  
  
 Para especificar os dados de origem, você pode usar também as seguintes opções:  
  
-   Qualquer instrução DMX válida  
  
-   Qualquer instrução MDX válida  
  
-   Uma tabela que retorna um procedimento armazenado  
  
-   Um conjunto de linhas XMLA  
  
-   Um parâmetro de conjunto de linhas  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Tabelas aninhadas &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  
