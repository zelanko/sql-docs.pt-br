---
description: Transferir dados em seu formato binário
title: Transferindo dados em sua forma binária | Microsoft Docs
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
ms.openlocfilehash: ec858729e76c1e360ec0933eca3a29ab17542f4f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386322"
---
# <a name="transferring-data-in-its-binary-form"></a>Transferir dados em seu formato binário
Um aplicativo pode transferir dados com segurança (no formulário interno usado por um DBMS especificado) entre duas fontes de dados que usam o mesmo DBMS e plataforma de hardware. Para uma determinada parte de dados, os tipos de dados SQL devem ser os mesmos nas fontes de dados de origem e de destino. O tipo de dados C é SQL_C_BINARY.  
  
 Quando o aplicativo chama **SQLFetch**, **SQLFetchScroll**ou **SQLGetData** para recuperar os dados da fonte de dados de origem, o driver recupera os dados da fonte de dados e transfere-os, sem conversão, para um local de armazenamento do tipo SQL_C_BINARY. Quando o aplicativo chama **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData ou SQLSetPos** para enviar os dados para a fonte de dados de destino, o driver recupera os dados do local de armazenamento e transfere-os, sem conversão, para a fonte de dados de destino.  
  
> [!NOTE]  
>  Os aplicativos que transferem quaisquer dados (exceto dados binários) dessa maneira não são interoperáveis entre DBMSs.  
  
 **SQLCopyDesc** pode ser usado para copiar associações de linha do DBMS de origem para associações de parâmetro no DBMS de destino.
