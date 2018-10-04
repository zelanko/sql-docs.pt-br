---
title: Conjunto de linhas DISCOVER_CONNECTIONS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DISCOVER_CONNECTIONS rowset
ms.assetid: e4703970-c31d-448c-ab68-503303c91aa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3718045bc6fdcc6d83fd862bbf1f45dce96492dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171466"
---
# <a name="discoverconnections-rowset"></a>Conjunto de linhas DISCOVER_CONNECTIONS
  Oferece uso de recursos e de informações de atividade sobre as conexões atualmente abertas no servidor.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_CONNECTIONS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrictions|Description|  
|-----------------|--------------------|------------------|-----------------|  
|`CONNECTION_ID`|`DBTYPE_I4`|Sim|Um número exclusivo que identifica a conexão.|  
|`CONNECTION_USER_NAME`|`DBTYPE_WSTR`|Sim|O nome de usuário da conexão.|  
|`CONNECTION_IMPERSONATED_USER_NAME`|`DBTYPE_WSTR`|Sim|Reservado para uso futuro. O Analysis Services sempre retorna NULL para o valor de CONNECTION_IMPERSONATED_USER_NAME.|  
|`CONNECTION_HOST_NAME`|`DBTYPE_WSTR`|Sim|O nome da máquina que iniciou a conexão.|  
|`CONNECTION_HOST_APPLICATION`|`DBTYPE_WSTR`||O nome do aplicativo que iniciou a conexão.|  
|`CONNECTION_START_TIME`|`DBTYPE_DBTIMESTAMP`||A data e a hora UTC do servidor quando a conexão foi iniciada.|  
|`CONNECTION_ELAPSED_TIME_MS`|`DBTYPE_I8`|Sim|O tempo decorrido, em milissegundos, desde o início da conexão.|  
|`CONNECTION_LAST_COMMAND_START_TIME`|`DBTYPE_DBTIMESTAMP`||A data e a hora UTC do servidor quando a execução do último comando foi iniciada.|  
|`CONNECTION_LAST_COMMAND_END_TIME`|`DBTYPE_DBTIMESTAMP`||A data e a hora UTC do servidor quando a execução do último comando foi concluída.|  
|`CONNECTION_LAST_COMMAND_ELAPSED_TIME_MS`|`DBTYPE_I8`|Sim|O tempo decorrido, em milissegundos, desde o término do último comando executado.|  
|`CONNECTION_IDLE_TIME_MS`|`DBTYPE_I8`|Sim|O tempo ocioso, em milissegundos, desde o início da conexão.|  
|`CONNECTION_BYTES_SENT`|`DBTYPE_I8`||O número acumulado de bytes enviados pela conexão desde o início da conexão.|  
|`CONNECTION_DATA_BYTES_SENT`|`DBTYPE_I8`||O número acumulado de bytes de dados enviados pela conexão desde o início da conexão.<br /><br /> Os dados viajam compactados pela conexão; esse valor representa os dados expandidos enviados.|  
|`CONNECTION_BYTES_RECEIVED`|`DBTYPE_I8`||O número acumulado de bytes recebidos pela conexão desde o início da conexão.|  
|`CONNECTION_DATA_BYTES_RECEIVED`|`DBTYPE_I8`||O número acumulado de bytes de dados recebidos pela conexão desde o início da conexão.<br /><br /> Os dados viajam compactados pela conexão; esse valor representa os dados expandidos recebidos.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd25-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|Conexões|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
