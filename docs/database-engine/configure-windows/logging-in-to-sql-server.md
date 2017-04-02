---
title: "Fazendo o logon no SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server, fazendo logon"
  - "serviços [SQL Server], fazendo logon"
  - "Cadeia de conexão TCP"
  - "conectando-se ao Mecanismo de Banco de Dados"
  - "logons [SQL Server], sobre como fazer logon"
  - "cadeia de conexão de pipe nomeado"
  - "logons [SQL Server]"
  - "cadeia de conexão de memória compartilhada"
  - "fazendo logon [SQL Server]"
  - "logons [SQL Server]"
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Fazendo o logon no SQL Server
  Você pode fazer o logon para uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando qualquer uma das ferramentas de administração gráficas ou em um prompt de comando.  
  
 Quando você faz o logon em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando uma ferramenta de administração gráfica, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é solicitado que você forneça o nome do servidor, um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e uma senha, se necessário. Se você fizer logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a Autenticação do Windows, não precisará fornecer um logon do SQL Server cada vez que acessar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em vez, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa sua conta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para fazer o logon automaticamente. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver em execução na autenticação de modo misto ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Modo de Autenticação do Windows) e você optar por fazer o logon usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], será necessário fornecer um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e uma senha. Quando possível, use a Autenticação do Windows.  
  
> [!NOTE]  
>  Se você selecionou um agrupamento que diferencia maiúsculas e minúsculas ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também diferenciará maiúsculas e minúsculas.  
  
## Formate para especificar o nome de SQL Server  
 Ao se conectar a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], especifique o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for a instância padrão (uma instância não nomeada), especifique o nome do computador onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, ou o endereço IP do computador. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for uma instância nomeada (como SQLEXPRESS), especifique o nome do computador onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado, ou o endereço IP do computador. Adicione uma barra e o nome da instância.  
  
 Os exemplos a seguir conectam a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executada em um computador denominado APPHOST. Ao especificar uma instância nomeada, os exemplos usam um nome de instância SQLEXPRESS.  
  
 **Exemplos:**  
  
|Tipo da instância|Entrada do nome de servidor|  
|----------------------|-------------------------------|  
|Conexão para uma instância padrão que usa o protocolo padrão. (Esta é a entrada indicada para uma instância padrão.)|APPHOST|  
|Conexão a uma instância nomeada que usa o protocolo padrão. (Esta é a entrada indicada para uma instância nomeada.)|APPHOST\SQLEXPRESS|  
|Conexão para uma instância padrão no mesmo computador que usa um período para indicar que a instância está sendo executada no computador local.|.|  
|Conexão a uma instância nomeada no mesmo computador usando um período para indicar que a instância está sendo executada no computador local.|.\SQLEXPRESS|  
|Conexão a uma instância padrão no mesmo computador usando localhost para indicar que a instância está sendo executada no computador local.|localhost|  
|Conexão a uma instância nomeada no mesmo computador usando localhost para indicar que a instância está sendo executada no computador local.|localhost\SQLEXPRESS|  
|Conexão a uma instância padrão no mesmo computador usando (local) para indicar que a instância está sendo executada no computador local.|(local)|  
|Conexão a uma instância nomeada no mesmo computador usando (local) para indicar que a instância está sendo executada no computador local.|(local)\SQLEXPRESS|  
|Conexão a uma instância padrão no mesmo computador que força uma conexão de memória compartilhada.|lpc:APPHOST|  
|Conexão a uma instância nomeada no mesmo computador que força uma conexão de memória compartilhada.|lpc:APPHOST\SQLEXPRESS|  
|Conexão a uma instância padrão que escuta no endereço TCP 192.168.17.28 usando um endereço IP.|192.168.17.28|  
|Conexão a uma instância nomeada que escuta no endereço TCP 192.168.17.28 usando um endereço IP.|192.168.17.28\SQLEXPRESS|  
|Conexão a uma instância padrão que não está escutando na porta TCP padrão, especificando a porta que está sendo usada, neste caso, 2828. (Isto não será necessário se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver escutando na porta padrão (1433).)|APPHOST,2828|  
|Conexão para uma instância nomeada em uma porta TCP designada, neste caso, 2828. (Isto costuma ser necessário quando o serviço de Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está sendo executado no computador host.)|APPHOST,2828|  
|Conexão a uma instância padrão que não está escutando na porta TCP padrão, especificando o endereço IP e a porta TCP que está sendo usada, neste caso, 2828.|192.168.17.28,2828|  
|Conexão a uma instância nomeada, especificando o endereço IP e a porta TCP que está sendo usada, neste caso, 2828.|192.168.17.28,2828|  
|Conectando à instância padrão através de nome, forçando uma conexão TCP.|tcp:APPHOST|  
|Conectando à instância nomeada através de nome, forçando uma conexão TCP.|tcp:APPHOST\SQLEXPRESS|  
|Conectando a uma instância padrão especificando um nome de pipe nomeado.|\\\APPHOST\pipe\unit\app|  
|Conectando a uma instância nomeada especificando um nome de pipe nomeado.|\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query|  
|Conectando à instância padrão através de nome, forçando uma conexão de pipes nomeados.|np:APPHOST|  
|Conectando à instância nomeada através de nome, forçando uma conexão de pipes nomeados.|np:APPHOST\SQLEXPRESS|  
  
## Verificando o protocolo de conexão  
 Quando conectado ao [!INCLUDE[ssDE](../../includes/ssde-md.md)], a consulta a seguir retornará o protocolo usado para a conexão atual, junto com o método de autenticação (NTLM ou Kerberos), e indicará se a conexão é criptografada.  
  
```tsql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## Tarefas relacionadas  
 [Fazer logon em uma instância do SQL Server &#40;Prompt de Comando&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 Os recursos a seguir podem ajudá-lo a solucionar um problema de conexão.  
  
-   [Como solucionar problemas na conexão ao Mecanismo de Banco de Dados do SQL Server](http://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [Etapas para solucionar problemas de conectividade do SQL](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
## Conteúdo relacionado  
 [Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [Usar o utilitário sqlcmd](../../relational-databases/scripting/use-the-sqlcmd-utility.md)  
  
 [criando um logon](../../t-sql/creating-a-login.md)  
  
  