---
title: Funções preteridas de mapeamento | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b59d2604dd9d4b7c3166027c1917dea096b331d9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181311"
---
# <a name="mapping-deprecated-functions"></a>Funções preteridas de mapeamento
Esta seção descreve as funções como preteridas são mapeados por ODBC 3 *. x* Gerenciador de Driver para garantir a compatibilidade com versões anteriores do ODBC 3 *. x* drivers que são usados com o ODBC 2. *x* aplicativos. O Gerenciador de Driver realiza esse mapeamento independentemente da versão do aplicativo. Porque cada um dos ODBC 2. *x* funções na lista a seguir é mapeado para o ODBC 3 correspondente *. x* funcionar quando chamado em um ODBC 3 *. x* driver, o ODBC 3 *. x*driver não precisa implementar o ODBC 2. *x* funções.  
  
 O mapeamento da lista é disparado quando o driver é um ODBC 3 *. x* driver e o driver não oferece suporte para a função que está sendo mapeada.  
  
 A tabela a seguir lista as funcionalidades duplicadas tudo que foi introduzida no ODBC 3 *. x*.  
  
|ODBC 2. *x* função|3 de ODBC *. x* função|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** com um *opção* de SQL_DROP|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1], embora essa função não existe no ODBC 2 *. x*, trata-se nos padrões ISO e Open Group.  
  
 [2] Essa é uma função de ODBC 1.0.  
  
 Esta seção contém os tópicos a seguir.  
  
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
