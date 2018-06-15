---
title: Conjunto de linhas DISCOVER_MEMORYUSAGE | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37600d1c99353cd31c1b88bfc6a2893ab968376e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029417"
---
# <a name="discovermemoryusage-rowset"></a>Conjunto de linhas DISCOVER_MEMORYUSAGE
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Retorna as estatísticas DISCOVER_MEMORYUSAGE de vários objetos alocados pelo servidor.  
  
> [!WARNING]  
>  Este conjunto de linhas pode gerar conjuntos de resultados muito grandes. Se não for possível exibir os resultados porque eles exigem mais memória de exibição do que o permitido pelo SQL Server Management Studio, os resultados serão gravados em um arquivo temporário, no seguinte local padrão:  
>   
>  '\<drive>:\Users\\<username\>\AppData\Local\Temp\\<fileID\>.xml'.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DISCOVER_MEMORYUSAGE** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MemoryID**|**DBTYPE_UI8**||Um número que identifica a memória.|  
|**MemoryName**|**DBTYPE_WSTR**||O nome do objeto proprietário da memória.|  
|**SPID**|**DBTYPE_UI4**|Sim|A sessão que alocou a memória. Zero indica memória não associada a uma sessão específica.|  
|**CreationTime**|**DBTYPE_DBTIMESTAMP**||"A hora de criação do objeto" ou "a hora da alocação da memória".|  
|**BaseObjectType**|**DBTYPE_UI4**|Sim|Este é um número que descreve o tipo de objeto. Objetos com o mesmo BaseObjectType têm o mesmo tipo.|  
|**MemoryUsed**|**DBTYPE_UI8**|Sim|Este é o tamanho atual do objeto, que pode ser inferior à memória alocada para uso pelo objeto.|  
|**MemoryAllocated**|**DBTYPE_UI8**||A quantidade de memória alocada para uso pelo objeto, que pode ser superior à quantidade de memória realmente usada pelo objeto.|  
|**MemoryAllocBase**|**DBTYPE_UI8**||Os bytes alocados inicialmente para o próprio objeto (excluindo as alocações adicionais para conteúdos de objeto).|  
|**MemoryAllocFromAlloc**|**DBTYPE_UI8**||A memória alocada para o conteúdo deste objeto.|  
|**elementCount**|**DBTYPE_UI4**||Para um objeto contêiner, este é o número de objetos contido por esse objeto.|  
|**Reduzível**|**DBTYPE_BOOL**|Sim|Um booliano que indica se a memória é reduzível (pode ser removida devido à pressão de memória). Se true, a memória será reduzível; se false, a memória não será reduzível.|  
|**ObjectParentPath**|**DBTYPE_WSTR**||Uma cadeia de caracteres que identifica o caminho completo deste objeto.|  
|**ObjectID**|**DBTYPE_WSTR**||Uma cadeia de caracteres que identifica o objeto. O caminho completo do objeto é representado pela cadeia de caracteres: (ObjectParentPath + '.' + ObjectId).|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|A07CCD21-8148-11D0-87BB-00C04FC33942|  
|ADOMDNAME|MemoryUsage|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
