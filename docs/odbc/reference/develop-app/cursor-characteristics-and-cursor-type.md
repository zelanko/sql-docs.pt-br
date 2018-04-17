---
title: Características de cursor e tipo de Cursor | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f54cc2f954a67d7a9cb3a4dfa6f6a006b652611d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-characteristics-and-cursor-type"></a>Características de cursor e tipo de Cursor
Um aplicativo pode especificar as características de um cursor em vez de especificar o tipo de cursor (somente avanço, estático, controlado por ou dinâmico). Para fazer isso, o aplicativo seleciona a rolagem do cursor (definindo o atributo de instrução SQL_ATTR_CURSOR_SCROLLABLE) e sensibilidade (definindo o atributo da instrução SQL_ATTR_CURSOR_SENSITIVITY) antes de abrir o cursor para a instrução identificador. O driver então escolhe o tipo de cursor que fornece com mais eficiência as características que o aplicativo solicitado.  
  
 Sempre que um aplicativo define qualquer um dos atributos de instrução SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY ou SQL_ATTR_CURSOR_TYPE, o driver faz qualquer alteração necessária para os outros atributos de instrução neste conjunto de quatro atributos para que seus valores permaneçam consistentes. Como resultado, quando o aplicativo especifica uma característica de cursor, o driver pode alterar o atributo que indica o tipo de cursor com base nessa seleção implícita; Quando o aplicativo especifica um tipo, o driver pode alterar qualquer um dos outros atributos para ser consistente com as características do tipo selecionado. Para obter mais informações sobre esses atributos de instrução, consulte o [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descrição da função.  
  
 Um aplicativo que define os atributos de instrução para especificar um tipo de cursor e características de cursor corre o risco de obter um cursor que não é o método mais eficiente disponível no driver de atender às necessidades do aplicativo.  
  
 A configuração implícita de atributos de instrução é definido pelo driver exceto que ele deve seguir estas regras:  
  
-   Cursores de somente avanço nunca são roláveis; Consulte a definição de SQL_ATTR_CURSOR_SCROLLABLE na [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   Cursores sem distinção nunca são atualizáveis (e, portanto, sua simultaneidade é somente leitura); Isso se baseia em sua definição de cursores sem distinção no ISO SQL padrão.  
  
 Consequentemente, a configuração implícita de atributos de instrução ocorre nos casos descritos na tabela a seguir.  
  
|Aplicativo define o atributo|Outros atributos são definidos implicitamente|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY para SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY como SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE, conforme definido pelo driver. Ele nunca pode ser definido como SQL_INSENSITIVE, como cursores sem distinção são sempre somente leitura.|  
|SQL_ATTR_CURSOR_SCROLLABLE como SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE como SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver. Ele nunca é definido como SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY como SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY para SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY como SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, conforme especificado pelo driver. Ele nunca é definido como SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver.|  
|SQL_ATTR_CURSOR_SENSITIVITY para SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY como SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, conforme especificado pelo driver.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver.|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE como SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY como SQL_SENSITIVE. (Mas somente se não for SQL_ATTR_CONCURRENCY como SQL_CONCUR_READ_ONLY. Cursores dinâmicos atualizáveis sempre são sensíveis às alterações feitas em suas próprias transações.)|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE como SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE como SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE (de acordo com driver critérios definidos, se SQL_ATTR_CONCURRENCY não for SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE como SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY como SQL_INSENSITIVE (se SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE (se SQL_ATTR_CONCURRENCY não estiver SQL_CONCUR_READ_ONLY).|
