---
title: Transfer Octet Length | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4204b47816747506a5672241eeeef736eca54856
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302807"
---
# <a name="transfer-octet-length"></a>Comprimento do octeto de transferência
O comprimento do octeto de transferência de uma coluna é o número máximo de bytes retornados ao aplicativo quando os dados são transferidos para o seu tipo de dados C padrão. Para os dados de caracteres, o comprimento do octeto de transferência não inclui espaço para o caractere de rescisão nula. O comprimento do octeto de transferência de uma coluna pode ser diferente do número de bytes necessários para armazenar os dados na fonte de dados.  
  
 O comprimento do octeto de transferência definido para cada tipo de dados ODBC SQL é mostrado na tabela a seguir.  
  
|Identificador tipo SQL|Comprimento|  
|-------------------------|------------|  
|Todos os tipos de caracteres[a]|O comprimento definido ou máximo (para tipo variável) da coluna em bytes. Este é o mesmo valor que o campo descritor SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|O número de bytes necessários para manter a representação de caracteres desses dados se o conjunto de caracteres for ANSI e o dobro desse número se o conjunto de caracteres for UNICODE. Este é o número máximo de dígitos mais dois, porque os dados são retornados como uma seqüência de caracteres e caracteres são necessários para os dígitos, um sinal e um ponto decimal. Por exemplo, o comprimento de transferência de uma coluna definida como NUMERIC(10,3) é de 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Todos os tipos binários[a]|O número de bytes necessáriopara manter o número definido (para tipos fixos) ou máximo (para tipos variáveis) de caracteres.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (o tamanho da estrutura SQL_DATE_STRUCT ou SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (o tamanho da estrutura SQL_TIMESTAMP_STRUCT).|  
|Todos os tipos de dados de intervalo|34 (o tamanho da estrutura do intervalo).|  
|SQL_GUID|16 (o tamanho da estrutura GUID).|  
| &nbsp; | &nbsp; |

 [a] Se o driver não puder determinar a coluna ou o comprimento do parâmetro para tipos variáveis, ele retorna SQL_NO_TOTAL.
