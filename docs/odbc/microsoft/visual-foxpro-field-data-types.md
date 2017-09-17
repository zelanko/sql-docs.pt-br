---
title: Tipos de dados de campo do Visual FoxPro | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c1ae849d91962cb7d11ca8bac755665217fe1a2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="visual-foxpro-field-data-types"></a>Tipos de dados de campo do Visual FoxPro
A tabela a seguir lista os valores para o *FieldType* argumento em ALTER TABLE e CREATE TABLE e indica se *nFieldWidth* e *nPrecision* argumentos são Necessário.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|Campo de caracteres de largura*n*|  
|D|-|-|Data|  
|F|N|d|Flutuante campo numérico da largura * n * com *d* casas decimais|  
|G|-|-|Geral|  
|I|-|-|Integer|  
|L|-|-|Logical|  
|M|-|-|Memorando|  
|N|N|d|Um campo numérico da largura * n * com *d* casas decimais|  
|T|-|-|DateTime|  
|S|-|-|Moeda|
