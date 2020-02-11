---
title: Iniciar o SQL Server com a configuração mínima | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cf7065d064e322e45fb95a38aed514b2acfc714a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62756217"
---
# <a name="start-sql-server-with-minimal-configuration"></a>Iniciar o SQL Server com configuração mínima
  Se houver problemas de configuração que impeçam a inicialização do servidor, você poderá iniciar uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância do usando a opção de inicialização de configuração mínima. Essa é a opção de inicialização **-f**. Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com configuração mínima, o servidor é colocado automaticamente em modo de usuário único.  
  
 Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de configuração mínimo, observe o seguinte:  
  
-   Apenas um usuário único pode fazer a conexão e o processo de CHECKPOINT não é executado.  
  
-   Acesso remoto e read-ahead são desabilitados.  
  
-   Procedimentos de inicialização armazenados não são executados.  
  
 Depois que o servidor tiver sido iniciado com a configuração mínima, altere o valor ou os valores da opção de servidor apropriada, interrompa e, em seguida, reinicie o servidor.  
  
> [!IMPORTANT]  
>  Use o utilitário **sqlcmd** e a DAC (conexão de administrador dedicada) para se conectar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você usar uma conexão típica, interrompa o SQL Server Agent antes de conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de configuração mínimo. Caso contrário, o SQL Server Agent usará a conexão, bloqueando-a.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar ou pausar o serviço SQL Server Agent](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)   
 [Conexão de diagnóstico para administradores de banco de dados](diagnostic-connection-for-database-administrators.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](database-engine-service-startup-options.md)  
  
  
