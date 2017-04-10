---
title: "Tipos de dados de inst&#226;ncia Oracle CDC | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eec13d8d-c15a-4542-bfc4-da66b1a6bfe0
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Tipos de dados de inst&#226;ncia Oracle CDC
  A Instância Oracle CDC oferece suporte à maioria dos tipos de dados Oracle. As seções a seguir descrevem os tipos de dados com suporte e sem suporte.  
  
## Tipos de dados com suporte  
 A tabela a seguir descreve os tipos de dados Oracle que podem ser capturados e o seu mapeamento padrão para tipos de dados do SQL Server nas tabelas de alteração. Ao adicionar uma instância de captura para uma tabela do Oracle de origem, você pode substituir alguns destes mapeamentos.  
  
|Tipo de dados de banco de dados Oracle|Tipo de dados do SQL Server|  
|-------------------------------|--------------------------|  
|BINARY_FLOAT|REAL|  
|BINARY_DOUBLE|FLOAT|  
|CHAR|NVARCHAR|  
|DATE|DATETIME|  
|FLOAT|FLOAT|  
|INT|NUMERIC (38)|  
|INTERVAL|DATETIME|  
|NCHAR|NVARCHAR|  
|NUMBER|FLOAT|  
|NAVARCHAR2|NVARCHAR|  
|RAW|VARBINARY|  
|REAL|FLOAT|  
|TIMESTAMP|DATETIME2|  
|TIMESTAMP WITH TIME ZONE|VARCHAR (37)|  
|TIMESTAMP WITH LOCAL TIME ZONE|VARCHAR (37)|  
|VARCHAR2|VARCHAR|  
|XMLTYPE|NVARCHAR (MAX)|  
  
## Tipos de dados sem suporte  
 As tabelas Oracle de origem com colunas dos seguintes tipos de dados Oracle não podem ser capturadas. As colunas capturadas com estes tipos de dados mostrarão como nulo; porém, uma alteração no seu valor é indicada na máscara de alteração das tabelas capturadas.  
  
-   LONG  
  
-   XMLTYPE  
  
-   BLOB  
  
-   CLOB  
  
 As tabelas Oracle de origem com colunas dos seguintes tipos de dados Oracle não podem ser capturadas.  
  
-   BFILE  
  
-   ROWID  
  
-   REF  
  
-   UROWID  
  
-   Tabela aninhada  
  
 Se os seguintes tipos de dados estiverem presentes em uma tabela, eles impedirão que o LogMiner obtenha dados para qualquer coluna da tabela:  
  
-   Tipos de dados definidos pelo usuário  
  
-   VARRAY  
  
## Consulte também  
 [Change Data Capture Designer para Oracle da Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [A instância Oracle CDC](../../integration-services/change-data-capture/the-oracle-cdc-instance.md)  
  
  