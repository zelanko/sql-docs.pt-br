---
title: Conjuntos de linhas de esquema e data e hora | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 710fbfdfd57608c24c56def1f2f9c4ec373f1957
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63238013"
---
# <a name="date-and-time-and-schema-rowsets"></a>Conjuntos de linhas de data e hora e esquema
  Este tópico fornece informações sobre os conjuntos de linhas de COLUMNS e de PROCEDURE_PARAMETERS. Essas informações referem-se aos aprimoramentos de data e hora do OLE DB introduzidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="columns-rowset"></a>Conjunto de linhas de COLUMNS  
 Os valores de coluna a seguir são retornados para tipos de data/hora:  
  
|Tipo de coluna|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|date|DBTYPE_DBDATE|Liberada|0|  
|time|DBTYPE_DBTIME2|Definir|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Liberada|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|Liberada|3|  
|datetime2|DBTYPE_DBTIMESTAMP|Definir|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|Definir|0..7|  
  
 Em COLUMN_FLAGS, DBCOLUMNFLAGS_ISFIXEDLENGTH é sempre true para tipos de data/hora e os sinalizadores seguintes sempre é false:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 Os sinalizadores restantes (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE e DBCOLUMNFLAGS_WRITEUNKNOWN) podem ser definidos, dependendo de como a coluna é definida.  
  
 Um novo sinalizador, DBCOLUMNFLAGS_SS_ISVARIABLESCALE, é fornecido em COLUMN_FLAGS para permitir que um aplicativo determine o tipo de servidor de colunas em que DATA_TYPE é DBTYPE_DBTIMESTAMP. DATETIME_PRECISION também deve ser usado para identificar o tipo de servidor.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE só é válido quando conectado a um servidor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior. DBCOLUMNFLAGS_SS_ISFIXEDSCALE é indefinido quando conectado a servidores de nível inferior.  
  
## <a name="procedure_parameters-rowset"></a>Conjunto de linhas de PROCEDURE_PARAMETERS  
 DATA_TYPE contém os mesmos valores que o conjunto de linhas de esquema de COLUMNS e TYPE_NAME contém o tipo de servidor.  
  
 Uma nova coluna, SS_DATETIME_PRECISION, foi adicionada para retornar a precisão do tipo como na coluna DATETIME_PRECISION, semelhante ao conjunto de linhas de COLUMNS.  
  
## <a name="provider_types-rowset"></a>Conjunto de linhas de PROVIDER_TYPES  
 As linhas a seguir são retornadas para tipos de data/hora:  
  
|Tipo -><br /><br /> Coluna|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULO|scale|NULO|NULO|scale|scale|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULO|NULO|NULO|NULO|NULO|NULO|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULO|0|NULO|NULO|0|0|  
|MAXIMUM_SCALE|NULO|7|NULO|NULO|7|7|  
|GUID|NULO|NULO|NULO|NULO|NULO|NULO|  
|TYPELIB|NULO|NULO|NULO|NULO|NULO|NULO|  
|VERSION|NULO|NULO|NULO|NULO|NULO|NULO|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE a menos que uma das condições a seguir seja verdadeira:<br /><br /> -O cliente está conectado a um servidor de nível inferior.<br />-A propriedade de conexão de compatibilidade de tipo de dados especifica um nível de compatibilidade igual a 80.|VARIANT_TRUE a menos que uma das condições a seguir seja verdadeira:<br /><br /> -O cliente está conectado a um servidor de nível inferior.<br />-A propriedade de conexão de compatibilidade de tipo de dados especifica um nível de compatibilidade igual a 80.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 O OLE DB apenas define MINIMUM_SCALE e MAXIMUM_SCALE para tipos decimais e numéricos, portanto, o uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client destas colunas para time, datetime2 e datetimeoffset é não padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Metadados &#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
  
  
