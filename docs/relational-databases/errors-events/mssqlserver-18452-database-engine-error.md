---
title: MSSQLSERVER_18452 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 18456 (Database Engine error)
- 18452 (Database Engine error)
ms.assetid: 21da332c-e81d-4dee-a9d2-95598911b3be
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7e08452accd39507cc3124ff4a1dc22a073c01dd
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver18452"></a>MSSQLSERVER_18452
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|18452|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LOGON_INVALID_CONNECT|  
|Texto da mensagem|Falha no logon do usuário '%.*ls'. O logon é um logon do SQL Server e não pode ser usado com a Autenticação do Windows.%.\*ls|  
  
## <a name="explanation"></a>Explicação  
O usuário tentou fazer logon com credenciais que não podem ser validadas. Causas possíveis:  
  
-   O logon pode ser um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas o servidor aceita somente a Autenticação do Windows (Segurança Integrada).  
  
-   Você está tentando se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas o logon usado não existe no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O logon pode usar a Autenticação do Windows (Segurança Integrada), mas é uma entidade não reconhecida do Windows. Uma entidade não reconhecida do Windows significa que o logon não pode ser verificado pelo Windows. Talvez isso ocorra porque o logon do Windows é de um domínio não confiável.  
  
Problemas semelhantes podem causar o erro menos específico 18456.  
  
## <a name="user-action"></a>Ação do usuário  
Se você estiver tentando se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado no Modo de Autenticação Mista.  
  
Se você estiver tentando se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existe.  
  
Se você estiver tentando se conectar usando a Autenticação do Windows, verifique se está devidamente conectado no domínio correto.  
  

