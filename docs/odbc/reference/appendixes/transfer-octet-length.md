---
title: Comprimento do octeto de transferência | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff187d5d2b67c5fc3d40a80a136ff9f0c65b2ed2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070039"
---
# <a name="transfer-octet-length"></a>Comprimento do octeto de transferência
O comprimento do octeto de transferência de uma coluna é o número máximo de bytes retornados para o aplicativo quando os dados são transferidos para seu tipo de dados C padrão. Para dados de caractere, o comprimento do octeto de transferência não inclui espaço para o caractere nulo de terminação. O comprimento do octeto de transferência de uma coluna pode ser diferente do número de bytes necessários para armazenar os dados na fonte de dados.  
  
 O comprimento do octeto de transferência definido para cada tipo de dados SQL ODBC é mostrado na tabela a seguir.  
  
|Identificador de tipo SQL|Comprimento|  
|-------------------------|------------|  
|Todos os tipos de caracteres [a]|O definido ou o comprimento máximo (para o tipo de variável) da coluna em bytes. Isso é o mesmo valor que o campo do descritor SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|O número de bytes necessários para armazenar a representação de caracteres desses dados, se o conjunto de caracteres ANSI e duas vezes esse número se o conjunto de caracteres é UNICODE. Isso é o número máximo de dígitos mais dois, porque os dados são retornados como uma cadeia de caracteres e caracteres são necessários para os dígitos, um sinal e um ponto decimal. Por exemplo, o tamanho da transferência de uma coluna definida como NUMERIC(10,3) é 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|O número de bytes necessários para armazenar a representação de caracteres desses dados, se o conjunto de caracteres ANSI e duas vezes esse número se o conjunto de caracteres for UNICODE, porque esse tipo de dados é retornado como uma cadeia de caracteres, por padrão. A representação de caracteres consiste em 20 caracteres: 19 dígitos e um sinal, se assinado ou 20 dígitos, se não tiver sinal. Portanto, o comprimento é 20.|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Todos os tipos binários [a]|O número de bytes necessários para manter o definido (para tipos fixos) ou o número máximo (para tipos de variáveis) de caracteres.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (o tamanho da estrutura SQL_DATE_STRUCT ou SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (o tamanho da estrutura de SQL_TIMESTAMP_STRUCT).|  
|Todos os tipos de dados de intervalo|34 (o tamanho da estrutura de intervalo).|  
|SQL_GUID|16 (o tamanho da estrutura de GUID).|  
  
 [a] se o driver não puder determinar o comprimento de coluna ou parâmetro para tipos de variáveis, ele retornará SQL_NO_TOTAL.
