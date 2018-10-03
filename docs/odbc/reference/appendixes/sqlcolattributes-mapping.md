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
ms.openlocfilehash: d0332e38a96d17589d9aa75bfe2a3c918dcc78d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639644"
---
# <a name="sqlcolattributes-mapping"></a>Mapeamento SQLColAttributes
Quando um aplicativo chama **SQLColAttributes** por meio de um ODBC 3 *. x* driver, a chamada para **SQLColAttributes** é mapeado para **SQLColAttribute** da seguinte maneira:  
  
> [!NOTE]  
>  O prefixo usado na *FieldIdentifier* valores em ODBC 3 *. x* tiver sido alterada de que o usado em ODBC 2. *x*. O novo prefixo é "SQL_DESC"; o prefixo antigo era "SQL_COLUMN".  
  
1.  Se o aplicativo for um ODBC 2. *x* aplicativo, *fDescType* é SQL_COLUMN_TYPE, e o tipo retornado é um tipo DATETIME conciso, os mapas de Gerenciador de Driver, o retorno de valores para códigos de data, hora e carimbo de hora.  
  
2.  Se *fDescType* é SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE ou SQL_COLUMN_COUNT, as chamadas de Gerenciador de Driver **SQLColAttribute** no driver com o *FieldIdentifier* argumento mapeado para SQL_DESC_NAME, SQL_DESC_NULLABLE ou SQL_DESC_COUNT, conforme apropriado *.* Todos os outros valores de *fDescType* são passados para o driver.  
  
 Um ODBC 3 *. x* driver deve oferecer suporte a todos os 3 do ODBC *. x* *FieldIdentifiers* listados para **SQLColAttribute**.  
  
 Um ODBC 3 *. x* driver deve oferecer suporte a SQL_COLUMN_PRECISION e SQL_DESC_PRECISION, SQL_COLUMN_SCALE e SQL_DESC_SCALE, SQL_COLUMN_LENGTH e SQL_DESC_LENGTH. Esses valores são diferentes, como precisão, escala e comprimento são definidas forma diferente em ODBC 3 *. x* que era no ODBC 2. *x*. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) apêndice d: tipos de dados.
