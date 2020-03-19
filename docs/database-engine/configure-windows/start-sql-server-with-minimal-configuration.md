---
title: Iniciar o SQL Server com a configuração mínima | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0c919ad9202c99c7b010b6aee9c921e76784eb24
ms.sourcegitcommit: 7008c7fe451a20d6610e40bb8f61dece86c0f17e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79027960"
---
# <a name="start-sql-server-with-minimal-configuration"></a>Iniciar o SQL Server com configuração mínima
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Se você tiver problemas de configuração que impeçam o servidor de ser iniciado, inicie uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a opção de inicialização de configuração mínima. Essa é a opção de inicialização **-f**. Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com configuração mínima, o servidor é colocado automaticamente em modo de usuário único.  
  
 Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de configuração mínimo, observe o seguinte:  
  
-   Apenas um único usuário pode se conectar e o processo `CHECKPOINT` não é executado.  
  
-   Acesso remoto e read-ahead são desabilitados.  
  
-   Procedimentos de inicialização armazenados não são executados.  

-   `tempdb` é configurado no menor tamanho possível.

-   A Auditoria será desabilitada, mas a DDL de Auditoria ainda poderá ser emitida. Na prática, **-m** deverá ser suficiente para a maioria dos casos que exige a reconfiguração da Auditoria do SQL Server. Para obter mais detalhes sobre a segurança na configuração de Auditoria, confira [Auditoria no SQL Server](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/dd392015(v=sql.100)#security).
  
 Depois que o servidor tiver sido iniciado com a configuração mínima, altere o valor ou os valores da opção de servidor apropriada, interrompa e, em seguida, reinicie o servidor.  
  
> [!IMPORTANT]  
>  Use o utilitário **sqlcmd** e a DAC (conexão de administrador dedicada) para se conectar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você usar uma conexão típica, interrompa o SQL Server Agent antes de conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de configuração mínimo. Caso contrário, o SQL Server Agent usará a conexão, bloqueando-a.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
