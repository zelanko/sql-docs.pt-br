---
title: Conjunto de linhas DISCOVER_MEMORYUSAGE | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: e416ea61-9615-468c-a96f-bbf731f803b1
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd97d1b2eb02dda3f8add861e6767b7a495a821d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="discovermemoryusage-rowset"></a>Conjunto de linhas DISCOVER_MEMORYUSAGE
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Retorna as estatísticas DISCOVER_MEMORYUSAGE de vários objetos alocados pelo servidor.  
  
> [!WARNING]  
>  Este conjunto de linhas pode gerar conjuntos de resultados muito grandes. Se não for possível exibir os resultados porque eles exigem mais memória de exibição do que o permitido pelo SQL Server Management Studio, os resultados serão gravados em um arquivo temporário, no seguinte local padrão:  
>   
>  '\<unidade >: \Users\\< nome de usuário\>\AppData\Local\Temp\\< fileID\>. XML '.  
  
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
|**ElementCount**|**DBTYPE_UI4**||Para um objeto contêiner, este é o número de objetos contido por esse objeto.|  
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
  
## <a name="see-also"></a>Consulte Também  
 [Conjunto de linhas de esquema do XML](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
