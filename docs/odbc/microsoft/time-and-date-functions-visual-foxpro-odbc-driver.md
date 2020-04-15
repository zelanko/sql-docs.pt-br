---
title: Funções de hora e data (driver Visual FoxPro ODBC) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303057"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Funções de data e hora (Driver ODBC do Visual FoxPro)
A tabela a seguir lista as funções de hora e data do ODBC suportadas pelo Driver Visual FoxPro ODBC; quando a gramática Visual FoxPro para a mesma função difere da sintaxe ODBC, o equivalente Visual FoxPro é listado.  
  
|Gramática ODBC|Gramática Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE *( )*|DATA *( )*|  
|CURTIME *( )*|TIME *( )*|  
|NOME DO DIA *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH *(date_exp)*|DIA *( )*|  
|HORA *(time_exp)*||  
|MINUTO *(time_exp)*||  
|MÊS *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|AGORA *( )*|HORA DE*DATA ( )*|  
|SEGUNDO *(time_exp)*|SEC *(time_exp)*|  
|SEMANA *(date_exp)*||  
|ANO *(date_exp)*||  
  
 As seguintes funções de hora e data não são suportadas:  
  
 DAYOFYEAR *(date_exp)*  
  
 TRIMESTRE *(DATE_EXP)*  
  
 TIMESTAMPADD *(intervalo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(intervalo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Sequências de escape do ODBC  
 O driver também suporta a seqüência de escape do ODBC para dados de data e carimbo de data. A sintaxe da cláusula de fuga é a seguinte:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 Nesta sintaxe, **d** indica que o *valor* é uma data no formato *yyyy-mm-dd* e **ts** indica que o *valor* é um carimbo de tempo no *yyyy-mm-dd hh:mm:ss*[.* f...*] Formato. A sintaxe taquigrafia para dados de data e carimbo de data é a seguinte:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Por exemplo, cada uma das seguintes instruções atualiza a tabela TODOS OS TIPOS usando a sintaxe taquigrafia data e carimbo de hora em um comando SQL UPDATE suportado:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre seqüências de fuga, consulte [Sequências de fuga no ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) na *referência do programador ODBC*.
