---
title: Transferência de dados em seu formato binário | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2897f882dc9dcd78ee8b919de01126d6be510c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070021"
---
# <a name="transferring-data-in-its-binary-form"></a>Transferir dados em seu formato binário
Um aplicativo com segurança pode transferir dados (no formato interno usado por um DBMS especificado) entre duas fontes de dados que usam a mesma DBMS e a plataforma de hardware. Para uma determinada parte dos dados, os tipos de dados do SQL devem ser o mesmo nas fontes de dados de origem e destino. O tipo de dados C é SQL_C_BINARY.  
  
 Quando o aplicativo chama **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData** para recuperar os dados da fonte de dados de origem, o driver recupera os dados dos dados fonte e os transfere, sem conversão, em um local de armazenamento do tipo SQL_C_BINARY. Quando o aplicativo chama **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData ou SQLSetPos** para enviar os dados para a fonte de dados de destino, o driver recupera os dados do local de armazenamento e os transfere, sem conversão, à fonte de dados de destino.  
  
> [!NOTE]  
>  Aplicativos que transferir nenhum dado (exceto dados binários) dessa maneira não são interoperáveis entre DBMSs.  
  
 **SQLCopyDesc** pode ser usado para copiar associações de linha de DBMS de origem para associações de parâmetro no DBMS de destino.
