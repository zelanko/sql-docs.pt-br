---
title: Conjunto de linhas DISCOVER_LOCATIONS | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 6d3a1171-8e4d-4022-ade0-b785cf795d70
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90fa167102e9e5a5c8a4ad916bb921205347f1c6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37284432"
---
# <a name="discoverlocations-rowset"></a>Conjunto de linhas DISCOVER_LOCATIONS
  Retorna informações sobre o conteúdo de um arquivo de backup. Você deve ter permissão para acessar o local do arquivo de backup.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_LOCATIONS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`LOCATION_BACKUP_FILE_PATHNAME`|`DBTYPE_WSTR`|Obrigatório, consulte abaixo.|O local do arquivo de backup.|  
|`LOCATION_PARTITION_OBJECTPATH`|`DBTYPE_WSTR`||O caminho para a partição relacionada à pasta de dados.|  
|`LOCATION_PARTITION_DATASOURCEID`|`DBTYPE_WSTR`||A ID da fonte de dados usada no processamento da partição.|  
|`LOCATION_PARTITION_DATASOURCENAME`|`DBTYPE_WSTR`||O nome da fonte de dados usada no processamento.|  
|`LOCATION_PARTITION_NAME`|`DBTYPE_WSTR`||O nome da partição.|  
|`LOCATION_PARTITION_SIZE`|`DBTYPE_WSTR`||O tamanho aproximado da partição.|  
|`LOCATION_CONNECTION_STRING`|`DBTYPE_WSTR`||A cadeia de conexão da fonte de dados usada no processamento.|  
|`LOCATION_PARTITION_FOLDER`|`DBTYPE_WSTR`||O local original dessa partição quando o arquivo de backup foi gerado.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DISCOVER_LOCATIONS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`LOCATION_BACKUP_FILE_PATHNAME`|`DBTYPE_WSTR`|Obrigatório|  
|`LOCATION_PASSWORD PF_DBTYPE`|`DBTYPE_WSTR`|Obrigatório se fosse especificado durante o backup. Essa restrição não é usada para restringir as linhas retornadas. É usada para fornecer a senha para acessar o local.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd92-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|Locais|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
