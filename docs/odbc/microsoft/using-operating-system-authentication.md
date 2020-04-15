---
title: Usando autenticação do sistema operacional | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292836"
---
# <a name="using-operating-system-authentication"></a>Usar a autenticação do sistema operacional
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A autenticação do sistema operacional Oracle conta com o sistema operacional subjacente para controlar o acesso às contas do banco de dados. Os usuários não precisam digitar uma senha ao usar esse tipo de login.  
  
 Para aproveitar esse recurso, especifique "/" como ID do usuário e não especifique uma senha ao se conectar usando qualquer uma das seguintes APIs de conexão: [SQLBrowseConnect,](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)ou [SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md).  
  
 Os bancos de dados Oracle usam serviços de autenticação SQL*Net para autenticar usuários conectados. Este serviço funciona bem se os usuários estiverem conectados ao Oracle através do SQLPlus; no entanto, quando o usuário logado é um serviço como o Internet Information Services, a autenticação falha. Esta é uma limitação\*conhecida da Autenticação SQL Net e produz o seguinte erro: "[Microsoft][Driver ODBC para Oracle][Oracle]ORA-12641: TNS:serviço de autenticação não foi inicializado."  
  
 Você pode corrigir esse problema editando o arquivo Sqlnet.ora. Esse arquivo de configuração geralmente é armazenado no subdiretório Network\Admin do diretório inicial oracle. Adicione a seguinte linha a Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
