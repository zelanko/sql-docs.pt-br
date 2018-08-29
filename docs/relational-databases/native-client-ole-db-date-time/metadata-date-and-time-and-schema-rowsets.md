---
title: Data e hora e conjuntos de linhas de esquema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4324cf488325c4fc9ea1ecea2d1f2cb3beb81a00
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43098470"
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>Metadados – conjuntos de linhas de esquema e data e hora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tópico fornece informações sobre os conjuntos de linhas de COLUMNS e de PROCEDURE_PARAMETERS. Essas informações referem-se aos aprimoramentos de data e hora do OLE DB introduzidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="columns-rowset"></a>Conjunto de linhas de COLUMNS  
 Os valores de coluna a seguir são retornados para tipos de data/hora:  
  
|Tipo de coluna|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|Data|DBTYPE_DBDATE|Liberada|0|  
|time|DBTYPE_DBTIME2|Defina|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Liberada|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|Liberada|3|  
|datetime2|DBTYPE_DBTIMESTAMP|Defina|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|Defina|0..7|  
  
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
  
## <a name="procedureparameters-rowset"></a>Conjunto de linhas de PROCEDURE_PARAMETERS  
 DATA_TYPE contém os mesmos valores que o conjunto de linhas de esquema de COLUMNS e TYPE_NAME contém o tipo de servidor.  
  
 Uma nova coluna, SS_DATETIME_PRECISION, foi adicionada para retornar a precisão do tipo como na coluna DATETIME_PRECISION, semelhante ao conjunto de linhas de COLUMNS.  
  
## <a name="providertypes-rowset"></a>Conjunto de linhas de PROVIDER_TYPES  
 As linhas a seguir são retornadas para tipos de data/hora:  
  
|Tipo -><br /><br /> coluna|Data|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|Data|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|scale|NULL|NULL|scale|scale|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|Data|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE a menos que uma das condições a seguir seja verdadeira:<br /><br /> É cliente conectado a um servidor de nível inferior.<br /><br /> A propriedade de conexão de compatibilidade de tipo de dados especifica um nível de compatibilidade igual a 80.|VARIANT_TRUE a menos que uma das condições a seguir seja verdadeira:<br /><br /> É cliente conectado a um servidor de nível inferior.<br /><br /> A propriedade de conexão de compatibilidade de tipo de dados especifica um nível de compatibilidade igual a 80.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 O OLE DB apenas define MINIMUM_SCALE e MAXIMUM_SCALE para tipos decimais e numéricos, portanto, o uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client destas colunas para time, datetime2 e datetimeoffset é não padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Metadados &#40;OLE DB&#41;](http://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
  
  
