---
title: Transferência de dados em sua forma binária | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 53531ff4a3b2e1441fabf22ec7a3ce12b15540eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301408"
---
# <a name="transferring-data-in-its-binary-form"></a>Transferir dados em seu formato binário
Um aplicativo pode transferir dados com segurança (na forma interna usada por um DBMS especificado) entre duas fontes de dados que usam a mesma DBMS e a plataforma de hardware. Para um determinado dado, os tipos de dados SQL devem ser os mesmos nas fontes de dados de origem e de destino. O tipo de dados C é SQL_C_BINARY.  
  
 Quando o aplicativo chama **SQLFetch,** **SQLFetchScroll**ou **SQLGetData** para recuperar os dados da fonte de dados de origem, o driver recupera os dados da fonte de dados e os transfere, sem conversão, para um local de armazenamento do tipo SQL_C_BINARY. Quando o aplicativo chama **SQLBulkOperations,** **SQLExecute,** **SQLExecDirect,** **SQLPutData ou SQLSetPos** para enviar os dados para a fonte de dados alvo, o driver recupera os dados do local de armazenamento e os transfere, sem conversão, para a fonte de dados alvo.  
  
> [!NOTE]  
>  Os aplicativos que transferem quaisquer dados (exceto dados binários) desta forma não são interoperáveis entre os DBMSs.  
  
 **SQLCopyDesc** pode ser usado para copiar vinculações de linha do DBMS de origem para vinculações de parâmetros no DBMS de destino.
