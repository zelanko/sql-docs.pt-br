---
title: Conjunto de linhas DISCOVER_CONNECTIONS | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_CONNECTIONS rowset
ms.assetid: e4703970-c31d-448c-ab68-503303c91aa4
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b02c9f5d9a9e22e626143a6ca5701ac5b1db50e
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverconnections-rowset"></a>Conjunto de linhas DISCOVER_CONNECTIONS
  Oferece uso de recursos e de informações de atividade sobre as conexões atualmente abertas no servidor.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_CONNECTIONS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrições|Description|  
|-----------------|--------------------|------------------|-----------------|  
|**CONNECTION_ID**|**DBTYPE_I4**|Sim|Um número exclusivo que identifica a conexão.|  
|**CONNECTION_USER_NAME**|**DBTYPE_WSTR**|Sim|O nome de usuário da conexão.|  
|**CONNECTION_IMPERSONATED_USER_NAME**|**DBTYPE_WSTR**|Sim|Reservado para uso futuro. O Analysis Services sempre retorna NULL para o valor de CONNECTION_IMPERSONATED_USER_NAME.|  
|**CONNECTION_HOST_NAME**|**DBTYPE_WSTR**|Sim|O nome da máquina que iniciou a conexão.|  
|**CONNECTION_HOST_APPLICATION**|**DBTYPE_WSTR**||O nome do aplicativo que iniciou a conexão.|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||A data e a hora UTC do servidor quando a conexão foi iniciada.|  
|**CONNECTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|Sim|O tempo decorrido, em milissegundos, desde o início da conexão.|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||A data e a hora UTC do servidor quando a execução do último comando foi iniciada.|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||A data e a hora UTC do servidor quando a execução do último comando foi concluída.|  
|**CONNECTION_LAST_COMMAND_ELAPSED_TIME_MS**|**DBTYPE_I8**|Sim|O tempo decorrido, em milissegundos, desde o término do último comando executado.|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**|Sim|O tempo ocioso, em milissegundos, desde o início da conexão.|  
|**CONNECTION_BYTES_SENT**|**DBTYPE_I8**||O número acumulado de bytes enviados pela conexão desde o início da conexão.|  
|**CONNECTION_DATA_BYTES_SENT**|**DBTYPE_I8**||O número acumulado de bytes de dados enviados pela conexão desde o início da conexão.<br /><br /> Os dados viajam compactados pela conexão; esse valor representa os dados expandidos enviados.|  
|**CONNECTION_BYTES_RECEIVED**|**DBTYPE_I8**||O número acumulado de bytes recebidos pela conexão desde o início da conexão.|  
|**CONNECTION_DATA_BYTES_RECEIVED**|**DBTYPE_I8**||O número acumulado de bytes de dados recebidos pela conexão desde o início da conexão.<br /><br /> Os dados viajam compactados pela conexão; esse valor representa os dados expandidos recebidos.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd25-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|Conexões|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

