---
title: SQLAllocConnect (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 70d48b12-def5-475c-b8e1-654a55fdfe0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2889ef8e5c6f3a0db4e133ddf0bdd51fda338b40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063291"
---
# <a name="sqlallocconnect-visual-foxpro-odbc-driver"></a>SQLAllocConnect (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível de núcleo  
  
 Aloca memória para um identificador de conexão *hdbc*, dentro do ambiente identificado pelo *henv*. O Gerenciador de Driver processa esta chamada e chama o driver **SQLAllocConnect** sempre que [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md), **SQLBrowseConnect**, ou [SQLDriverConnect ](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) é chamado.  
  
 Para obter mais informações, consulte [SQLAllocConnect](../../odbc/reference/syntax/sqlallocconnect-function.md) na *referência do programador de ODBC*.
