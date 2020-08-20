---
description: Chamar SQLSetPos
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
ms.openlocfilehash: ecb1708b6d5fe9877ab647b11488131645e56690
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494707"
---
# <a name="calling-sqlsetpos"></a>Chamar SQLSetPos
No ODBC *2. x*, o ponteiro para a matriz de status de linha era um argumento para **SQLExtendedFetch**. A matriz de status de linha foi atualizada posteriormente por uma chamada para **SQLSetPos**. Alguns drivers se basearam no fato de que essa matriz não é alterada entre **SQLExtendedFetch** e **SQLSetPos**. No ODBC *3. x*, o ponteiro para a matriz de status é um campo de descritor e, portanto, o aplicativo pode alterá-lo facilmente para apontar para uma matriz diferente. Isso pode ser um problema quando um aplicativo ODBC *3. x* está trabalhando com um driver ODBC *2. x* , mas está chamando **SQLSetStmtAttr** para definir o ponteiro de status da matriz e está chamando **SQLFetchScroll** para buscar dados. O Gerenciador de driver o mapeia como uma sequência de chamadas para **SQLExtendedFetch**. No código a seguir, um erro normalmente seria gerado quando o Gerenciador de driver mapeia a segunda chamada **SQLSetStmtAttr** ao trabalhar com um driver ODBC *2. x* :  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 O erro seria gerado se não houvesse nenhuma maneira de alterar o ponteiro de status de linha no ODBC *2. x* entre as chamadas para **SQLExtendedFetch**. Em vez disso, o Gerenciador de driver executa as seguintes etapas ao trabalhar com um driver ODBC *2. x* :  
  
1.  Inicializa um sinalizador do Gerenciador de driver interno *fSetPosError* como true.  
  
2.  Quando um aplicativo chama **SQLFetchScroll**, o Gerenciador de driver define *fSetPosError* como false.  
  
3.  Quando o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de driver define *FSETPOSERROR* igual a true.  
  
4.  Quando o aplicativo chama **SQLSetPos**, com *FSETPOSERROR* igual a true, o gerenciador de driver gera SQL_ERROR com SQLSTATE hy011 (o atributo não pode ser definido agora) para indicar que o aplicativo tentou chamar **SQLSetPos** depois de alterar o ponteiro de status de linha, mas antes de chamar **SQLFetchScroll**.
