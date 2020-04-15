---
title: Chamando SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46cfbb4e2e6b60f620cd7e38272bf9308ece91bc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306237"
---
# <a name="calling-sqlsetpos"></a>Chamar SQLSetPos
Em ODBC *2.x,* o ponteiro para a matriz de status da linha foi um argumento para **SQLExtendedFetch**. A matriz de status da linha foi atualizada mais tarde por uma chamada para **SQLSetPos**. Alguns drivers têm se apoiado no fato de que esta matriz não muda entre **SQLExtendedFetch** e **SQLSetPos**. Em ODBC *3.x,* o ponteiro para a matriz de status é um campo descritor e, portanto, o aplicativo pode facilmente alterá-lo para apontar para uma matriz diferente. Isso pode ser um problema quando um aplicativo ODBC *3.x* está trabalhando com um driver ODBC *2.x,* mas está chamando **SQLSetStmtAttr** para definir o ponteiro de status do array e está chamando **SQLFetchScroll** para buscar dados. O Gerenciador de driver mapeia-o como uma seqüência de chamadas para **SQLExtendedFetch**. No código a seguir, um erro normalmente seria levantado quando o Driver Manager mapeia a segunda chamada **SQLSetStmtAttr** ao trabalhar com um driver ODBC *2.x:*  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 O erro seria levantado se não houvesse como alterar o ponteiro de status da linha no ODBC *2.x* entre chamadas para **SQLExtendedFetch**. Em vez disso, o Driver Manager executa as seguintes etapas ao trabalhar com um driver ODBC *2.x:*  
  
1.  Inicializa um *fSetPosError* do Driver Manager interno para TRUE.  
  
2.  Quando um aplicativo chama **SQLFetchScroll,** o Gerenciador de driver define *fSetPosError* como FALSO.  
  
3.  Quando o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR, o Driver Manager define *fSetPosError* igual aTRUE.  
  
4.  Quando o aplicativo chama **SQLSetPos,** com *fSetPosError* igual a TRUE, o Gerenciador de driver aumenta SQL_ERROR com SQLSTATE HY011 (Atributo não pode ser definido agora) para indicar que o aplicativo tentou chamar **SQLSetPos** depois de alterar o ponteiro de status da linha, mas antes de chamar **SQLFetchScroll**.
