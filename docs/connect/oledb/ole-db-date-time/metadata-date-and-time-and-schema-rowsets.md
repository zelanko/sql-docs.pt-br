---
title: Data e hora e conjuntos de linhas de esquema | Microsoft Docs
description: Conjuntos de linhas de esquema e de data e hora
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0b854408bff304dd15255b19ab470df41cdb0bc5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>Metadados - data e hora e conjuntos de linhas de esquema
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este tópico fornece informações sobre os conjuntos de linhas de COLUMNS e de PROCEDURE_PARAMETERS. Essas informações referem-se aos aprimoramentos de data e hora do OLE DB introduzidos no [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="columns-rowset"></a>Conjunto de linhas de COLUMNS  
 Os valores de coluna a seguir são retornados para tipos de data/hora:  
  
|Tipo de coluna|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|date|DBTYPE_DBDATE|Liberada|0|  
|time|DBTYPE_DBTIME2|Defina|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Liberada|0|  
|datetime|DBTYPE_DBTIMESTAMP|Liberada|3|  
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
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE só é válido quando conectado a um [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] ou servidor mais recente. DBCOLUMNFLAGS_SS_ISFIXEDSCALE é indefinido quando conectado a servidores de nível inferior.  
  
## <a name="procedureparameters-rowset"></a>Conjunto de linhas de PROCEDURE_PARAMETERS  
 DATA_TYPE contém os mesmos valores que o conjunto de linhas de esquema de COLUMNS e TYPE_NAME contém o tipo de servidor.  
  
 Uma nova coluna, SS_DATETIME_PRECISION, foi adicionada para retornar a precisão do tipo como na coluna DATETIME_PRECISION, semelhante ao conjunto de linhas de COLUMNS.  
  
## <a name="providertypes-rowset"></a>Conjunto de linhas de PROVIDER_TYPES  
 As linhas a seguir são retornadas para tipos de data/hora:  
  
|Tipo -><br /><br /> Coluna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
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
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE a menos que uma das condições a seguir seja verdadeira:<br /><br /> É cliente conectado a um servidor de nível inferior.<br /><br /> A propriedade de conexão de compatibilidade de tipo de dados especifica um nível de compatibilidade igual a 80.|VARIANT_TRUE a menos que uma das condições a seguir seja verdadeira:<br /><br /> É cliente conectado a um servidor de nível inferior.<br /><br /> A propriedade de conexão de compatibilidade de tipo de dados especifica um nível de compatibilidade igual a 80.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB apenas define MINIMUM_SCALE e MAXIMUM_SCALE para tipos numéricos e decimais, OLE DB Driver para uso do SQL Server dessas colunas para time, datetime2 e datetimeoffset é não padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Metadados &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
  
  
