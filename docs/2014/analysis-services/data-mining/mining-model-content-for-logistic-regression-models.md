---
title: Conteúdo do modelo de mineração para modelos de regressão logística (Analysis Services-Mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- mining model content, logistic regression models
- regression algorithms [Analysis Services]
ms.assetid: 69cc0b86-e8bc-4d6c-903e-85724f5c0396
author: minewiskan
ms.author: owend
ms.openlocfilehash: 3232e4344b94e0b812df72ddebdc9a8d389d9f05
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84521362"
---
# <a name="mining-model-content-for-logistic-regression-models-analysis-services---data-mining"></a>Conteúdo do modelo de mineração para modelos de regressão logística (Analysis Services – Mineração de Dados)
  Este tópico descreve o conteúdo do modelo de mineração que é específico para modelos que usam o algoritmo Regressão Logística da Microsoft. Para obter uma explicação de como interpretar as estatísticas e a estrutura compartilhada por todos os tipos de modelos, e definições gerais dos termos relacionados ao conteúdo do modelo de mineração, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-a-logistic-regression-model"></a>Entendendo a estrutura de um modelo de regressão logística  
 Um modelo de regressão logística é criado usando o algoritmo Rede Neural da Microsoft com parâmetros que restringem o modelo para eliminar o nó oculto. Portanto, a estrutura geral de um modelo de regressão logística é quase idêntica à de um modelo de rede neural: cada modelo tem um único nó pai que representa o modelo e seus metadados e um nó de estatísticas marginais especial (NODE_TYPE = 24) que fornece estatísticas descritivas sobre as entradas usadas no modelo.  
  
 Além disso, o modelo contém uma sub-rede (NODE_TYPE = 17) para cada atributo previsível. Exatamente como em um modelo de rede neural, cada sub-rede sempre contém duas ramificações: uma para a camada de entrada e outra que contém a camada oculta (NODE_TYPE = 19) e a camada de saída (NODE_TYPE = 20) da rede. A mesma sub-rede pode ser usada para diversos atributos se eles forem especificados como somente para previsão. Os atributos previsíveis que também são entradas podem não ser exibidos na mesma sub-rede.  
  
 Porém, em um modelo de regressão logística, o nó que representa a camada oculta está vazio e não tem nenhum filho. Sendo assim, o modelo contém nós que representam saídas individuais (NODE_TYPE = 23) e entradas individuais (NODE_TYPE = 21), mas não nós ocultos individuais.  
  
 ![estrutura de conteúdo do modelo de regressão logística](../media/skt-modelcontentstructure-logregc.gif "estrutura de conteúdo do modelo de regressão logística")  
  
 Por padrão, um modelo de regressão logística é exibido no **Visualizador de Rede Neural da Microsoft**. Com esse visualizador personalizado, você pode filtrar os atributos de entrada e seus valores e visualizar, graficamente, como eles afetam as saídas. As dicas de ferramentas no visualizador mostram a probabilidade e a comparação de precisão associadas a cada par de valores de entrada e saída. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Rede Neural da Microsoft](browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 Para explorar a estrutura de entradas e sub-redes e visualizar estatísticas detalhadas, você pode usar o Visualizador de Árvore de Conteúdo Genérica da Microsoft. É possível clicar em qualquer nó para expandi-lo e visualizar os nós filho ou exibir as ponderações e outras estatísticas contidas no nó.  
  
## <a name="model-content-for-a-logistic-regression-model"></a>Conteúdo de um modelo de regressão logística  
 Esta seção fornece detalhes e exemplos somente para as colunas do conteúdo do modelo de mineração que são relevantes para a regressão logística. O conteúdo do modelo é praticamente idêntico ao de um modelo de rede neural, porém as descrições que se aplicam aos modelos de rede neural podem ser repetidas aqui por conveniência.  
  
 Para obter informações sobre as colunas de uso general no conjunto de linhas de esquema, como MODEL_CATALOG e MODEL_NAME que não são descritos aqui, ou explicações relacionadas à terminologia do modelo de mineração, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
 MODEL_CATALOG  
 Nome do banco de dados no qual o modelo é armazenado.  
  
 MODEL_NAME  
 Nome do modelo.  
  
 ATTRIBUTE_NAME  
 O nome do atributo que corresponde a esse nó.  
  
|Nó|Conteúdo|  
|----------|-------------|  
|Raiz do modelo|Em Branco|  
|Estatísticas marginais|Em Branco|  
|Camada de entrada|Em Branco|  
|Nó de entrada|Nome do atributo de entrada|  
|hidden layer|Em Branco|  
|Camada de saída|Em Branco|  
|Nó de saída|Nome do atributo de saída|  
  
 NODE_NAME  
 O nome do nó. Atualmente, esta coluna contém o mesmo valor de NODE_UNIQUE_NAME, embora isso possa mudar em versões futuras.  
  
 NODE_UNIQUE_NAME  
 Nome exclusivo do nó.  
  
 Para obter mais informações sobre como os nomes e as IDs fornecem dados estruturais sobre o modelo, consulte a seção, [Usando nomes e IDs de nós](#bkmk_NodeIDs).  
  
 NODE_TYPE  
 Um modelo de regressão logística gera os seguintes tipos de nó:  
  
|ID do tipo de nó|Descrição|  
|------------------|-----------------|  
|1|Modelo.|  
|17|Nó do organizador para a sub-rede.|  
|18|Nó do organizador da camada de entrada.|  
|19|Nó do organizador da camada oculta. A camada oculta é vazia.|  
|20|Nó do organizador da camada de saída.|  
|21|Nó do atributo de entrada.|  
|23|Nó do atributo de saída.|  
|24|Nó de estatísticas marginais.|  
  
 NODE_CAPTION  
 Um rótulo ou uma legenda associada ao nó. Em modelos de regressão logística, sempre em branco.  
  
 CHILDREN_CARDINALITY  
 Uma estimativa do número de filhos do nó.  
  
|Nó|Conteúdo|  
|----------|-------------|  
|Raiz do modelo|Indica a contagem de nós filho, que inclui pelo menos 1 rede, 1 nó marginal necessário e 1 camada de entrada necessária. Por exemplo, se o valor for 5, haverá 3 sub-redes.|  
|Estatísticas marginais|Sempre 0.|  
|Camada de entrada|Indica o número de pares de atributo-valores de entrada usados pelo modelo.|  
|Nó de entrada|Sempre 0.|  
|hidden layer|Em um modelo de regressão logística, sempre 0.|  
|Camada de saída|Indica o número de valores de saída.|  
|Nó de saída|Sempre 0.|  
  
 PARENT_UNIQUE_NAME  
 O nome exclusivo do nó pai. NULL é retornado para todos os nós em nível raiz.  
  
 Para obter mais informações sobre como os nomes e as IDs fornecem dados estruturais sobre o modelo, consulte a seção, [Usando nomes e IDs de nós](#bkmk_NodeIDs).  
  
 NODE_DESCRIPTION  
 Uma descrição amigável do nó.  
  
|Nó|Conteúdo|  
|----------|-------------|  
|Raiz do modelo|Em Branco|  
|Estatísticas marginais|Em Branco|  
|Camada de entrada|Em Branco|  
|Nó de entrada|Nome do atributo de entrada|  
|hidden layer|Em Branco|  
|Camada de saída|Em Branco|  
|Nó de saída|Se o atributo de saída for contínuo, conterá o nome do atributo de saída.<br /><br /> Se o atributo de saída for discreto ou diferenciado, contém o nome do atributo e o valor.|  
  
 NODE_RULE  
 Uma descrição XML da regra é inserida no nó.  
  
|Nó|Conteúdo|  
|----------|-------------|  
|Raiz do modelo|Em Branco|  
|Estatísticas marginais|Em Branco|  
|Camada de entrada|Em Branco|  
|Nó de entrada|Um fragmento de XML contendo as mesmas informações que a coluna NODE_DESCRIPTION.|  
|hidden layer|Em Branco|  
|Camada de saída|Em Branco|  
|Nó de saída|Um fragmento de XML contendo as mesmas informações que a coluna NODE_DESCRIPTION.|  
  
 MARGINAL_RULE  
 Em modelos de regressão logística, sempre em branco.  
  
 NODE_PROBABILITY  
 A probabilidade associada a este nó. Em modelos de regressão logística, sempre 0.  
  
 MARGINAL_PROBABILITY  
 A probabilidade de que o nó seja alcançado a partir do nó pai. Em modelos de regressão logística, sempre 0.  
  
 NODE_DISTRIBUTION  
 Uma tabela aninhada que contém informações estatísticas para o nó. Para obter informações detalhadas sobre o conteúdo dessa tabela para cada tipo de nó, consulte a seção Entendendo a tabela NODE_DISTRIBUTION no [Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
 NODE_SUPPORT  
 Em modelos de regressão logística, sempre 0.  
  
> [!NOTE]  
>  O suporte a probabilidades é sempre 0 porque a saída desse tipo modelo não é probabilística. A única coisa significativa para esse algoritmo são as ponderações. Sendo assim, o algoritmo não computa probabilidade, suporte ou variação.  
  
 Para obter informações sobre o suporte nos casos de treinamento para valores específicos, consulte o nó de estatísticas marginais.  
  
 MSOLAP_MODEL_COLUMN  
 |Nó|Conteúdo|  
|----------|-------------|  
|Raiz do modelo|Em Branco|  
|Estatísticas marginais|Em Branco|  
|Camada de entrada|Em Branco|  
|Nó de entrada|Nome do atributo de entrada.|  
|hidden layer|Em Branco|  
|Camada de saída|Em Branco|  
|Nó de saída|Nome do atributo de entrada.|  
  
 MSOLAP_NODE_SCORE  
 Em modelos de regressão logística, sempre 0.  
  
 MSOLAP_NODE_SHORT_CAPTION  
 Em modelos de regressão logística, sempre em branco.  
  
##  <a name="using-node-names-and-ids"></a><a name="bkmk_NodeIDs"></a> Usando nomes e IDs de nós  
 A nomenclatura dos nós em um modelo de regressão logística fornece mais informações sobre os tipos de relações entre os nós no modelo. A tabela a seguir mostra as convenções para as IDs atribuídas aos nós em cada camada.  
  
|Tipo de nó|Convenção da ID de nó|  
|---------------|----------------------------|  
|Raiz do modelo (1)|00000000000000000.|  
|Nó de estatísticas marginais (24)|10000000000000000|  
|Camada de entrada (18)|30000000000000000|  
|Nó de entrada (21)|Inicia em 60000000000000000|  
|Sub-rede (17)|20000000000000000|  
|Camada oculta (19)|40000000000000000|  
|Camada de saída (20)|50000000000000000|  
|Nó de saída (23)|Inicia às 80000000000000000|  
  
 Você pode usar essas IDs para determinar como os atributos de saída são relacionados a atributos específicos da camada de entrada exibindo a tabela NODE_DISTRIBUTION no nó de saída. Cada linha nessa tabela contém uma ID que indica um nó de atributo de entrada específico. A tabela NODE_DISTRIBUTION também contém o coeficiente para o par de entrada-saída.  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo de regressão logística da Microsoft](microsoft-logistic-regression-algorithm.md)   
 [Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services&#41;de mineração de dados](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Exemplos de consulta de modelo de regressão logística](logistic-regression-model-query-examples.md)   
 [Referência técnica do algoritmo Regressão Logística da Microsoft](microsoft-logistic-regression-algorithm-technical-reference.md)  
  
  
