---
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
ms.openlocfilehash: 8354fdabf6830780ec2d128492c86cc1edd582ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301623"
---
# <a name="cursor-characteristics-and-cursor-type"></a>Características do cursor e tipo de cursor
Um aplicativo pode especificar as características de um cursor em vez de especificar o tipo de cursor (somente para frente, estático, orientado por chave ou dinâmico). Para fazer isso, o aplicativo seleciona a rolability do cursor (definindo o atributo de declaração SQL_ATTR_CURSOR_SCROLLABLE) e a sensibilidade (definindo o atributo de declaração SQL_ATTR_CURSOR_SENSITIVITY) antes de abrir o cursor na alça da declaração. Em seguida, o motorista escolhe o tipo de cursor que fornece de forma mais eficiente as características solicitadas pelo aplicativo.  
  
 Sempre que um aplicativo define qualquer um dos atributos de declaração SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY ou SQL_ATTR_CURSOR_TYPE, o motorista faz qualquer alteração necessária para os outros atributos de declaração neste conjunto de quatro atributos para que seus valores permaneçam consistentes. Como resultado, quando o aplicativo especifica uma característica do cursor, o driver pode alterar o atributo que indica o tipo de cursor com base nesta seleção implícita; quando o aplicativo especifica um tipo, o driver pode alterar qualquer um dos outros atributos para ser consistente com as características do tipo selecionado. Para obter mais informações sobre esses atributos de declaração, consulte a descrição da função [SQLSetStmtAttr.](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
 Um aplicativo que define atributos de declaração para especificar tanto um tipo de cursor quanto características do cursor corre o risco de obter um cursor que não seja o método mais eficiente disponível naquele driver de atender aos requisitos do aplicativo.  
  
 A configuração implícita dos atributos de declaração é definida pelo driver, exceto que ela deve seguir essas regras:  
  
-   Os cursores somente para frente nunca são roláveis; ver a definição de SQL_ATTR_CURSOR_SCROLLABLE em [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   Os cursores insensíveis nunca são updatable (e, portanto, sua simultâneo é somente leitura); isso se baseia na definição de cursores insensíveis no padrão ISO SQL.  
  
 Consequentemente, a definição implícita dos atributos de declaração ocorre nos casos descritos na tabela a seguir.  
  
|O aplicativo define o atributo para|Outros atributos definidos implicitamente|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY para SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY para SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY para SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE, conforme definido pelo motorista. Ele nunca pode ser definido para SQL_INSENSITIVE, porque os cursores insensíveis são sempre lidos.|  
|SQL_ATTR_CURSOR_SCROLLABLE para SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE para SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo motorista. Nunca está definido para SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY para SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY para SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY para SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, conforme especificado pelo motorista. Nunca está definido para SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo motorista.|  
|SQL_ATTR_CURSOR_SENSITIVITY para SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, conforme especificado pelo motorista.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo motorista.|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE para SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY para SQL_SENSITIVE. (Mas só se SQL_ATTR_CONCURRENCY não for igual a SQL_CONCUR_READ_ONLY. Os cursores dinâmicos updatable são sempre sensíveis às mudanças que foram feitas em sua própria transação.)|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE a SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE para SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE (de acordo com critérios definidos pelo motorista, se SQL_ATTR_CONCURRENCY não for SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE para SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY para SQL_INSENSITIVE (se SQL_ATTR_CONCURRENCY for SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY para SQL_UNSPECIFIED ou SQL_SENSITIVE (se SQL_ATTR_CONCURRENCY não estiver SQL_CONCUR_READ_ONLY).|
