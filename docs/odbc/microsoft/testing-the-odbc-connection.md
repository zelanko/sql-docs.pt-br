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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8de19af2b50a58eef22ec074a308f86717278a48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303107"
---
# <a name="testing-the-odbc-connection"></a>Testar a conexão ODBC
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Ao solucionar problemas do acesso do ODBC aos servidores Oracle 7.x e Oracle8 RDBMS, talvez seja necessário verificar se os adaptadores de protocolo SQL*Net e Oracle subjacentes estão corretamente instalados. Para fazer isso, use o utilitário nettest.exe fornecido pela Oracle no diretório Orawin\Bin.  
  
 Nettest é um utilitário simples que tenta fazer logon no servidor selecionado usando apenas o software SQL*Net instalado que faz parte do cliente Oracle. O utilitário pedirá um nome de login, senha e seqüência de conexão TNS. Se o cliente Oracle estiver instalado corretamente, o utilitário simplesmente exibirá "Ping Successful". Se o login não foi bem sucedido, você precisará consultar um administrador de banco de dados.
