---
title: Mapeando funções preteridas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 307f0f54434fdcb4ebb19c38256a7a04f4a5c46d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990713"
---
# <a name="mapping-deprecated-functions"></a>Funções preteridas de mapeamento
Esta seção descreve como as funções preteridas são mapeadas pelo Gerenciador de driver ODBC *3. x* para garantir a compatibilidade com versões anteriores dos drivers ODBC *3. x* que são usados com aplicativos ODBC *2. x* . O Gerenciador de driver executa esse mapeamento independentemente da versão do aplicativo. Como cada uma das funções ODBC *2. x* na lista a seguir é mapeada para a função ODBC *3. x* correspondente quando chamada em um driver ODBC *3. x* , o driver ODBC *3. x* não precisa implementar as funções ODBC *2. x* .  
  
 O mapeamento na lista é disparado quando o driver é um driver ODBC *3. x* e o driver não oferece suporte à função que está sendo mapeada.  
  
 A tabela a seguir lista todas as funcionalidades duplicadas que foram introduzidas no ODBC *3. x*.  
  
|Função ODBC *2. x*|Função ODBC *3. x*|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** com uma *opção* de SQL_DROP|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] mesmo que essa função não exista no ODBC *2. x*, ela está no grupo aberto e nos padrões ISO.  
  
 [2] Esta é uma função ODBC 1,0.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Mapeamento SQLAllocConnect](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [Mapeamento SQLAllocEnv](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [Mapeamento SQLAllocStmt](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [Mapeamento SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [Mapeamento SQLColAttributes](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [Mapeamento SQLError](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [Mapeamento SQLFreeConnect](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [Mapeamento SQLFreeEnv](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [Mapeamento SQLFreeStmt](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [Mapeamento SQLGetConnectOption](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [Mapeamento SQLGetStmtOption](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [Mapeamento SQLInstallTranslator](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [Mapeamento SQLParamOptions](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [Mapeamento SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [Mapeamento SQLSetParam](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [Mapeamento SQLSetScrollOptions](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [Mapeamento SQLSetStmtOption](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [Mapeamento SQLTransact](../../../odbc/reference/appendixes/sqltransact-mapping.md)
