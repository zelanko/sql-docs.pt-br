---
description: Metadados-parâmetro e conjunto de linhas em SQL Server Native Client
title: Metadados de parâmetro e conjunto de linhas (provedor de OLE DB de cliente nativo)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
ms.assetid: 31b318a4-20e7-4db0-b367-eb9938859029
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f45147881ec8cc2c62f8d023a1fe443164682678
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88381742"
---
# <a name="metadata---parameter-and-rowset-in-sql-server-native-client"></a>Metadados-parâmetro e conjunto de linhas em SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Este tópico fornece informações sobre o tipo e os membros de tipo a seguir, relacionados aos aprimoramentos de data e hora de OLE DB.  
  
-   Estrutura DBBINDING  
  
-   **ICommandWithParameters::GetParameterInfo**  
  
-   **ICommandWithParameters::SetParameterInfo**  
  
-   **IColumnsRowset::GetColumnsRowset**  
  
-   **IColumnsInfo::GetColumnInfo**  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 As seguintes informações são retornadas na estrutura DBPARAMINFO por meio de *prgParamInfo*:  
  
|Tipo de parâmetro|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Liberada|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Definir|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Liberada|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Liberada|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21.. 27|0..7|Definir|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28.. 34|0..7|Definir|  
  
 Observe que em alguns casos os intervalos de valores não são contínuos. Isso se deve à adição de um ponto decimal quando a precisão fracionária é maior que zero.  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE só é válido quando conectado a um servidor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior). DBPARAMFLAGS_SS_ISVARIABLESCALE nunca é definido quando conectado a servidores de nível inferior.  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo e tipos de parâmetro implícitos  
 As informações fornecidas na estrutura DBPARAMBINDINFO devem estar de acordo com o seguinte:  
  
|*pwszDataSourceType*<br /><br /> (específico do provedor)|*pwszDataSourceType*<br /><br /> (OLE DB genérico)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|Ignored|  
|date|DBTYPE_DBDATE|6|Ignored|  
||DBTYPE_DBTIME|10|Ignored|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|Ignored|  
|DATETIME||16|Ignored|  
|datetime2 ou DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 O parâmetro *bPrecision* é ignorado.  
  
 "DBPARAMFLAGS_SS_ISVARIABLESCALE" é ignorado ao enviar dados ao servidor. Os aplicativos podem forçar o uso de tipos do protocolo TDS herdados usando os nomes de tipo específicos do provedor "**datetime**" e "**smalldatetime**". Quando estiver conectado a servidores do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior), o formato "**datetime2**" será usado e uma conversão de servidor implícita ocorrerá, se necessário, quando o nome do tipo for "**datetime2**" ou "DBTYPE_DBTIMESTAMP". *bScale* será ignorado se os nomes "**datetime**" ou "**smalldatetime**" específicos do provedor forem usados. Caso contrário, aplicativos deverá garantir que *bScale* esteja definido corretamente. Os aplicativos atualizados do MDAC e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Native Client [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a partir desse uso "DBTYPE_DBTIMESTAMP" falharão se não definirem *bScale* corretamente. Quando estiver conectado a instâncias do servidor anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], um valor *bScale* diferente de 0 ou 3 com "DBTYPE_DBTIMESTAMP" será considerado um erro e E_FAIL será retornado.  
  
 Quando ICommandWithParameters:: SetParameterInfo não é chamado, o provedor imples o tipo de servidor do tipo de associação, conforme especificado em IAccessor:: createaccesser da seguinte maneira:  
  
|Tipo de associação|*pwszDataSourceType*<br /><br /> (específico do provedor)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|date|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|Datetime2 (7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 **IColumnsRowset::GetColumnsRowset** retorna as seguintes colunas:  
  
|Tipo de coluna|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Liberada|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Definir|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Liberada|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Liberada|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Definir|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Definir|  
  
 Em DBCOLUMN_FLAGS, DBCOLUMNFLAGS_ISFIXEDLENGTH é sempre true para os tipos de data/hora e os seguintes sinalizadores são sempre false:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 Os sinalizadores restantes (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE e DBCOLUMNFLAGS_WRITEUNKNOWN) podem ser definidos, dependendo de como a coluna é definida e da consulta propriamente dita.  
  
 Um novo sinalizador DBCOLUMNFLAGS_SS_ISVARIABLESCALE é fornecido em DBCOLUMN_FLAGS para permitir que um aplicativo determine o tipo de servidor de colunas, onde DBCOLUMN_TYPE é DBTYPE_DBTIMESTAMP. DBCOLUMN_SCALE ou DBCOLUMN_DATETIMEPRECISION também deve ser usado para identificar o tipo de servidor.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE só é válido quando conectado a um servidor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (ou posterior). DBCOLUMNFLAGS_SS_ISVARIABLESCALE é indefinido quando conectado a servidores de nível inferior.  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 A estrutura DBCOLUMNINFO retorna as seguintes informações:  
  
|Tipo de parâmetro|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Liberada|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|Definir|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Liberada|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Liberada|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Definir|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Definir|  
  
 Em *dwFlags*, DBCOLUMNFLAGS_ISFIXEDLENGTH sempre tem o valor verdadeiro para os tipos de data/hora e os seguintes sinalizadores sempre têm o valor falso:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER, MAYDEFER  
  
 Os sinalizadores restantes (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE e DBCOLUMNFLAGS_WRITEUNKNOWN) podem ser definidos.  
  
 Um novo sinalizador, DBCOLUMNFLAGS_SS_ISVARIABLESCALE, é fornecido em *dwFlags* para permitir que um aplicativo determine o tipo de servidor de colunas, em que *wType* é DBTYPE_DBTIMESTAMP. *bScale* também precisa ser usado para identificar o tipo de servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Metadados &#40;OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
  
  
