---
title: "Iniciar o SQL Server com configura&#231;&#227;o m&#237;nima | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "configuração mínima [SQL Server]"
  - "iniciando o SQL Server, configuração mínima"
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Iniciar o SQL Server com configura&#231;&#227;o m&#237;nima
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se você tiver problemas de configuração que impeçam o servidor de ser iniciado, você poderá iniciar uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a opção de inicialização de configuração mínima. Essa é a opção de inicialização **-f**. Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com configuração mínima, o servidor é colocado automaticamente em modo de usuário único.  
  
 Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de configuração mínimo, observe o seguinte:  
  
-   Apenas um usuário único pode fazer a conexão e o processo de CHECKPOINT não é executado.  
  
-   Acesso remoto e read-ahead são desabilitados.  
  
-   Procedimentos de inicialização armazenados não são executados.  
  
 Depois que o servidor tiver sido iniciado com a configuração mínima, altere o valor ou os valores da opção de servidor apropriada, interrompa e, em seguida, reinicie o servidor.  
  
> [!IMPORTANT]  
>  Use o utilitário **sqlcmd** e a DAC (conexão de administrador dedicada) para se conectar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você usar uma conexão típica, interrompa o SQL Server Agent antes de conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de configuração mínimo. Caso contrário, o SQL Server Agent usará a conexão, bloqueando-a.  
  
## Consulte também  
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)   
 [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  