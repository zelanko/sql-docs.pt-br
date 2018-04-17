---
title: Tipos de dados de campo do Visual FoxPro | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccb1adbe822aeb29bd34749333d59b6b67f6f5fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de dados de campo do Visual FoxPro
A tabela a seguir lista os valores para o *FieldType* argumento em ALTER TABLE e CREATE TABLE e indica se *nFieldWidth* e *nPrecision* argumentos são Necessário.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|Campo de caracteres de largura *n*|  
|D|-|-|Data|  
|F|N|d|Flutuante campo numérico da largura *n* com *d* casas decimais|  
|G|-|-|Geral|  
|I|-|-|Integer|  
|L|-|-|Logical|  
|M|-|-|Memorando|  
|N|N|d|Um campo numérico da largura *n* com *d* casas decimais|  
|T|-|-|DateTime|  
|S|-|-|Moeda|
