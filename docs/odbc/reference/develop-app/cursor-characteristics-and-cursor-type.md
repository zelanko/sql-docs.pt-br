---
description: Características do cursor e tipo de cursor
title: Características do cursor e tipo de cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10ec9c7fc42ad20ce0a5a6d70ef4a2a692afbec3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429418"
---
# <a name="cursor-characteristics-and-cursor-type"></a>Características do cursor e tipo de cursor
Um aplicativo pode especificar as características de um cursor em vez de especificar o tipo de cursor (somente avanço, estático, controlado por conjunto de chaves ou dinâmico). Para fazer isso, o aplicativo seleciona a rolabilidade do cursor (definindo o atributo SQL_ATTR_CURSOR_SCROLLABLE Statement) e a sensibilidade (definindo o atributo SQL_ATTR_CURSOR_SENSITIVITY Statement) antes de abrir o cursor no identificador da instrução. Em seguida, o driver escolhe o tipo de cursor que fornece com mais eficiência as características solicitadas pelo aplicativo.  
  
 Sempre que um aplicativo define qualquer um dos atributos de instrução SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY ou SQL_ATTR_CURSOR_TYPE, o driver faz qualquer alteração necessária aos outros atributos de instrução nesse conjunto de quatro atributos para que seus valores permaneçam consistentes. Como resultado, quando o aplicativo especifica uma característica de cursor, o driver pode alterar o atributo que indica o tipo de cursor com base nessa seleção implícita; Quando o aplicativo especifica um tipo, o driver pode alterar qualquer um dos outros atributos para que seja consistente com as características do tipo selecionado. Para obter mais informações sobre esses atributos de instrução, consulte a descrição da função [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) .  
  
 Um aplicativo que define atributos de instrução para especificar um tipo de cursor e características de cursor executa o risco de obter um cursor que não é o método mais eficiente disponível nesse driver de atender aos requisitos do aplicativo.  
  
 A configuração implícita de atributos de instrução é definida pelo driver, exceto pelo fato de que ele deve seguir estas regras:  
  
-   Cursores de somente avanço nunca são roláveis; consulte a definição de SQL_ATTR_CURSOR_SCROLLABLE em [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   Cursores insensíveis nunca são atualizáveis (e, portanto, sua simultaneidade é somente leitura); Isso se baseia em sua definição de cursores insensíveis no padrão ISO SQL.  
  
 Consequentemente, a configuração implícita de atributos de instrução ocorre nos casos descritos na tabela a seguir.  
  
|Atributo de conjuntos de aplicativos para|Outros atributos definidos implicitamente|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY para SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE, conforme definido pelo driver. Ele nunca pode ser definido como SQL_INSENSITIVE, porque cursores insensíveis são sempre somente leitura.|  
|SQL_ATTR_CURSOR_SCROLLABLE SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver. Ele nunca é definido como SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, conforme especificado pelo driver. Ele nunca é definido como SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver.|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, conforme especificado pelo driver.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY SQL_SENSITIVE. (Mas somente se SQL_ATTR_CONCURRENCY não for igual a SQL_CONCUR_READ_ONLY. Cursores dinâmicos atualizáveis são sempre sensíveis a alterações que foram feitas em sua própria transação.)|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE (de acordo com os critérios definidos pelo driver, se SQL_ATTR_CONCURRENCY não for SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_INSENSITIVE (se SQL_ATTR_CONCURRENCY for SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE (se SQL_ATTR_CONCURRENCY não for SQL_CONCUR_READ_ONLY).|
