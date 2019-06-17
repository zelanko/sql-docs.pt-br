---
title: Testando a Conexão ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- testing connections [ODBC]
- ODBC driver for Oracle [ODBC], testing connections
ms.assetid: 5e671665-2aba-49a7-8871-70784d8b3cc9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 543ab436ac7dca5e0d5965220cd90a798afb5ccf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633171"
---
# <a name="testing-the-odbc-connection"></a>Testar a conexão ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Ao solucionar problemas de acesso a ODBC para Oracle 7. x e servidores Oracle8 RDBMS, talvez seja necessário verificar se o SQL subjacente * Net e adaptadores de protocolo do Oracle estão instalados corretamente. Para fazer isso, use o utilitário fornecido pelo Oracle Nettest.exe no diretório Orawin\Bin.  
  
 Nettest é um utilitário simples que tenta fazer logon no servidor selecionado usando apenas o SQL instalado * Net de software que faz parte do cliente da Oracle. O utilitário solicitará um nome de logon, senha e TNS cadeia de conexão. Se o cliente Oracle está instalado corretamente, o utilitário simplesmente exibirá "Ping com êxito." Se o logon não foi bem-sucedida, você precisará consultar com um administrador de banco de dados.
