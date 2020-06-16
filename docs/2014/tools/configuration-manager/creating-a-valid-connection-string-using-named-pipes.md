---
title: Criando uma cadeia de conexão válida usando pipes nomeados | Microsoft Docs
description: Saiba como criar uma cadeia de conexão válida ao usar o protocolo de pipes nomeados para se conectar a uma instância do SQL Server. Exibir exemplos de nomes de pipe válidos.
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine], named pipes
- pipes [SQL Server]
- pipes [SQL Server], connecting to
- aliases [SQL Server], named pipes
- Named Pipes [SQL Server], connection strings
ms.assetid: 90930ff2-143b-4651-8ae3-297103600e4f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 65fcebc3bbe12061e699106fb23eed15a5498414
ms.sourcegitcommit: c8e45e0fdab8ea2ae1c7e709346354576b18ca1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84716703"
---
# <a name="creating-a-valid-connection-string-using-named-pipes"></a>Criando uma cadeia de conexão válida usando pipes nomeados
  A menos que seja alterado pelo usuário, quando a instância padrão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta no protocolo de pipes nomeados, ela é usada `\\.\pipe\sql\query` como o nome do pipe. O ponto indica que o computador é local, `pipe` indica que a conexão é um pipe nomeado e `sql\query` é o nome do pipe. Para conectar ao pipe padrão, o alias deve ter `\\<computer_name>\pipe\sql\query` como nome do pipe. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver sido configurado para escutar em um pipe diferente, o nome do pipe deverá usar esse pipe. Por exemplo, se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver usando `\\.\pipe\unit\app` como o pipe, o alias deverá usar `\\<computer_name>\pipe\unit\app` como o nome do pipe.  
  
 Para criar um nome de pipe válido, deve você:  
  
-   Especificar um **Nome de Alias**.  
  
-   Selecione **pipes nomeados** como o **protocolo**.  
  
-   Insira o **nome do pipe**. Como alternativa, você pode deixar o **nome do pipe** em branco e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager concluirá o nome do pipe apropriado depois de especificar o **protocolo** e o **servidor**  
  
-   Especifique um **servidor**. Para uma instância nomeada, você pode fornecer um nome de servidor e um nome de instância.  
  
 No momento da conexão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente cliente nativo lê os valores de servidor, protocolo e nome de pipe do registro para o nome de alias especificado e cria um nome de pipe no formato `np:\\<computer_name>\pipe\<pipename>` ou `np:\\<IPAddress>\pipe\<pipename>` . Para uma instância nomeada, o nome do pipe padrão é `\\<computer_name>\pipe\MSSQL$<instance_name>\sql\query` .  
  
> [!NOTE]  
>  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] Firewall do Windows fecha a porta 445 por padrão. Como o [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se comunica pela porta 445, você deverá reabri-la se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurado para escutar conexões de entrada usando pipes nomeados. Para obter informações sobre como configurar um firewall, consulte "Como configurar um firewall para acessar o SQL Server" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ou verifique a documentação do firewall.  
  
## <a name="connecting-to-the-local-server"></a>Conectando-se ao servidor local  
 Ao conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no mesmo computador que o cliente, você pode usar `(local)` como o nome do servidor. O uso de `(local)` não é incentivado, pois leva a ambiguidade; no entanto, ele pode ser útil quando se sabe que o cliente está sendo executado no computador pretendido. Por exemplo, ao criar um aplicativo para usuários móveis desconectados, como uma força de vendas, em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será executado em computadores laptop e armazenará dados de projeto, um cliente conectado a (local) sempre se conectaria ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no laptop. A palavra `localhost` ou um ponto (.) pode ser usado no lugar de `(local)`.  
  
## <a name="verifying-your-connection-protocol"></a>Verificando seu protocolo de conexão  
 A consulta a seguir retornará o protocolo usado para a conexão atual.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Exemplos  
 Conectando-se ao pipe padrão pelo nome do servidor:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Conectando-se ao pipe padrão pelo Endereço IP:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <leave blank>  
Protocol           Named Pipes  
Server             <IPAddress>  
  
```  
  
 Conectando-se ao pipe não padrão pelo nome do servidor:  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\unit\app  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Conectando-se a uma instância nomeada pelo nome do servidor:  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\MSSQL$<instancename>\SQL\query  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Conectando-se ao computador local usando `localhost`:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             localhost  
  
```  
  
 Conectando-se ao computador local usando um ponto:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <left blank>  
Protocol           Named Pipes  
Server             .  
  
```  
  
> [!NOTE]  
>  Para especificar o protocolo de rede como um parâmetro **sqlcmd** , consulte "como conectar-se ao Mecanismo de Banco de Dados usando sqlcmd.exe" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [Criando uma cadeia de conexão válida usando IP TCP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Escolhendo um protocolo de rede](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
