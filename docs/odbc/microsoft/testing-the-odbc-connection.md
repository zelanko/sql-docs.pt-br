---
title: "Testando a Conexão ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cffb08b48128500b37c6f55e37a848be19c266a8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="testing-the-odbc-connection"></a>Testando a Conexão ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Ao solucionar problemas de acesso a ODBC para o Oracle 7. x e servidores Oracle8 RDBMS, talvez seja necessário verificar se o subjacente SQL * Net e adaptadores de protocolo do Oracle estão instalados corretamente. Para fazer isso, use o utilitário fornecido pela Oracle Nettest.exe no diretório Orawin\Bin.  
  
 Nettest é um utilitário simple que tenta fazer logon no servidor selecionado usando apenas o SQL instalado * Net software que faz parte do cliente Oracle. O utilitário solicitará um nome de logon, senha e TNS cadeia de conexão. Se o cliente Oracle está instalado corretamente, o utilitário simplesmente exibirá "Ping com êxito." Se o logon não foi bem-sucedida, você precisará consultar com um administrador de banco de dados.
