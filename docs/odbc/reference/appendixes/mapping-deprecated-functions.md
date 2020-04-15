---
title: Mapeamento de Funções Depreciadas | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a4e89cd9281520e70ec5fb289c6050e77ec6194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299876"
---
# <a name="mapping-deprecated-functions"></a>Funções preteridas de mapeamento
Esta seção descreve como as funções depreciadas são mapeadas pelo Gerenciador de Driver ODBC *3.x* para garantir a compatibilidade retrógrada dos drivers ODBC *3.x* que são usados com aplicativos ODBC *2.x.* O Driver Manager realiza esse mapeamento independentemente da versão do aplicativo. Como cada uma das funções ODBC *2.x* na lista a seguir é mapeada para a função ODBC *3.x* correspondente quando chamada em um driver ODBC *3.x,* o driver ODBC *3.x* não precisa implementar as funções ODBC *2.x.*  
  
 O mapeamento na lista é acionado quando o driver é um driver ODBC *3.x* e o motorista não suporta a função que está sendo mapeada.  
  
 A tabela a seguir lista todas as funcionalidades duplicadas introduzidas no ODBC *3.x*.  
  
|Função ODBC *2.x*|Função ODBC *3.x*|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributea**|**SQLColAttribute**|  
|**Sqlerror**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** com *opção* de SQL_DROP|**SQLFreeHandle**|  
|**Opção SQLGetConnect**|**SQLGetConnectAttr**|  
|**Opção SQLGetStmt**|**SQLGetStmtAttr**|  
|**Opções de SQLParam**|**SQLSetStmtAttr**|  
|**Sqlsetconnectoption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOpção**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] Embora essa função não existisse no ODBC *2.x,* ela está nos padrões Open Group e ISO.  
  
 [2] Esta é uma função ODBC 1.0.  
  
 Esta seção contém os seguintes tópicos.  
  
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
