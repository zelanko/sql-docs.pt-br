---
title: Conecte-se ao dispositivo nós - Analytics Platform System | Microsoft Docs
description: Este artigo explica as várias maneiras de se conectar a cada nó no dispositivo de sistema de plataforma de análise.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2d7d634023c5fc3d0a6f522b5f60933ce3b96272
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539536"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>Conecte-se a nós de dispositivo no sistema de plataforma de análise
Este artigo explica as várias maneiras de se conectar a cada nó no dispositivo de sistema de plataforma de análise.  
  
## <a name="connecting-with-hadoop"></a>Conectando com Hadoop  
Antes de usar Hadoop com o SQL Server PDW, peça ao administrador do dispositivo para instalar o Java Runtime Environment para SQL Server PDW. Para obter instruções, consulte [configurar conectividade do PolyBase para dados externos &#40;Analytics Platform System&#41; ](configure-polybase-connectivity-to-external-data.md) no guia de operações do dispositivo.  
  
## <a name="ConnectingToIndividualNodes"></a>Conectando-se a nós de dispositivo  
Cada um de nós de dispositivo é acessada diretamente somente em cenários de uso específico e por tipos de usuário específico. A tabela a seguir lista cada nó de dispositivo e os cenários em que os usuários se conectarão diretamente para esse nó.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  
  
|||  
|-|-|  
|**Nó**|**Cenários de acesso**|  
|Nó de controle|Use um navegador da web para acessar o Console de administração, que é executado no nó de controle. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Todas as ferramentas e aplicativos cliente conectar-se ao nó de controle, independentemente se a conexão está usando Ethernet ou InfiniBand.<br /><br />Para configurar uma conexão Ethernet ao nó de controle, use o endereço de IP do Cluster do nó de controle e a porta **17001**. Por exemplo, "192.168.0.1,17001".<br /><br />Para configurar uma conexão InfiniBand ao nó de controle, use ***appliance_domain *-SQLCTL01** e porta **17001**. Usando ***appliance_domain *-SQLCTL01**, o servidor DNS do dispositivo se conectará seu servidor à rede InfiniBand ativa. Para configurar o servidor não seja de aplicação para usá-la, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).<br /><br />O administrador do dispositivo se conecta ao nó de controle para executar operações de gerenciamento. Por exemplo, o administrador do aplicativo executa as seguintes operações do nó de controle:<br /><br />Configurar o Analytics Platform System com o **dwconfig.exe** ferramenta de configuração.|  
|Nó de computação|Conexões de nó são direcionadas ao nó de controle de computação. Os endereços IP de nós de computação nunca são inseridos em comandos do aplicativo como parâmetros.<br /><br />Para carregamento, backup, cópia de tabela remota e o Hadoop, o SQL Server PDW enviar ou receber dados diretamente em paralelo entre os nós de computação e o dispositivo não nós ou servidores. Esses aplicativos se conectar com o SQL Server PDW conectando-se ao nó de controle e, em seguida, o nó de controle direciona PDW do SQL Server para estabelecer a comunicação entre os nós de computação e o servidor não seja de aplicação.<br /><br />Por exemplo, essas operações de transferência de dados ocorrem em paralelo com conexões diretas com os nós de computação:<br /><br />Carregamento do servidor de carregamento para o SQL Server PDW.<br /><br />Fazendo backup de um banco de dados do SQL Server PDW ao servidor de backup.<br /><br />Restaurando um banco de dados do servidor de backup para o SQL Server PDW.<br /><br />Consultar dados de Hadoop do SQL Server PDW.<br /><br />Exportando dados do SQL Server PDW para uma tabela externa do Hadoop.<br /><br />Copiar uma tabela do SQL Server PDW para um banco de dados remoto do SMP SQL Server.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>Conectando-se a Ethernet e redes InfiniBand  
Servidores remotos podem se conectar por meio da rede de InfiniBand de dispositivo ou por meio da rede de Ethernet. Por motivos de desempenho, o carregamento de servidores, fazer backup de servidores e servidores que recebem dados por meio de **CREATE REMOTE TABLE AS SELECT** instruções, geralmente transferir dados pela rede InfiniBand appliance.  
  
Você pode configurar servidores de dispositivo não pertencentes a seu próprio domínio ou grupo de trabalho do cliente e, em seguida, usar sua própria rede de cliente para se conectar a esses servidores e transferir dados para eles. Além disso, servidores de dispositivo não conectados ao dispositivo InfiniBand tem a opção para transferir dados entre si pela rede InfiniBand appliance; tenha cuidado com isso porque pode reduzir o desempenho do SQL Server PDW.  
  
Por exemplo, essa instrução adiciona credenciais de rede para executar backups através de InfiniBand para um servidor de backup que tenha um endereço IP InfiniBand 192.168.0.1. O domínio de aplicativo é *mypdw*, e a instrução é executada a partir do servidor de backup. Antes de executar essa instrução, você precisa preencher seus próprios parâmetros.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
Por exemplo, um comando de carregamento será iniciado com o seguinte:  
  
```  
dwloader –S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
