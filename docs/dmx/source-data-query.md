---
title: '&lt;consulta de fonte de dados&gt; | Microsoft Docs'
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- data sources [DMX]
- predictions [DMX]
- source data query element
- queries [DMX], source data
- external data access [DMX]
- <source data query> element
- training mining models
ms.assetid: 9dce5e37-1354-4d28-87c2-f9c419cb5b09
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 195c2ecd04a28ad830aca2d90df821b76d46e98e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt"></a>&lt;consulta de fonte de dados&gt;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Para treinar um modelo de mineração de dados e criar previsões de um modelo de mineração, você precisa acessar dados externos para o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados. Você usa o \<consulta de fonte de dados > cláusula em extensões DMX (Data Mining) para definir estes dados externos. O [INSERT INTO &#40; DMX &#41;](../dmx/insert-into-dmx.md), [SELECT FROM &#60; modelo de &#62; JUNÇÃO de previsão &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md), e [SELECT FROM NATURAL PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) todas as instruções usam  **\<consulta de fonte de dados >**.  
  
## <a name="query-types"></a>Tipos de consultas  
 As três modos mais comuns para especificar dados de origem são:  
  
 [OPENQUERY &#40; DMX &#41;](../dmx/source-data-query-openquery.md)  
 Esta instrução consulta dados que são externos a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], usando uma fonte de dados existente.  
  
 Enquanto **OPENQUERY** é semelhante à função para **OPENROWSET**, **OPENQUERY** tem os seguintes benefícios:  
  
-   Uma consulta DMX é muito mais fácil de escrever com **OPENQUERY**. Ao invés de criar uma nova cadeia de caracteres de conexão toda vez que você escreve uma consulta, é possível aproveitar a cadeia de caracteres de conexão existente na fonte de dados. O objeto de fonte de dados também pode controlar o acesso de dados para usuários individuais.  
  
-   O administrador tem mais controle sobre como são acessados os dados no servidor. Por exemplo, o administrador pode controlar quais provedores são carregados no servidor e quais dados externos podem ser acessados.  
  
 [OPENROWSET &#40; DMX &#41;](../dmx/source-data-query-openrowset.md)  
 Esta instrução consulta dados que são externos a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], usando uma fonte de dados existente.  
  
 [FORMA &#40; DMX &#41;](../dmx/source-data-query-shape.md)  
 Esta instrução consulta múltiplas fontes de dados para criar uma tabela aninhada. Usando **forma**, você pode combinar dados de várias fontes em uma única tabela hierárquica. Isto permite a você aproveitar a capacidade do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de aninhar tabelas inserindo uma tabela dentro de outra.  
  
 Para especificar os dados de origem, você pode usar também as seguintes opções:  
  
-   Qualquer instrução DMX válida  
  
-   Qualquer instrução MDX válida  
  
-   Uma tabela que retorna um procedimento armazenado  
  
-   Um conjunto de linhas XMLA  
  
-   Um parâmetro de conjunto de linhas  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Tabelas aninhadas &#40; Analysis Services – mineração de dados &#41;](../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  

