---
description: Tamanho de exibição
title: Tamanho de exibição | Microsoft Docs
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
ms.openlocfilehash: 747c2076c528df8c312c9b3ed45e45a165299d59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456581"
---
# <a name="display-size"></a>Tamanho de exibição
O tamanho de exibição de uma coluna é o número máximo de caracteres necessários para exibir dados no formato de caractere. A tabela a seguir define o tamanho de exibição para cada tipo de dados ODBC SQL.  
  
|Identificador de tipo SQL|Tamanho de exibição|  
|-------------------------|------------------|  
|Todos os tipos de caractere [a]|O número de caracteres definido (para tipos fixos) ou máximo (para tipos de variável) necessários para exibir os dados no formato de caractere.|  
|SQL_DECIMAL SQL_NUMERIC|A precisão da coluna mais 2 (um sinal, dígitos de *precisão* e um ponto decimal). Por exemplo, o tamanho de exibição de uma coluna definida como NUMERIC (10, 3) é 12.|  
|SQL_BIT|1 (1 dígito).|  
|SQL_TINYINT|4 se assinado (um sinal e 3 dígitos) ou 3 se não assinado (3 dígitos).|  
|SQL_SMALLINT|6 se assinada (um sinal e 5 dígitos) ou 5 se não for assinado (5 dígitos).|  
|SQL_INTEGER|11 se assinada (um sinal e 10 dígitos) ou 10 se não estiver assinado (10 dígitos).|  
|SQL_BIGINT|20 (um sinal e 19 dígitos, se assinado ou 20 dígitos, se não assinado).|  
|SQL_REAL|14 (um sinal, 7 dígitos, um ponto decimal, a letra *e*, um sinal e 2 dígitos).|  
|SQL_FLOAT SQL_DOUBLE|24 (um sinal, 15 dígitos, um ponto decimal, a letra *e*, um sinal e 3 dígitos).|  
|Todos os tipos binários [a]|O comprimento definido ou máximo (para tipos de variável) da coluna vezes 2. (Cada byte binário é representado por um número hexadecimal de 2 dígitos.)|  
|SQL_TYPE_DATE|10 (uma data no formato *aaaa-mm-dd*).|  
|SQL_TYPE_TIME|8 (uma hora no formato *hh: mm: SS*)<br /><br /> - ou -<br /><br /> 9 + *s* (uma hora no formato *hh: mm: SS*[. FFF...], em que *s* é a precisão de segundos fracionários).|  
|SQL_TYPE_TIMESTAMP|19 (para um carimbo de data/hora no formato *aaaa-mm-dd hh: mm: SS* )<br /><br /> - ou -<br /><br /> 20 + *s* (para um carimbo de data/hora no formato *aaaa-mm-dd hh: mm: SS*[. FFF...], em que *s* é a precisão de segundos fracionários).|  
|Todos os tipos de dados de intervalo|Consulte [comprimento do tipo de dados do intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md).|  
|SQL_GUID|36 (o número de caracteres no formato *aaaaaaaa-bbbb-cccc-dddd-EEEEEEEEEEEE*|  
  
 [a] se o driver não puder determinar o comprimento da coluna ou do parâmetro de tipos de variáveis, ele retornará SQL_NO_TOTAL.
