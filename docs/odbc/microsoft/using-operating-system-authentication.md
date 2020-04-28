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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6520202bdbc31baf1156531457cb70a98656e88
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292836"
---
# <a name="using-operating-system-authentication"></a>Usar a autenticação do sistema operacional
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A autenticação do sistema operacional Oracle depende do sistema operacional subjacente para controlar o acesso às contas do banco de dados. Os usuários não precisam inserir uma senha ao usar esse tipo de logon.  
  
 Para aproveitar esse recurso, especifique "/" como a ID de usuário e não especifique uma senha ao se conectar usando qualquer uma das seguintes APIs de conexão: [SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md), [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)ou [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Os bancos de dados Oracle usam os serviços de autenticação SQL * net para autenticar os usuários que fizeram logon. Esse serviço funciona bem se os usuários estiverem conectados ao Oracle por meio do sqlplus; no entanto, quando o usuário conectado for um serviço como Serviços de Informações da Internet, a autenticação falhará. Essa é uma limitação conhecida do SQL\*net Authentication e produz o seguinte erro: "[Microsoft] [ODBC driver for Oracle] [Oracle] ORA-12641: TNS: falha ao inicializar o serviço de autenticação."  
  
 Você pode corrigir esse problema editando o arquivo sqlnet. ora. Esse arquivo de configuração geralmente é armazenado no subdiretório Network\Admin do diretório base do Oracle. Adicione a seguinte linha a sqlnet. Ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
