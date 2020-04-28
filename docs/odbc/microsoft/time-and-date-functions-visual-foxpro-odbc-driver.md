---
title: Funções de data e hora (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86260f8e7245bed15122d4dbfc4649131674e17f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303057"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Funções de data e hora (Driver ODBC do Visual FoxPro)
A tabela a seguir lista as funções de data e hora ODBC com suporte no driver ODBC do Visual FoxPro; Quando a gramática do Visual FoxPro para a mesma função difere da sintaxe ODBC, o equivalente do Visual FoxPro é listado.  
  
|Gramática ODBC|Gramática do Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE *()*|Data *()*|  
|CURTIME *()*|HORA *()*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH (*date_exp)*|DIA *()*|  
|HORA *(time_exp)*||  
|MINUTO *(time_exp)*||  
|MÊS *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|NOW *()*|DATA e hora *()*|  
|SEGUNDO *(time_exp)*|S *(time_exp)*|  
|SEMANA *(date_exp)*||  
|ANO *(date_exp)*||  
  
 As seguintes funções de data e hora não têm suporte:  
  
 DAYOFYEAR *(date_exp)*  
  
 TRIMESTRE *(date_exp)*  
  
 TIMESTAMPADD *(intervalo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(intervalo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Sequências de escape do ODBC  
 O driver também dá suporte à sequência de escape ODBC para dados de data e timestamp. A sintaxe da cláusula escape é a seguinte:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 Nessa sintaxe, **d** indica que o *valor* é uma data no formato *aaaa-mm-dd* e **TS** indica que o *valor* é um carimbo de data/hora em *aaaa-mm-dd hh: mm: SS*[.* f...*] ao. A sintaxe abreviada para dados de data e timestamp é a seguinte:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Por exemplo, cada uma das instruções a seguir atualiza a tabela de meus tipos usando a sintaxe de data e timestamp abreviada em um comando SQL UPDATE com suporte:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre sequências de escape, consulte [sequências de escape no ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) na *referência do programador de ODBC*.
