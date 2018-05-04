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
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf6df134c5a4ad54e574e42e57d7a68e10b4e077
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
