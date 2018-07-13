---
title: Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_MODEL_CONTENT
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT rowset
ms.assetid: 1e85d9e7-3b74-42ac-b94e-f52f76d8a25d
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76724967936008e52cb43f7af02bbb7a833475d0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165447"
---
# <a name="dmschemaminingmodelcontent-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT
  Permite que o aplicativo cliente procure o conteúdo de um modelo de mineração de dados. Os aplicativos cliente podem usar as restrições de operação de árvore especiais descritas no fim deste tópico para navegar no conteúdo do modelo de mineração.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DMSCHEMA_MINING_MODEL_CONTENT` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||O nome do catálogo. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] preenche esta coluna com o nome do banco de dados do qual o modelo é um membro.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||O nome do esquema não qualificado. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `VT_NULL`.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||O nome do modelo ao qual o conteúdo descrito por esta linha é associado.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||Os nomes dos atributos que correspondem a este nó.|  
|`NODE_NAME`|`DBTYPE_WSTR`||O nome do nó. No momento, esta coluna contém o mesmo valor de `NODE_UNIQUE_NAME`, embora isso possa mudar em versões futuras.|  
|`NODE_UNIQUE_NAME`|`DBTYPE_WSTR`||Nome exclusivo do nó.|  
|`NODE_TYPE`|`DBTYPE_I4`||O tipo do nó. Gera um dos valores a seguir (algoritmos de mineração de dados de terceiros podem estender esta lista):<br /><br /> -   `DM_NODE_TYPE_CLASSIFICATION_TREE_ROOT` (`2`)<br />-   `DM_NODE_TYPE_TREE_INTERIOR` (`3`)<br />-   `DM_NODE_TYPE_TREE_DISTRIBUTION` (`4`)<br />-   `DM_NODE_TYPE_CLUSTER` (`5`)<br />-   `DM_NODE_TYPE_UNKNOWN` (`6`)<br />-   `DM_NODE_TYPE_ITEMSET` (`7`)<br />-   `DM_NODE_TYPE_ASSOCIATION_RULE` (`8`)<br />-   `DM_NODE_TYPE_NB_PREDICTABLE_ATTRIBUTE` (`9`)<br />-   `DM_NODE_TYPE_NB_INPUT_ATTRIBUTE` (`10`)<br />-   `DM_NODE_TYPE_NB_INPUT_ATTRIBUTE_STATE` (`11`)<br />-   `DM_NODE_TYPE_SEQUENCE` (`13`)<br />-   `DM_NODE_TYPE_TRANSITION` (`14`)<br />-   `DM_NODE_TYPE_TIME_SERIES` (`15`)<br />-   `DM_NODE_TYPE_TS_TREE` (`16`)<br />-   `DM_NODE_TYPE_NN_SUBNETWORK` (`17`) Rede neural, sub-rede<br />-   `DM_NODE_TYPE_NN_INPUT_LAYER` (`18`) Rede neural, camada de entrada (pai de nós de entrada)<br />-   **DM_NODE_TYPE_NN_HIDDEN_LAYER** (`19`) rede Neural, camada oculta (pai de nós ocultos)<br />-   `DM_NODE_TYPE_NN_OUTPUT_LAYER` (`20`) Rede neural, camada de saída (pai de nós de saída)<br />-   `DM_NODE_TYPE_NN_INPUT_NODE` (`21`) Rede neural, nó de entrada<br />-   `DM_NODE_TYPE_NN_HIDDEN_NODE` (`22`) Rede neural, nó oculto<br />-   `DM_NODE_TYPE_NN_OUTPUT_NODE` (`23`) Rede neural, nó de saída<br />-   `DM_NODE_TYPE_NN_MARGINAL_STAT_NODE` (`24`) Rede neural, nó de estatísticas marginais<br />-   **DM_NODE_TYPE_REGRESSION_TREE_ROOT** (`25`)<br />-   `DM_NODE_TYPE_NB_MARGINAL_STAT_NODE` (`26`) Rede neural, nó de estatísticas marginais|  
|`NODE_GUID`|`DBTYPE_GUID`||Nó GUID. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá `NULL`.|  
|`NODE_CAPTION`|`DBTYPE_WSTR`||Um rótulo ou uma legenda associada ao nó. Essa propriedade é usada principalmente para exibição.|  
|`CHILDREN_CARDINALITY`|`DBTYPE_UI4`||Uma estimativa do número de filhos do nó.|  
|`PARENT_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo do nó pai. `NULL` é retornado para todos os nós em nível raiz.|  
|`NODE_DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição amigável do nó.|  
|`NODE_RULE`|`DBTYPE_WSTR`||Uma descrição XML da regra é inserida no nó.|  
|`MARGINAL_RULE`|`DBTYPE_WSTR`||A descrição XML da regra que se move para o nó a partir do nó pai.|  
|`NODE_PROBABILITY`|`DBTYPE_R8`||A probabilidade associada a este nó.|  
|`MARGINAL_PROBABILITY`|`DBTYPE_R8`||A probabilidade de que o nó seja alcançado a partir do nó pai.|  
|`NODE_DISTRIBUTION`|`DBTYPE_HCHAPTER`||Um tabela que contém o histograma de probabilidade do nó.|  
|`NODE_SUPPORT`|`DBTYPE_R8`||O número de casos com suporte para este nó.|  
|`MSOLAP_MODEL_COLUMN`|`DBTYPE_WSTR`||O nome da coluna da definição do modelo a qual este nó pertence.|  
|`MSOLAP_NODE_SCORE`|`DBTYPE_R8`||A pontuação computada para este nó.|  
|`MSOLAP_NODE_SHORT_CAPTION`|`DBTYPE_WSTR`||Uma legenda curta para o nó que pode ser usado para monitoramento e assim melhorar a legibilidade.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DMSCHEMA_MINING_MODEL_CONTENT` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`NODE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`NODE_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`NODE_TYPE`|`DBTYPE_I4`|Opcional.|  
|`NODE_GUID`|`DBTYPE_WSTR`|Opcional.|  
|`NODE_CAPTION`|`DBTYPE_WSTR`|Opcional.|  
|`TREE_OPERATION`|`DBTYPE_UI4`|Opcional. Consulte os comentários adicionais a seguir.|  
  
 A restrição, `TREE_OPERATION`, não está em qualquer coluna específica do conjunto de linhas `DMSCHEMA_MINING_MODEL_CONTENT`; em vez disso, especifica um operador de árvore. O consumidor pode especificar uma restrição `NODE_UNIQUE_NAME` e o operador de árvore (`ANCESTORS`, `CHILDREN`, `SIBLINGS`, `PARENT`, `DESCENDANTS`, `SELF`) para obter o conjunto de membros solicitado. O operador `SELF` inclui a linha para o próprio nó na lista de linhas retornadas. A tabela a seguir descreve as constantes que compõem a definição de bitmap para a restrição `TREE_OPERATION`. Elas podem ser combinadas por meio de um operador lógico `OR`.  
  
|Constante|Valor|  
|--------------|-----------|  
|**DMTREEOP_ANCESTORS**|`0x00000020`|  
|**DMTREEOP_CHILDREN**|`0x00000001`|  
|**DMTREEOP_SIBLINGS**|`0x00000002`|  
|**DMTREEOP_PARENT**|`0x00000004`|  
|**DMTREEOP_SELF**|`0x00000008`|  
|**DMTREEOP_DESCENDANTS**|`0x00000010`|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema de mineração de dados](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
