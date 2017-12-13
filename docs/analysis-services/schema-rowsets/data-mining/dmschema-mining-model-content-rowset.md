---
title: Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_MODEL_CONTENT
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_MODEL_CONTENT rowset
ms.assetid: 1e85d9e7-3b74-42ac-b94e-f52f76d8a25d
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d0bd29ab1dcd96412710e9d79255119489253bde
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="dmschemaminingmodelcontent-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Permite que o aplicativo cliente procurar o conteúdo de um modelo de mineração de dados. Os aplicativos cliente podem usar as restrições de operação de árvore especiais descritas no fim deste tópico para navegar no conteúdo do modelo de mineração.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DMSCHEMA_MINING_MODEL_CONTENT** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||O nome do catálogo. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] preenche essa coluna com o nome do banco de dados do qual o modelo é um membro.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||O nome do esquema não qualificado. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **VT_NULL**.|  
|**NOME_DO_MODELO**|**DBTYPE_WSTR**||O nome do modelo ao qual o conteúdo descrito por esta linha é associado.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||Os nomes dos atributos que correspondem a este nó.|  
|**NODE_NAME**|**DBTYPE_WSTR**||O nome do nó. No momento, esta coluna contém o mesmo valor como **NODE_UNIQUE_NAME**, embora isso possa mudar em versões futuras.|  
|**NODE_UNIQUE_NAME**|**DBTYPE_WSTR**||Nome exclusivo do nó.|  
|**NODE_TYPE**|**DBTYPE_I4**||O tipo do nó. Gera um dos valores a seguir (algoritmos de mineração de dados de terceiros podem estender esta lista):<br /><br /> **DM_NODE_TYPE_CLASSIFICATION_TREE_ROOT** (**2**)<br /><br /> **DM_NODE_TYPE_TREE_INTERIOR** (**3**)<br /><br /> **DM_NODE_TYPE_TREE_DISTRIBUTION** (**4**)<br /><br /> **DM_NODE_TYPE_CLUSTER** (**5**)<br /><br /> **DM_NODE_TYPE_UNKNOWN** (**6**)<br /><br /> **DM_NODE_TYPE_ITEMSET** (**7**)<br /><br /> **DM_NODE_TYPE_ASSOCIATION_RULE** (**8**)<br /><br /> **DM_NODE_TYPE_NB_PREDICTABLE_ATTRIBUTE** (**9**)<br /><br /> **DM_NODE_TYPE_NB_INPUT_ATTRIBUTE** (**10**)<br /><br /> **DM_NODE_TYPE_NB_INPUT_ATTRIBUTE_STATE** (**11**)<br /><br /> **DM_NODE_TYPE_SEQUENCE** (**13**)<br /><br /> **DM_NODE_TYPE_TRANSITION** (**14**)<br /><br /> **DM_NODE_TYPE_TIME_SERIES** (**15**)<br /><br /> **DM_NODE_TYPE_TS_TREE** (**16**)<br /><br /> **DM_NODE_TYPE_NN_SUBNETWORK** (**17**) rede Neural, sub-rede<br /><br /> **DM_NODE_TYPE_NN_INPUT_LAYER** (**18**) rede Neural, camada de entrada (pai de nós de entrada)<br /><br /> **DM_NODE_TYPE_NN_HIDDEN_LAYER** (**19**) rede Neural, camada oculta (pai de nós ocultos)<br /><br /> **DM_NODE_TYPE_NN_OUTPUT_LAYER** (**20**) rede Neural, camada de saída (pai de nós de saída)<br /><br /> **DM_NODE_TYPE_NN_INPUT_NODE** (**21**) rede Neural, nó de entrada<br /><br /> **DM_NODE_TYPE_NN_HIDDEN_NODE** (**22**) rede Neural, nó oculto<br /><br /> **DM_NODE_TYPE_NN_OUTPUT_NODE** (**23**) rede Neural, nó de saída<br /><br /> **DM_NODE_TYPE_NN_MARGINAL_STAT_NODE** (**24**) rede Neural, nó de estatísticas marginais<br /><br /> **DM_NODE_TYPE_REGRESSION_TREE_ROOT** (**25**)<br /><br /> **DM_NODE_TYPE_NB_MARGINAL_STAT_NODE** (**26**) rede Neural, nó de estatísticas marginais|  
|**NODE_GUID**|**DBTYPE_GUID**||Nó GUID. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**NODE_CAPTION**|**DBTYPE_WSTR**||Um rótulo ou uma legenda associada ao nó. Essa propriedade é usada principalmente para exibição.|  
|**CHILDREN_CARDINALITY**|**DBTYPE_UI4**||Uma estimativa do número de filhos do nó.|  
|**PARENT_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo do nó pai. **NULO** é retornado para todos os nós no nível raiz.|  
|**NODE_DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição amigável do nó.|  
|**NODE_RULE**|**DBTYPE_WSTR**||Uma descrição XML da regra é inserida no nó.|  
|**MARGINAL_RULE**|**DBTYPE_WSTR**||A descrição XML da regra que se move para o nó a partir do nó pai.|  
|**NODE_PROBABILITY**|**DBTYPE_R8**||A probabilidade associada a este nó.|  
|**MARGINAL_PROBABILITY**|**DBTYPE_R8**||A probabilidade de que o nó seja alcançado a partir do nó pai.|  
|**NODE_DISTRIBUTION**|**DBTYPE_HCHAPTER**||Um tabela que contém o histograma de probabilidade do nó.|  
|**NODE_SUPPORT**|**DBTYPE_R8**||O número de casos com suporte para este nó.|  
|**MSOLAP_MODEL_COLUMN**|**DBTYPE_WSTR**||O nome da coluna da definição do modelo a qual este nó pertence.|  
|**MSOLAP_NODE_SCORE**|**DBTYPE_R8**||A pontuação computada para este nó.|  
|**MSOLAP_NODE_SHORT_CAPTION**|**DBTYPE_WSTR**||Uma legenda curta para o nó que pode ser usado para monitoramento e assim melhorar a legibilidade.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **DMSCHEMA_MINING_MODEL_CONTENT** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**NOME_DO_MODELO**|**DBTYPE_WSTR**|Opcional.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NODE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NODE_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NODE_TYPE**|**DBTYPE_I4**|Opcional.|  
|**NODE_GUID**|**DBTYPE_WSTR**|Opcional.|  
|**NODE_CAPTION**|**DBTYPE_WSTR**|Opcional.|  
|**TREE_OPERATION**|**DBTYPE_UI4**|Opcional. Consulte os comentários adicionais a seguir.|  
  
 A restrição, **TREE_OPERATION**, não está em qualquer coluna específica do **DMSCHEMA_MINING_MODEL_CONTENT** linhas; em vez disso, ele especifica um operador de árvore. O consumidor pode especificar um **NODE_UNIQUE_NAME** restrição e o operador de árvore (**ancestrais**, **FILHOS**, **irmãos**,  **PAI**, **descendentes**, **SELF**) para obter o conjunto de membros solicitado. O **SELF** operador inclui a linha para o próprio nó na lista de linhas retornadas. A tabela a seguir descreve as constantes que compõem a definição de bitmap para o **TREE_OPERATION** restrição. Eles podem ser combinados usando lógico **ou** operador.  
  
|Constante|Valor|  
|--------------|-----------|  
|**DMTREEOP_ANCESTORS**|**0x00000020**|  
|**DMTREEOP_CHILDREN**|**0x00000001**|  
|**DMTREEOP_SIBLINGS**|**0x00000002**|  
|**DMTREEOP_PARENT**|**0x00000004**|  
|**DMTREEOP_SELF**|**0x00000008**|  
|**DMTREEOP_DESCENDANTS**|**0x00000010**|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
