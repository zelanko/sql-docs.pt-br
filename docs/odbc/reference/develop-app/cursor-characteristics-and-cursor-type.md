---
title: Características do cursor e tipo de Cursor | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8803e7827102f564be63454b0387df938064d84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002049"
---
# <a name="cursor-characteristics-and-cursor-type"></a>Características do cursor e tipo de cursor
Um aplicativo pode especificar as características de um cursor em vez de especificar o tipo de cursor (somente de avanço, estático, controlado por conjunto de chaves ou dinâmico). Para fazer isso, o aplicativo seleciona a rolagem do cursor (definindo o atributo de instrução SQL_ATTR_CURSOR_SCROLLABLE) e sensibilidade (definindo o atributo da instrução SQL_ATTR_CURSOR_SENSITIVITY) antes de abrir o cursor na instrução identificador. O driver, em seguida, escolhe o tipo de cursor que fornece com mais eficiência as características que o aplicativo solicitado.  
  
 Sempre que um aplicativo define todos os atributos de instrução SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY ou SQL_ATTR_CURSOR_TYPE, o driver faz qualquer alteração necessária para os outros atributos de instrução neste conjunto de quatro atributos para que seus valores permanecem consistentes. Como resultado, quando o aplicativo especifica uma característica de cursor, o driver pode alterar o atributo que indica o tipo de cursor com base nessa seleção implícita; Quando o aplicativo especifica um tipo, o driver pode alterar qualquer um dos outros atributos para ser consistente com as características do tipo selecionado. Para obter mais informações sobre esses atributos de instrução, consulte o [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descrição da função.  
  
 Um aplicativo que define os atributos de instrução para especificar um tipo de cursor e características de cursor corre o risco de obter um cursor que não é o método mais eficiente disponível no driver de atender às necessidades do aplicativo.  
  
 A configuração implícita de atributos de instrução é definido pelo driver, exceto que ele deve seguir estas regras:  
  
-   Cursores de somente avanço nunca são roláveis; Consulte a definição de SQL_ATTR_CURSOR_SCROLLABLE na [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   Cursores sem distinção nunca são atualizáveis (e, portanto, seu simultaneidade é somente leitura); Isso se baseia em sua definição de cursores sem distinção no ISO SQL padrão.  
  
 Consequentemente, a configuração implícita de atributos de instrução ocorre nos casos descritos na tabela a seguir.  
  
|Aplicativo define o atributo para|Outros atributos definidos implicitamente|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY para SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY como SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY e SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE, conforme definido pelo driver. Ele nunca pode ser definido como SQL_INSENSITIVE, como cursores sem distinção sempre são somente leitura.|  
|SQL_ATTR_CURSOR_SCROLLABLE como SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE como SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver. Ele nunca é definido como SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY como SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY para SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY como SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, conforme especificado pelo driver. Ele nunca é definido como SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver.|  
|SQL_ATTR_CURSOR_SENSITIVITY para SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_READ_ONLY, SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES, conforme especificado pelo driver.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN ou SQL_CURSOR_DYNAMIC, conforme especificado pelo driver.|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE como SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY como SQL_SENSITIVE. (Mas apenas se SQL_ATTR_CONCURRENCY não é igual a SQL_CONCUR_READ_ONLY. Cursores dinâmicos atualizáveis sempre são sensíveis às alterações que foram feitas em suas próprias transações.)|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE como SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE como SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE (de acordo com driver critérios definidos, se SQL_ATTR_CONCURRENCY não for SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE para SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE como SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY como SQL_INSENSITIVE (se SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED ou SQL_SENSITIVE (se SQL_ATTR_CONCURRENCY não for SQL_CONCUR_READ_ONLY).|
