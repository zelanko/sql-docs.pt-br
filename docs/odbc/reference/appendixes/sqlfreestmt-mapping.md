---
title: Mapeamento SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d187db4d40132385b9ae4564fddbf89987e3e97
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302007"
---
# <a name="sqlfreestmt-mapping"></a>Mapeamento SQLFreeStmt
Quando um aplicativo chama **sqlFreeStmt** com um argumento *de opção* de SQL_DROP através de um driver ODBC *3.x,* a chamada para  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 é mapeado para  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 com o argumento *Handle* definido para o valor em *hstmt*.
