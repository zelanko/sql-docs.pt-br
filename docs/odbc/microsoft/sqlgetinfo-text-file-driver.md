---
description: SQLGetInfo (Driver de Arquivo de texto)
title: SQLGetInfo (driver de arquivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ee6d54322d3a72c6b4b0ca31223e70fd44aa2a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421680"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo (Driver de Arquivo de texto)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver de arquivo de texto. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** dá suporte ao tipo de informações SQL_FILE_USAGE. O valor retornado é um inteiro de 16 bits que indica como o driver trata diretamente os arquivos em uma fonte de dados:  
  
-   SQL_FILE_NOT_SUPPORTED-o driver não é um driver de camada única.  
  
-   SQL_FILE_TABLE-um driver de camada única trata arquivos em uma fonte de dados como tabelas.  
  
-   SQL_FILE_QUALIFIER-um driver de camada única trata arquivos em uma fonte de dados como um qualificador.  
  
 O driver ODBC retorna SQL_FILE_TABLE para o textunidader, porque cada arquivo é uma tabela.  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|Format|Versão|Formato dos números de versão|  
|----------|-------------|-------------------------------|  
|Texto|1.0|01.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
