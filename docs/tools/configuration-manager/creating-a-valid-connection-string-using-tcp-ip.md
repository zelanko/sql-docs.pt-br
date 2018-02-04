---
title: "Criando uma cadeia de Conexão válida usando TCP/IP | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection strings [Database Engine]
- ports [SQL Server], connecting to
- TCP/IP [SQL Server], connection strings
- connection strings [Database Engine], TCP/IP
- aliases [SQL Server], TCP/IP
ms.assetid: ee5dbc2c-1fc6-42bd-bdf5-efa792557934
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 869aff413da127fac11244e8d2613696c963c323
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="creating-a-valid-connection-string-using-tcp-ip"></a>Criando uma cadeia de conexão válida usando TCP/IP
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
Para criar uma cadeia de conexão válida usando TCP/IP, deve você:  
  
-   Especificar um **Nome de Alias**.  
  
-   Para o **Servidor**, digite um nome do servidor ao qual você possa se conectar usando o utilitário **PING** ou um endereço IP ao qual possa se conectar usando o utilitário **PING** . Para uma instância nomeada, acrescente o nome da instância.  
  
-   Especificar **TCP/IP** para o **Protocolo**.  
  
-   Opcionalmente, digitar um número de porta para **Número da Porta**. O padrão é 1433, que é o número da porta da instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] em um servidor. Para se conectar a uma instância nomeada ou a uma instância padrão que não esteja escutando na porta 1433, é necessário fornecer o número da porta, ou iniciar o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter informações sobre como configurar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, consulte [Serviço do SQL Server Browser](../../tools/configuration-manager/sql-server-browser-service.md).  
  
 No momento da conexão, o componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client lê os valores de servidor, protocolo e porta no Registro para o nome de alias especificado e cria uma cadeia de conexão no formato `tcp:<servername>[\<instancename>],<port>` ou `tcp:<IPAddress>[\<instancename>],<port>`.  
  
> [!NOTE]  
>  O Firewall do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows fecha a porta 1433 por padrão. Porque [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se comunica pela porta 1433, reabra a porta se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para escutar conexões de cliente usando TCP/IP. Para obter informações sobre como configurar um firewall, consulte "Como configurar um firewall para acessar o SQL Server" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ou verifique a documentação do firewall.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dão suporte total ao protocolo IP versão 4 (IPv4) e versão 6 (IPv6). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager aceita IPv4 e IPv6 formatos para endereços IP. Para obter informações sobre IPv6, consulte "Conectando com o uso de IPv6" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="connecting-to-the-local-server"></a>Conectando-se ao servidor local  
 Ao conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no mesmo computador que o cliente, você pode usar `(local)` como o nome do servidor. Esse procedimento não é incentivado, pois leva a ambiguidade. No entanto, ele pode ser útil quando se sabe que o cliente está sendo executado no computador pretendido. Por exemplo, ao criar um aplicativo para usuários móveis desconectados, como uma força de vendas, em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será executado em computadores laptop e armazenará dados de projeto, um cliente conectado a `(local)` sempre se conectaria ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no laptop. A palavra `localhost` ou um ponto (**.**) pode ser usado no lugar de `(local)`.  
  
## <a name="verifying-your-connection-protocol"></a>Verificando seu protocolo de conexão  
 A consulta a seguir retorna o protocolo usado para a conexão atual.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Exemplos  
 Conectando pelo nome do servidor:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 Conectando-se a uma instância nomeada pelo nome do servidor:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>\<instancename>  
  
```  
  
 Conectando-se a uma porta especificada pelo nome do servidor:  
  
```  
Alias Name         <serveralias>  
Port No            <port>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 Conectando pelo endereço IP:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 Conectando-se a uma instância nomeada pelo endereço IP:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>\<instancename>  
  
```  
  
 Conectando-se a uma porta especificada pelo endereço IP:  
  
```  
Alias Name         <serveralias>  
Port No            <port number>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 Conectando-se ao computador local usando `(local)`:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             (local)  
  
```  
  
 Conectando-se ao computador local usando `localhost`:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost  
  
```  
  
 Conectando-se a uma instância nomeada no computador local `localhost`:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost\<instancename>  
  
```  
  
 Conectando-se ao computador local usando um ponto:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .  
  
```  
  
 Conectando-se a uma instância nomeada no computador local usando um ponto:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .\<instancename>  
  
```  
  
> [!NOTE]  
>  Para obter informações sobre como especificar o protocolo de rede como um parâmetro **sqlcmd** , consulte "Como fazer conexão com o Mecanismo de Banco de Dados usando sqlcmd.exe" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma cadeia de Conexão válida usando o protocolo de memória compartilhada](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [Criando uma cadeia de Conexão válida usando Pipes nomeados](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)   
 [Escolhendo um protocolo de rede](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
