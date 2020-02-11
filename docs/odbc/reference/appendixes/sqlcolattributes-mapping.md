---
title: Mapeamento de SQLColAttributes | Microsoft Docs
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
ms.openlocfilehash: 08abd0128a6fa2a478af0e9dc9c292ff973ace79
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064494"
---
# <a name="sqlcolattributes-mapping"></a>Mapeamento SQLColAttributes
Quando um aplicativo chama **SQLColAttributes** por meio de um driver ODBC *3. x* , a chamada para **SQLColAttributes** é mapeada para **SQLColAttribute** da seguinte maneira:  
  
> [!NOTE]
>  O prefixo usado nos valores de *FieldIdentifier* no ODBC *3. x* foi alterado de usado no ODBC *2. x*. O novo prefixo é "SQL_DESC"; o prefixo antigo era "SQL_COLUMN".  
  
1.  Se o aplicativo for um aplicativo ODBC *2. x* , *fDescType* for SQL_COLUMN_TYPE e o tipo RETORNADO for um tipo DateTime conciso, o Gerenciador de driver mapeará os valores de retorno para os códigos de data, hora e timestamp.  
  
2.  Se *fDescType* for SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE ou SQL_COLUMN_COUNT, o Gerenciador de driver chamará **SQLColAttribute** no driver com o argumento *FieldIdentifier* mapeado para SQL_DESC_NAME, SQL_DESC_NULLABLE ou SQL_DESC_COUNT, conforme apropriado *.* Todos os outros valores de *fDescType* são passados para o driver.  
  
 Um driver ODBC *3. x* deve dar suporte a todos os *FieldIdentifiers* ODBC *3. x* listados para **SQLColAttribute**.  
  
 Um driver ODBC *3. x* deve dar suporte a SQL_COLUMN_PRECISION e SQL_DESC_PRECISION, SQL_COLUMN_SCALE e SQL_DESC_SCALE e SQL_COLUMN_LENGTH e SQL_DESC_LENGTH. Esses valores são diferentes porque precisão, escala e comprimento são definidos de forma diferente no ODBC *3. x* do que estavam no ODBC *2. x*. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.
