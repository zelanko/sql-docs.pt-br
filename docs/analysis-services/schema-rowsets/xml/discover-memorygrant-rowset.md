---
title: Conjunto de linhas DISCOVER_MEMORYGRANT | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a19d5520e15df761dc019a994edf7b794ac1eb0f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027626"
---
# <a name="discovermemorygrant-rowset"></a>Conjunto de linhas DISCOVER_MEMORYGRANT
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Retorna uma lista de concessões de cota de memória interna que são usadas por trabalhos atualmente em execução no servidor. Para descobrir se um trabalho está sendo executado no servidor, use `Select * from $System.Discover_Jobs`.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_MEMORYGRANT** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MEMORY_ID**|**DBTYPE_I8**||Um número que identifica a concessão de cota de memória. Exclusivo no contexto de uma única solicitação DISCOVER_MEMORYGRANT.|  
|**SPID**|**DBTYPE_I4**|Obrigatório|O SPID que você pode obter executando `Select * from $System.Discover_Sessions`.|  
|**CreationTime**|**DBTYPE_I8 DBTYPE_DBTIMESTAMP**||A hora em que a cota foi concedida.|  
|**LastRequestTime**|**DBTYPE_DBTIMESTAMP**||A hora em que a solicitação de cota foi modificada pela última vez.|  
|**MemoryUsed**|**DBTYPE_I4**||A quantidade de memória usada em associação com a cota.|  
|**MemoryGranted**|**DBTYPE_I4**||A quantidade de memória concedida para uso pelo trabalho que está obtendo a cota de memória.|  
|**Bloqueado**|**DBTYPE_BOOL**||Um booliano que indica o status de bloqueio do trabalho. True indica que o trabalho está bloqueado, aguardando que outro trabalho libere uma cota suficiente para conceder sua solicitação de cota. False indica que o trabalho recebeu sua cota e pode ser executado.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
