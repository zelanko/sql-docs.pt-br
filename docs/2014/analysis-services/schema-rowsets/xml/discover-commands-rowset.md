---
title: Conjunto de linhas DISCOVER_COMMANDS | Microsoft Docs
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
helpviewer_keywords:
- DISCOVER_COMMANDS rowset
ms.assetid: d228f265-05d9-4d2c-a622-44c73eab7a71
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 860645ba09ee294b6421472f235a38d66f54abe8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157317"
---
# <a name="discovercommands-rowset"></a>Conjunto de linhas DISCOVER_COMMANDS
  Oferece uso do recurso e informações de atividade sobre os comandos em execução ou sobre os últimos comandos executados nas conexões abertas no servidor.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_COMMANDS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`SESSION_SPID`|`DBTYPE_I4`|Sim|A ID da sessão.|  
|`SESSION_COMMAND_COUNT`|`DBTYPE_I4`||O número de comandos executados desde o início da sessão.|  
|`COMMAND_START_TIME`|`DBTYPE_DBTIMESTAMP`||A data e a hora de início do último comando, expressas como hora UTC no servidor.|  
|`COMMAND_ELAPSED_TIME_MS`|`DBTYPE_I8`||O tempo decorrido, em milissegundos, desde o início do comando.|  
|`COMMAND_CPU_TIME_MS`|`DBTYPE_I8`||O tempo de CPU, em milissegundos, consumido pelo comando desde o início da sua execução.|  
|`COMMAND_READS`|`DBTYPE_I8`||O número acumulado de leituras de disco desde o início do comando.|  
|`COMMAND_READ_KB`|`DBTYPE_I8`||O valor acumulado de leitura de dados do disco, em quilobytes, desde o início do comando.|  
|`COMMAND_WRITES`|`DBTYPE_I8`||O número acumulado de gravações de disco desde o início do comando.|  
|`COMMAND_WRITE_KB`|`DBTYPE_I8`||O valor acumulado de gravação de dados no disco, em quilobytes, desde o início do comando.|  
|`COMMAND_TEXT`|`DBTYPE_WSTR`||O texto do comando.|  
|`COMMAND_END_TIME`|`DBTYPE_DBTIMESTAMP`||A data e a hora UTC do servidor quando a execução do comando é concluída.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd34-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|Commands|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
