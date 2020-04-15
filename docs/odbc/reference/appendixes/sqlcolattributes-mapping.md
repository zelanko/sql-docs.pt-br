---
title: Mapeamento de Atributos SQLCol | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c2c8386d6771141eaa0145a5d5964d70d6084d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305412"
---
# <a name="sqlcolattributes-mapping"></a>Mapeamento SQLColAttributes
Quando um aplicativo chama **SQLColAttributes** através de um driver ODBC *3.x,* a chamada para **SQLColAttributes** é mapeada para **SQLColAttribute** da seguinte forma:  
  
> [!NOTE]
>  O prefixo usado nos valores *fieldidentifier* no ODBC *3.x* foi alterado do usado no ODBC *2.x*. O novo prefixo é "SQL_DESC"; o prefixo antigo era "SQL_COLUMN".  
  
1.  Se o aplicativo for um aplicativo ODBC *2.x,* *fDescType* é SQL_COLUMN_TYPE e o tipo retornado é um tipo de HORA DE DATA CONCISa, o Gerenciador de driver mapeia os valores de devolução para códigos de data, hora e carimbo de data.  
  
2.  Se *o fDescType* for SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE ou SQL_COLUMN_COUNT, o Driver Manager chama **SQLColAttribute** no driver com o argumento *FieldIdentifier* mapeado para SQL_DESC_NAME, SQL_DESC_NULLABLE ou SQL_DESC_COUNT, conforme apropriado *.* Todos os outros valores de *fDescType* são repassados ao driver.  
  
 Um driver ODBC *3.x* deve suportar todos os *Identificadores* de Campo ODBC *3.x* listados para **SQLColAttribute**.  
  
 Um driver ODBC *3.x* deve suportar SQL_COLUMN_PRECISION e SQL_DESC_PRECISION, SQL_COLUMN_SCALE e SQL_DESC_SCALE, e SQL_COLUMN_LENGTH e SQL_DESC_LENGTH. Esses valores são diferentes porque precisão, escala e comprimento são definidos de forma diferente no ODBC *3.x* do que no ODBC *2.x*. Para obter mais informações, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no apêndice D: Tipos de dados.
