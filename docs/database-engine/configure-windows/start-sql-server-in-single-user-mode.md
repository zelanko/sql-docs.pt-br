---
title: Iniciar o SQL Server no modo de usuário único | Microsoft Docs
description: Saiba mais sobre o modo de usuário único no SQL Server. Veja quando ele é útil e como usar a opção de inicialização "-m" para iniciar uma instância do SQL Server nesse modo.
ms.custom: ''
ms.date: 09/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server, single-user mode
- single-user mode [SQL Server]
ms.assetid: 72eb4fc1-7af4-4ec6-9e02-11a69e02748e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 31b0075dfa6b3f4fa380e8b43054d0c98ebd8d81
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764003"
---
# <a name="start-sql-server-in-single-user-mode"></a>Iniciar o SQL Server no modo de usuário único
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Em determinadas circunstâncias, pode ser necessário iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único usando a **opção de inicialização -m.** Por exemplo, você pode querer mudar as opções de configuração de servidor ou recuperar um banco de dados mestre danificado ou outro banco de dados do sistema. As duas ações exigem iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único.  
  
 Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único permite que qualquer membro do grupo de Administradores locais do computador se conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um membro da função de servidor fixa sysadmin. Para obter mais informações, veja [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md).  
  
 Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único, observe o seguinte:  
  
-   Apenas um usuário pode se conectar ao servidor.  
  
-   O processo CHECKPOINT não é executado. Por padrão, ele é executado automaticamente na inicialização.  
  
> [!NOTE]  
>  Interrompa o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent antes de se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único. Caso contrário, o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usará a conexão, bloqueando-a.  
  
Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O Pesquisador de Objetos no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] pode falhar porque ele exige mais de uma conexão para algumas operações. Para gerenciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único, execute as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] conectando-se somente por meio do Editor de Consultas no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]ou use o [utilitário sqlcmd](../../tools/sqlcmd-utility.md).  
  
Ao usar a opção **-m** com **SQLCMD** ou [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], você pode limitar as conexões a um aplicativo cliente especificado. 

> [!NOTE]
> No Linux, **SQLCMD** deve estar em letras maiúsculas, como mostrado.

Por exemplo, **-m"SQLCMD"** limita as conexões a uma única conexão e essa conexão deve se identificar como o programa cliente **SQLCMD**. Use essa opção quando estiver iniciando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único e se um aplicativo cliente desconhecido estiver usando a única conexão disponível. Para se conectar por meio do Editor de Consultas no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use **-m"Microsoft SQL Server Management Studio - Query"** .  
  
> [!IMPORTANT]  
>  Não use essa opção como um recurso de segurança. O aplicativo cliente fornece o nome do aplicativo cliente e pode fornecer um nome falso como parte da cadeia de conexão.  
  
## <a name="note-for-clustered-installations"></a>Observação sobre instalações clusterizadas  
 Para instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente clusterizado, quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for iniciado em modo de usuário único, a dll de recurso de cluster usará a conexão disponível, bloqueando quaisquer outras conexões com o servidor. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver nesse estado e você tentar colocar o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent online, ele poderá realizar o failover do recurso SQL em outro nó, caso o recurso esteja configurado para afetar o grupo.  
  
 Para resolver o problema, use o procedimento a seguir:  
  
1.  Remova o parâmetro de inicialização -m das propriedades avançadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Coloque o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline.  
  
3.  No nó do proprietário atual desse grupo, emita o seguinte comando no prompt de comando:  
    net start MSSQLSERVER /m.  
  
4.  Verifique junto ao administrador do cluster ou no console de gerenciamento de cluster de failover se o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda está offline.  
  
5.  Conecte-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agora usando o seguinte comando e execute a operação necessária: SQLCMD -E -S\<servername>.  
  
6.  Quando a operação for concluída, feche o prompt de comando, e coloque o SQL e os outros recursos online novamente através do administrador do cluster.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar, parar ou pausar o serviço do SQL Server Agent](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
