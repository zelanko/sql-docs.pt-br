---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7d4a14a6afc2d716e85e687cbae1a202a596d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241247"
---
# <a name="display-size"></a>Tamanho de exibição
O tamanho da exibição de uma coluna é o número máximo de caracteres necessário para exibir dados em formato de caractere. A tabela a seguir define o tamanho de exibição para cada tipo de dados SQL ODBC.  
  
|Identificador de tipo SQL|Tamanho de exibição|  
|-------------------------|------------------|  
|Todos os tipos de caracteres [a]|Definido (para tipos fixos) ou máximo (para tipos de variáveis) número de caracteres necessários para exibir os dados em formato de caractere.|  
|SQL_DECIMAL SQL_NUMERIC|A precisão da coluna mais 2 (um sinal, *precisão* dígitos e um ponto decimal). Por exemplo, o tamanho da exibição de uma coluna definida como NUMERIC(10,3) é 12.|  
|SQL_BIT|1 (1 dígito).|  
|SQL_TINYINT|4 se assinado (um sinal e 3 dígitos) ou 3, se não tiver sinal (3 dígitos).|  
|SQL_SMALLINT|6 se assinado (um sinal e 5 dígitos) ou 5 se não tiver sinal (5 dígitos).|  
|SQL_INTEGER|11 se assinado (um sinal e 10 dígitos) ou 10, se não tiver sinal (10 dígitos).|  
|SQL_BIGINT|20 (um sinal e 19 dígitos se assinado ou 20 dígitos se não tiver sinal).|  
|SQL_REAL|14 (um sinal, 7 dígitos, um ponto decimal, a letra *eletrônico*, um sinal e 2 dígitos).|  
|SQL_FLOAT SQL_DOUBLE|24 (um sinal, 15 dígitos, um ponto decimal, a letra *eletrônico*, um sinal e 3 dígitos).|  
|Todos os tipos binários [a]|Definido ou máximo (para tipos de variáveis) 2 de tempo do comprimento da coluna. (Cada byte binário é representado por um número hexadecimal de 2 dígitos.)|  
|SQL_TYPE_DATE|10 (uma data no formato *aaaa-mm-dd*).|  
|SQL_TYPE_TIME|8 (uma hora no formato *hh*)<br /><br /> - ou -<br /><br /> 9 + *s* (uma hora no formato *hh*[.... fff], onde *s* é a precisão de frações de segundo).|  
|SQL_TYPE_TIMESTAMP|19 (para um carimbo de hora a *aaaa-mm-dd hh* formato)<br /><br /> - ou -<br /><br /> 20 + *s* (para um carimbo de hora a *aaaa-mm-dd hh*formato [.... fff], onde *s* é a precisão de frações de segundo).|  
|Todos os tipos de dados de intervalo|Ver [comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md).|  
|SQL_GUID|36 (o número de caracteres a *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* formato|  
  
 [a] se o driver não puder determinar o comprimento de coluna ou parâmetro de tipos de variáveis, ele retornará SQL_NO_TOTAL.
