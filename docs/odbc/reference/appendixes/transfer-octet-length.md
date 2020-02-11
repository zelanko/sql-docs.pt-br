---
title: Comprimento do octeto de transferência | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
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
ms.openlocfilehash: a92a9ead66736ff2b72813d6d4cbec5acfcda4fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73032967"
---
# <a name="transfer-octet-length"></a>Comprimento do octeto de transferência
O comprimento do octeto de transferência de uma coluna é o número máximo de bytes retornados para o aplicativo quando os dados são transferidos para seu tipo de dados C padrão. Para dados de caractere, o comprimento do octeto de transferência não inclui espaço para o caractere de terminação nula. O comprimento do octeto de transferência de uma coluna pode ser diferente do número de bytes necessários para armazenar os dados na fonte de dados.  
  
 O comprimento do octeto de transferência definido para cada tipo de dados SQL ODBC é mostrado na tabela a seguir.  
  
|Identificador de tipo SQL|Comprimento|  
|-------------------------|------------|  
|Todos os tipos de caractere [a]|O comprimento definido ou máximo (para o tipo de variável) da coluna em bytes. Esse é o mesmo valor que o campo de descritor SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|O número de bytes necessários para manter a representação de caracteres desses dados se o conjunto de caracteres for ANSI e o dobro desse número se o conjunto de caracteres for UNICODE. Esse é o número máximo de dígitos mais dois, pois os dados são retornados como uma cadeia de caracteres e os caracteres são necessários para os dígitos, um sinal e um ponto decimal. Por exemplo, o comprimento da transferência de uma coluna definida como numérica (10, 3) é 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Todos os tipos binários [a]|O número de bytes necessários para manter o número de caracteres definido (para tipos fixos) ou máximo (para tipos de variável).|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (o tamanho da estrutura SQL_DATE_STRUCT ou SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (o tamanho da estrutura de SQL_TIMESTAMP_STRUCT).|  
|Todos os tipos de dados de intervalo|34 (o tamanho da estrutura do intervalo).|  
|SQL_GUID|16 (o tamanho da estrutura de GUID).|  
| &nbsp; | &nbsp; |

 [a] se o driver não puder determinar o comprimento da coluna ou do parâmetro para tipos de variáveis, ele retornará SQL_NO_TOTAL.
