---
title: Mapeamento de SQLColAttributes | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d21d1a9a9565ad2c0accbebb716d0b24f18f854d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-mapping"></a>Mapeamento de SQLColAttributes
Quando um aplicativo chama **SQLColAttributes** por meio de um ODBC 3*. x* driver, a chamada para **SQLColAttributes** é mapeado para **SQLColAttribute** da seguinte maneira:  
  
> [!NOTE]  
>  O prefixo usado em *FieldIdentifier* valores em ODBC 3*. x* foi alterado do que o usado em ODBC 2.* x*. O novo prefixo é "SQL_DESC"; o prefixo antigo foi "SQL_COLUMN".  
  
1.  Se o aplicativo for um ODBC 2. *x* aplicativo, *fDescType* é SQL_COLUMN_TYPE e o tipo retornado é do tipo DATETIME conciso, os mapas de Gerenciador de Driver, o retorno de valores para códigos de data, hora e carimbo de hora.  
  
2.  Se *fDescType* é SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE ou SQL_COLUMN_COUNT, as chamadas de Gerenciador de Driver **SQLColAttribute** no driver com o *FieldIdentifier* argumento mapeado para SQL_DESC_NAME, SQL_DESC_NULLABLE ou SQL_DESC_COUNT, conforme apropriado*.* Todos os outros valores de *fDescType* são passados para o driver.  
  
 Um ODBC 3*. x* driver deve oferecer suporte a todos os o ODBC 3*. x* *FieldIdentifiers* listados para **SQLColAttribute**.  
  
 Um ODBC 3*. x* driver deve oferecer suporte a SQL_COLUMN_PRECISION e SQL_DESC_PRECISION, SQL_COLUMN_SCALE e SQL_DESC_SCALE e SQL_COLUMN_LENGTH e SQL_DESC_LENGTH. Esses valores são diferentes porque a precisão, escala e comprimento são definidos de forma diferente em ODBC 3*. x* que estavam no ODBC 2.* x*. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: os tipos de dados.
