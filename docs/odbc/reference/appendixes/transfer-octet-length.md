---
title: Transferir o comprimento do octeto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59b790845ee6360edcb5c5ea796e9ad910c397a4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="transfer-octet-length"></a>Comprimento do octeto transferência
O comprimento de octetos de transferência de uma coluna é o número máximo de bytes retornados para o aplicativo quando os dados são transferidos para seu tipo de dados C padrão. Para dados de caracteres, o comprimento de octetos de transferência não inclui o espaço para o caractere null de terminação. O comprimento de octetos de transferência de uma coluna pode ser diferente do número de bytes necessários para armazenar os dados na fonte de dados.  
  
 O comprimento de octetos de transferência definido para cada tipo de dados SQL ODBC é mostrado na tabela a seguir.  
  
|Identificador de tipo SQL|Comprimento|  
|-------------------------|------------|  
|Todos os tipos de caracteres [a]|O definido ou o comprimento máximo (para o tipo de variável) da coluna em bytes. Este é o mesmo valor que o campo do descritor SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|O número de bytes necessários para manter a representação de caracteres de dados se o conjunto de caracteres ANSI e duas vezes esse número se o conjunto de caracteres UNICODE. Este é o número máximo de dígitos mais dois, porque os dados são retornados como uma cadeia de caracteres e caracteres são necessárias para os dígitos, um logon e um ponto decimal. Por exemplo, o tamanho da transferência de uma coluna definida como NUMERIC(10,3) é 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|O número de bytes necessários para manter a representação de caracteres de dados se o conjunto de caracteres ANSI e duas vezes esse número se o conjunto de caracteres for UNICODE, porque esse tipo de dados é retornado como uma cadeia de caracteres, por padrão. A representação de caracteres consiste em 20 caracteres: 19 dígitos e um sinal, se conectado ou 20 dígitos, se não assinado. Portanto, o comprimento é 20.|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Todos os tipos binários [a]|O número de bytes necessários para manter o definido (para tipos fixos) ou o número máximo (para tipos de variável) de caracteres.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (o tamanho da estrutura de SQL_DATE_STRUCT ou SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (o tamanho da estrutura de SQL_TIMESTAMP_STRUCT).|  
|Todos os tipos de dados de intervalo|34 (o tamanho da estrutura de intervalo).|  
|SQL_GUID|16 (o tamanho da estrutura de GUID).|  
  
 [a] se o driver não pode determinar o comprimento de coluna ou parâmetro para tipos de variáveis, ela retornará SQL_NO_TOTAL.
