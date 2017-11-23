---
title: Exibir tamanho | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9facf94a89033e4bc765439d45b897a96ba7bf88
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="display-size"></a>Tamanho de exibição
O tamanho de exibição de uma coluna é o número máximo de caracteres necessários para exibir dados em formato de caractere. A tabela a seguir define o tamanho de exibição para cada tipo de dados SQL ODBC.  
  
|Identificador de tipo SQL|Tamanho de exibição|  
|-------------------------|------------------|  
|Todos os tipos de caracteres [a]|Definido (para tipos fixos) ou máximo (para tipos de variável) número de caracteres necessários para exibir os dados em formato de caractere.|  
|SQL_DECIMAL SQL_NUMERIC|A precisão da coluna mais 2 (um sinal, *precisão* dígitos e um ponto decimal). Por exemplo, o tamanho de exibição de uma coluna definida como NUMERIC(10,3) é 12.|  
|SQL_BIT|1 (1 dígito).|  
|SQL_TINYINT|4 se conectado (um sinal e 3 dígitos) ou 3 se não assinado (3 dígitos).|  
|SQL_SMALLINT|6 se assinado (um sinal e 5 dígitos) ou 5 se não assinado (5 dígitos).|  
|SQL_INTEGER|11 se assinado (um sinal e 10 dígitos) ou 10 se não assinado (10 dígitos).|  
|SQL_BIGINT|20 (um sinal e 19 se conectado ou 20 dígitos se não assinado).|  
|SQL_REAL|14 (um sinal, 7 dígitos, um ponto decimal, a letra *E*, um sinal e 2 dígitos).|  
|SQL_FLOAT SQL_DOUBLE|24 (um sinal, 15 dígitos, um ponto decimal, a letra *E*, um sinal e 3 dígitos).|  
|Todos os tipos binários [a]|Definido ou máximo (para tipos de variáveis) da coluna tempo 2. (Cada byte binário é representado por um número hexadecimal de 2 dígitos.)|  
|SQL_TYPE_DATE|10 (uma data no formato *aaaa-mm-dd*).|  
|SQL_TYPE_TIME|8 (uma hora no formato *hh*)<br /><br /> - ou -<br /><br /> 9 + *s* (uma hora no formato *hh*[.... fff], onde *s* é a precisão de frações de segundo).|  
|SQL_TYPE_TIMESTAMP|19 (para um carimbo de hora a *aaaa-mm-dd hh* formato)<br /><br /> - ou -<br /><br /> 20 + *s* (para um carimbo de hora a *aaaa-mm-dd hh*formato [.... fff], onde *s* é a precisão de frações de segundo).|  
|Todos os tipos de dados de intervalo|Consulte [comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md).|  
|SQL_GUID|36 (o número de caracteres a *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* formato|  
  
 [a] se o driver não pode determinar o comprimento de coluna ou parâmetro de tipos de variáveis, ela retornará SQL_NO_TOTAL.
