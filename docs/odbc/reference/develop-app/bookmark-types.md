---
title: Tipos de marcadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- variable-length bookmarks [ODBC]
- bookmarks [ODBC]
- fixed-length bookmarks [ODBC]
ms.assetid: cb2e7443-0260-4d1a-930f-0154db447979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d0297cd9dc57e9f30945a9248b235ae469da3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306327"
---
# <a name="bookmark-types"></a>Tipos de indicador
Todos os marcadores no ODBC *3.x* são marcadores de comprimento variável. Isso permite que uma chave primária ou um índice único associado a uma tabela seja usado como marcador. O marcador também pode ser um valor de 32 bits, como foi usado no ODBC *2.x*. Para especificar que um marcador é usado com um cursor, um aplicativo ODBC *3.x* define o atributo de declaração SQL_ATTR_USE_BOOKMARK a SQL_UB_VARIABLE. Um marcador de comprimento variável é usado automaticamente.  
  
 Um aplicativo pode chamar **SQLColAttribute** com o argumento *FieldIdentifier* definido para SQL_DESC_OCTET_LENGTH para obter o comprimento do marcador. Como um marcador de comprimento variável pode ser um valor longo, um aplicativo não deve se vincular à coluna 0, a menos que use o marcador para muitas das linhas no conjunto de linhas.  
  
 Marcadores de comprimento fixo são suportados apenas para compatibilidade retrógrada. Se um aplicativo ODBC *2.x* que trabalha com um driver ODBC *3.x* chamar **sqlsetstmtOption** para definir SQL_USE_BOOKMARKS para SQL_UB_ON, ele será mapeado no Driver Manager para SQL_UB_VARIABLE. Um marcador de comprimento variável é usado, mesmo que apenas 32 bits dele sejam preenchidos. Se um driver suportar marcadores de comprimento fixo, ele suportará marcadores de comprimento variável. Se um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* chamar **o SQLSetStmtAttr** para definir SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE, ele será mapeado no Driver Manager para SQL_UB_ON e um marcador de comprimento fixo de 32 bits é usado. O atributo de declaração SQL_ATTR_FETCH_BOOKMARK_PTR deve então apontar para um marcador de 32 bits. Se os marcadores usados forem maiores que 32 bits, como quando as teclas primárias são usadas como marcadores, o cursor deve mapear os valores reais para valores de 32 bits. Poderia, por exemplo, construir uma tabela hash deles. Quando um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* liga um marcador, o comprimento do buffer deve ser 4.
