---
title: "Usando a autenticação do sistema operacional | Microsoft Docs"
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
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffcdcf10f0114b9c695031626f707843527050b5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="using-operating-system-authentication"></a>Usando a autenticação do sistema operacional
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Autenticação de sistema operacional do Oracle se baseia no sistema operacional subjacente para controlar o acesso às contas do banco de dados. Os usuários não precisam inserir uma senha ao usar esse tipo de logon.  
  
 Para tirar proveito desse recurso, especifique "/" como a ID de usuário e não especificar uma senha ao conectar-se usando qualquer um da conexão seguinte APIs: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md), ou [ SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Usam o bancos de dados Oracle SQL * Net serviços de autenticação para autenticar os usuários que fizerem logon. Esse serviço funciona bem se os usuários estão conectados no Oracle por meio de SQLPlus; No entanto, quando o usuário conectado é um serviço, como serviços de informações da Internet, a autenticação falhará. Essa é uma limitação conhecida do SQL\*autenticação de rede e produz o seguinte erro: "[Microsoft] [ODBC driver for Oracle] [Oracle] ORA-12641: TNS:authentication service falhou ao inicializar."  
  
 Você pode corrigir esse problema, editando o arquivo SQLNET. Geralmente, esse arquivo de configuração é armazenado no subdiretório Network\Admin do diretório base do Oracle. Adicione a seguinte linha ao SQLNET:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
