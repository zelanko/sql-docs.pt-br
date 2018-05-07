---
title: Conjunto de linhas DMSCHEMA_MINING_MODELS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cd9f66d6fc8155c8390f45130f1354f9d223bc81
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="dmschemaminingmodels-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_MODELS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enumera os modelos de mineração de dados no catálogo atual. O **DMSCHEMA_MINING_MODELS** conjunto de linhas inclui informações como nomes de modelo, data de processamento e o algoritmo de mineração associados a cada modelo de mineração.  
  
 . O **DMSCHEMA_MINING_MODELS** de linhas de esquema é muito semelhante do [DBSCHEMA_TABLES](../../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md) de linhas de esquema e podem ser usados da mesma maneira.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DMSCHEMA_MINING_MODELS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|O nome do catálogo. Preenchido com o nome do banco de dados do qual o modelo é membro.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|O nome do esquema não qualificado. Esta coluna não é suportada pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**NOME_DO_MODELO**|**DBTYPE_WSTR**|O nome do modelo de mineração. Esta coluna contém o nome do modelo de mineração e nunca está vazia.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|O tipo de modelo.|  
|**MODEL_GUID**|**DBTYPE_GUID**|O GUID do modelo.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Uma descrição amigável do modelo.|  
|**MODEL_PROPID**|**DBTYPE_UI4**|A ID de propriedade do modelo. Esta coluna não é suportada pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; sempre conterá **nulo**.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**|A data em que o modelo foi criado.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**|A data na qual a definição do modelo foi modificada pela última vez.|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|Uma enumeração que identifica o tipo de algoritmo de mineração de dados usado pelo modelo. Esse tipo pode ser um dos seguintes valores:<br /><br /> **DM_SERVICETYPE_CLASSIFICATION** (1)<br /><br /> **DM_SERVICETYPE_SEGMENTATION**(2)<br /><br /> **ASSOCIAÇÃO DE DM_SERVICETYPE_**(4)<br /><br /> **DM_SERVICETYPE_ DENSITY_ESTIMATE**(8)<br /><br /> **DM_SERVICETYPE_SEQUENCE**(16)|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|O nome específico do provedor para o algoritmo de mineração de dados usado pelo modelo.|  
|**CREATION_STATEMENT**|**DBTYPE_WSTR**|A instrução usada na criação do modelo de mineração.|  
|**PREDICTION_ENTITY**|**DBTYPE_WSTR**|Uma lista delimitada por vírgulas que indica quais colunas de mineração poderão ser previstas.|  
|**IS_POPULATED**|**DBTYPE_BOOL**|Um sinalizador Booliano que indica se o modelo está preenchido.<br /><br /> **TRUE** se o modelo é populado; caso contrário, **FALSE**.|  
|**MINING_PARAMETERS**|**DBTYPE_WSTR**|Uma lista separada por vírgulas dos parâmetros usados quando o modelo foi criado.|  
|**MINING_STRUCTURE**|**DBTYPE_WSTR**|A ID da estrutura de mineração em que o modelo se baseia.|  
|**LAST_PROCESSED**|**DBTYPE_DBTIMESTAMP**|A data em que o modelo foi processado pela última vez.|  
|**MSOLAP_IS_DRILLTHROUGH_ENABLED**|**DBTYPE_BOOL**|Um sinalizador Booliano que indica se o modelo oferece suporte a detalhamento.|  
|**FILTRO**|**DBTYPE_WSTR**|A expressão de filtro associada ao modelo de mineração.<br /><br /> NULL ou uma cadeia de caracteres vazia indica que nenhum filtro foi aplicado.|  
|**TRAINING_SET_SIZE**|**DBTYPE_UIS**|O número de casos contidos no conjunto de treinamento do modelo de mineração após o processamento da estrutura e da aplicação de qualquer filtro ao modelo.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **DMSCHEMA_MINING_MODELS** linhas pode ser restringido nas colunas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**NOME_DO_MODELO**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|Opcional.|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|Opcional.|  
|**MINING_STRUCTURE**|**DBTYPE_WSTR**|Opcional.|  
  
 Para obter exemplos de como consultar esse conjunto de linhas, consulte [consultar os parâmetros usados para criar um modelo de mineração](../../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md).  
  
## <a name="see-also"></a>Consulte também  
 [Linhas do esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
