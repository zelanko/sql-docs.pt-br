---
title: Conjunto de linhas DMSCHEMA_MINING_STRUCTURES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0aac1d7fb0d8c54ae18cd7b45f5f414a02eafffe
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingstructures-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_STRUCTURES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enumera informações sobre as estruturas de mineração no catálogo atual.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DMSCHEMA_MINING_STRUCTURES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||O nome do catálogo.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||O nome do esquema não qualificado. **NULL** se os esquemas não tiver suporte do provedor.|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**||O nome da estrutura. Esta coluna não pode conter **NULL**.|  
|**STRUCTURE_GUID**|**DBTYPE_GUID**||Um GUID que identifica exclusivamente a estrutura. **NULL** se não tiver suporte do provedor.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição concisa da estrutura. **NULL** se nenhuma descrição estiver associada com a estrutura.|  
|**STRUCTURE_PROPID**|**DBTYPE_UI4**||A ID de propriedade da estrutura. **NULL** se não tiver suporte do provedor.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||A data em que a estrutura foi criada. **NULL** se não for disponibilizado pelo provedor.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||A data em que a estrutura foi modificada pela última vez. **NULL** se não for disponibilizado pelo provedor.|  
|**CREATION_STATEMENT**|**DBTYPE_WSTR**||(Opcional) A instrução usada na criação do modelo de mineração de dados original.|  
|**IS_POPULATED**|**DBTYPE_BOOL**||Um Booliano que indica se a estrutura está preenchida.<br /><br /> Será**VARIANT_TRUE** se a estrutura estiver preenchida; caso contrário, será **VARIANT_FALSE** .|  
|**LAST_PROCESSED**|**DBTYPE_DBTIMESTAMP**||A data em que a estrutura foi processada pela última vez. **NULL** se não for disponibilizado pelo provedor.|  
|**HOLDOUT_MAXPERCENT**|**DBTYPE _ UI1**||Valor especificado pelo usuário que indica a porcentagem máxima das ocorrências de entrada mantidas como o conjunto de testes.<br /><br /> 0 ou **NULL** indica a ausência de limites.|  
|**HOLDOUT_MAXCASES**|**DBTYPE_UI8**||Valor especificado pelo usuário que indica o número máxima das ocorrências de entrada mantidas como o conjunto de testes.<br /><br /> 0 ou **NULL** indica a ausência de limites.|  
|**HOLDOUT_SEED**|**DBTYPE_UI8**||Valor especificado pelo usuário usado como a semente para particionamento repetível.<br /><br /> 0 indica que um hash da ID da estrutura de mineração será usado como a semente.|  
|**HOLDOUT_ACTUAL_SIZE**|**DBTYPE_UI8**||Se a estrutura de mineração for processada, indicará o tamanho real do conjunto de dados de teste, expresso em número de ocorrências.<br /><br /> **NULL** indica que a estrutura de mineração não é processada.|  
  
 O conjunto de linhas é classificado em **STRUCTURE_CATALOG**, **STRUCTURE_SCHEMA**, **STRUCTURE_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DMSCHEMA_MINING_STRUCTURES** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Linhas do esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
