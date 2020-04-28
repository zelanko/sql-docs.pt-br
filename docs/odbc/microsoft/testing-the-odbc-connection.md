---
title: Testando a conexão ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8de19af2b50a58eef22ec074a308f86717278a48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303107"
---
# <a name="testing-the-odbc-connection"></a>Testar a conexão ODBC
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Ao solucionar problemas de acesso ODBC a servidores do Oracle 7. x e Oracle8 RDBMS, pode ser necessário verificar se os adaptadores de protocolo SQL * net e Oracle subjacentes estão instalados corretamente. Para fazer isso, use o utilitário fornecido pela Oracle Nettest. exe no diretório Orawin\Bin  
  
 O Nettest é um utilitário simples que tenta fazer logon no servidor selecionado usando apenas o software SQL * net instalado que faz parte do cliente Oracle. O utilitário solicitará um nome de logon, uma senha e uma cadeia de conexão TNS. Se o cliente Oracle estiver instalado corretamente, o utilitário simplesmente exibirá "ping bem-sucedido". Se o logon não tiver sido bem-sucedido, será necessário consultar um administrador de banco de dados.
