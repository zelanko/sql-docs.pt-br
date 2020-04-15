---
title: Tamanho do display | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 578bf0cbdf2dd1dbd06dd4a248f4efa5eb839916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307027"
---
# <a name="display-size"></a>Tamanho de exibição
O tamanho da tela de uma coluna é o número máximo de caracteres necessários para exibir dados em forma de caractere. A tabela a seguir define o tamanho do display para cada tipo de dados ODBC SQL.  
  
|Identificador tipo SQL|Tamanho do display|  
|-------------------------|------------------|  
|Todos os tipos de caracteres[a]|O número definido (para tipos fixos) ou máximo (para tipos variáveis) de caracteres necessários para exibir os dados em forma de caractere.|  
|SQL_DECIMAL SQL_NUMERIC|A precisão da coluna mais 2 (um sinal, dígitos de *precisão* e um ponto decimal). Por exemplo, o tamanho do display de uma coluna definida como NUMERIC(10,3) é 12.|  
|SQL_BIT|1 (1 dígito).|  
|SQL_TINYINT|4 se assinado (um sinal e 3 dígitos) ou 3 se não assinado (3 dígitos).|  
|SQL_SMALLINT|6 se assinado (um sinal e 5 dígitos) ou 5 se não assinado (5 dígitos).|  
|SQL_INTEGER|11 se assinado (um sinal e 10 dígitos) ou 10 se não assinado (10 dígitos).|  
|SQL_BIGINT|20 (um sinal e 19 dígitos se assinado ou 20 dígitos se não assinado).|  
|SQL_REAL|14 (um sinal, 7 dígitos, um ponto decimal, a letra *E*, um sinal e 2 dígitos).|  
|SQL_FLOAT SQL_DOUBLE|24 (um sinal, 15 dígitos, um ponto decimal, a letra *E*, um sinal e 3 dígitos).|  
|Todos os tipos binários[a]|O comprimento definido ou máximo (para tipos variáveis) da coluna vezes 2. (Cada byte binário é representado por um número hexadecimal de 2 dígitos.)|  
|SQL_TYPE_DATE|10 (uma data no formato *yyyy-mm-dd*).|  
|SQL_TYPE_TIME|8 (um tempo no formato *hh:mm:ss*)<br /><br /> - ou -<br /><br /> 9 + *s* (um tempo no formato *hh:mm:ss*[.fff...], onde *s* é a precisão de segundos fracionados).|  
|SQL_TYPE_TIMESTAMP|19 (para um carimbo de tempo no formato *yyyy-mm-dd hh:mm:ss)*<br /><br /> - ou -<br /><br /> 20 + *s* (para um carimbo de tempo no formato *yyyy-mm-dd hh:mm:ss*[.fff...], onde *s* é a precisão de segundos fracionados).|  
|Todos os tipos de dados de intervalo|Consulte [o comprimento do tipo de dados do intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md).|  
|SQL_GUID|36 (o número de caracteres no formato *aaaaaaaaaaa-bbbb-cccc-ddddd-eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee*|  
  
 [a] Se o driver não puder determinar a coluna ou o comprimento do parâmetro dos tipos variáveis, ele volta SQL_NO_TOTAL.
