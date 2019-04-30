---
title: Mapeamento SQLColAttributes | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7a1508d10431ba9975c44a2002faa4e5b913312
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199417"
---
# <a name="sqlcolattributes-mapping"></a>Mapeamento SQLColAttributes
Quando um aplicativo chama **SQLColAttributes** por meio de um ODBC 3 *. x* driver, a chamada para **SQLColAttributes** é mapeado para **SQLColAttribute** da seguinte maneira:  
  
> [!NOTE]
>  O prefixo usado na *FieldIdentifier* valores em ODBC 3 *. x* tiver sido alterada de que o usado em ODBC 2. *x*. O novo prefixo é "SQL_DESC"; o prefixo antigo era "SQL_COLUMN".  
  
1.  Se o aplicativo for um ODBC 2. *x* aplicativo, *fDescType* é SQL_COLUMN_TYPE, e o tipo retornado é um tipo DATETIME conciso, os mapas de Gerenciador de Driver, o retorno de valores para códigos de data, hora e carimbo de hora.  
  
2.  Se *fDescType* é SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE ou SQL_COLUMN_COUNT, as chamadas de Gerenciador de Driver **SQLColAttribute** no driver com o *FieldIdentifier* argumento mapeado para SQL_DESC_NAME, SQL_DESC_NULLABLE ou SQL_DESC_COUNT, conforme apropriado *.* Todos os outros valores de *fDescType* são passados para o driver.  
  
 Um ODBC 3 *. x* driver deve oferecer suporte a todos os 3 do ODBC *. x* *FieldIdentifiers* listados para **SQLColAttribute**.  
  
 Um ODBC 3 *. x* driver deve oferecer suporte a SQL_COLUMN_PRECISION e SQL_DESC_PRECISION, SQL_COLUMN_SCALE e SQL_DESC_SCALE, SQL_COLUMN_LENGTH e SQL_DESC_LENGTH. Esses valores são diferentes, como precisão, escala e comprimento são definidas forma diferente em ODBC 3 *. x* que era no ODBC 2. *x*. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: Tipos de dados.
