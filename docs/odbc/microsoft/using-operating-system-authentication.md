---
title: Usando a autenticação do sistema operacional | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 56f09a82c2e67ee74ce140f4742bfaf0bcce247f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088121"
---
# <a name="using-operating-system-authentication"></a>Usar a autenticação do sistema operacional
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Autenticação do sistema operacional Oracle depende do sistema operacional subjacente para controlar o acesso às contas de banco de dados. Os usuários não precisam inserir uma senha ao usar esse tipo de logon.  
  
 Para tirar proveito desse recurso, especifique "/" como a ID de usuário e não especificar uma senha ao se conectar usando qualquer um da conexão seguinte APIs: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md), or [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Usam o bancos de dados Oracle SQL * Net serviços de autenticação para autenticar os usuários que fizerem logon. Esse serviço funciona bem se os usuários são registrados no Oracle por meio de SQLPlus; No entanto, quando o usuário conectado é um serviço, como serviços de informações da Internet, a autenticação falhará. Essa é uma limitação conhecida de SQL\*autenticação Net e produz o seguinte erro: "[Microsoft] [driver ODBC para Oracle] [Oracle] ORA-12641: Serviço de TNS:Authentication falhou ao inicializar."  
  
 Você pode corrigir esse problema, editando o arquivo SQLNET. Geralmente, esse arquivo de configuração é armazenado no subdiretório Network\Admin do diretório base do Oracle. Adicione a seguinte linha ao SQLNET:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
