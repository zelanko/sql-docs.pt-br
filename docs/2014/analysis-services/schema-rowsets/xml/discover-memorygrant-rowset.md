---
title: Conjunto de linhas DISCOVER_MEMORYGRANT | Microsoft Docs
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
ms.assetid: d254e42d-9918-47ce-b6df-47f1f0b432dd
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3066a924b572324fcf70dbec7aa726b9ba05f846
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118982"
---
# <a name="discovermemorygrant-rowset"></a>Conjunto de linhas DISCOVER_MEMORYGRANT
  Retorna uma lista de concessões de cota de memória interna que são usadas por trabalhos atualmente em execução no servidor. Para descobrir se um trabalho está sendo executado no servidor, use `Select * from $System.Discover_Jobs`.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_MEMORYGRANT` linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`MEMORY_ID`|**DBTYPE_I8**||Um número que identifica a concessão de cota de memória. Exclusivo no contexto de uma única solicitação DISCOVER_MEMORYGRANT.|  
|`SPID`|`DBTYPE_I4`|Obrigatório|O SPID que você pode obter executando `Select * from $System.Discover_Sessions`.|  
|`CreationTime`|`DBTYPE_I8 DBTYPE_DBTIMESTAMP`||A hora em que a cota foi concedida.|  
|`LastRequestTime`|**DBTYPE_DBTIMESTAMP**||A hora em que a solicitação de cota foi modificada pela última vez.|  
|`MemoryUsed`|`DBTYPE_I4`||A quantidade de memória usada em associação com a cota.|  
|`MemoryGranted`|`DBTYPE_I4`||A quantidade de memória concedida para uso pelo trabalho que está obtendo a cota de memória.|  
|`Blocked`|`DBTYPE_BOOL`||Um booliano que indica o status de bloqueio do trabalho. True indica que o trabalho está bloqueado, aguardando que outro trabalho libere uma cota suficiente para conceder sua solicitação de cota. False indica que o trabalho recebeu sua cota e pode ser executado.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  