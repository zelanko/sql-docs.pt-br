---
title: Funções de hora e data (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b47cd46b93878b6b394d302ff4493a6ec5bbd032
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Funções de hora e data (Driver ODBC do Visual FoxPro)
A tabela a seguir lista funções de data e hora ODBC com suporte do Visual FoxPro ODBC Driver; Quando a gramática do Visual FoxPro para a mesma função difere da sintaxe de ODBC, o Visual FoxPro equivalente é listado.  
  
|Gramática ODBC|Gramática do Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE *)*|DATA *)*|  
|CURTIME *)*|TEMPO *)*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH (*date_exp)*|DIA *)*|  
|HORA *(time_exp)*||  
|MINUTO *(time_exp)*||  
|MÊS *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|AGORA *)*|DATETIME *)*|  
|SEGUNDO *(time_exp)*|S *(time_exp)*|  
|SEMANA *(date_exp)*||  
|ANO *(date_exp)*||  
  
 Não há suporte para as seguintes funções de data e hora:  
  
 DAYOFYEAR *(date_exp)*  
  
 TRIMESTRE *(date_exp)*  
  
 TIMESTAMPADD *(intervalo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(intervalo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Sequências de Escape ODBC  
 O driver também oferece suporte a sequência de escape ODBC para dados de data e o carimbo de hora. A sintaxe da cláusula escape é o seguinte:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)—  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)—  
```  
  
 Nessa sintaxe, **d** indica que *valor* é uma data no *aaaa-mm-dd* formato e **ts** indica que *valor*  é um carimbo de hora a *aaaa-mm-dd hh*[.*f...*] formato. A sintaxe abreviada para dados de data e o carimbo de hora é o seguinte:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Por exemplo, cada uma das instruções a seguir atualiza a tabela ALLTYPES usando a sintaxe abreviada de data e o carimbo de hora em um comando de atualização do SQL com suporte:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre sequências de escape, consulte [sequências de Escape no ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) no *referência do programador de ODBC*.
