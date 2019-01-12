---
title: Conectar-se ao dispositivo nós - Analytics Platform System | Microsoft Docs
description: Este artigo explica as várias maneiras para se conectar a cada nó em que o dispositivo do Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e8c61bebd6265d25e2c3fe0a14516e986f3ee414
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124435"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>Conectar-se a nós de dispositivo no Analytics Platform System
Este artigo explica as várias maneiras para se conectar a cada nó em que o dispositivo do Analytics Platform System.  
  
## <a name="connecting-with-hadoop"></a>Conectar-se com o Hadoop  
Antes de usar o Hadoop com o SQL Server PDW, peça ao administrador do dispositivo para instalar o Java Runtime Environment em SQL Server PDW. Para obter instruções, consulte [configurar a conectividade do PolyBase para dados externos &#40;Analytics Platform System&#41; ](configure-polybase-connectivity-to-external-data.md) no guia de operações de dispositivo.  
  
## <a name="ConnectingToIndividualNodes"></a>Conectar-se a nós de dispositivo  
Cada um de nós de dispositivo é acessada diretamente somente em cenários de uso específico e pelos tipos de usuário específico. A tabela a seguir lista cada nó de dispositivo e os cenários em que os usuários se conectarão diretamente para esse nó.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  
  
|||  
|-|-|  
|**Nó**|**Cenários de acesso**|  
|Nó de controle|Use um navegador da web para acessar o Console de administração, que é executado no nó de controle. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Todas as ferramentas e aplicativos cliente se conectar ao nó de controle, independentemente da conexão usando Ethernet ou InfiniBand.<br /><br />Para configurar uma conexão de Ethernet ao nó de controle, use o endereço de IP do Cluster de nó de controle e a porta **17001**. Por exemplo, "192.168.0.1,17001".<br /><br />Para configurar uma conexão de InfiniBand para o nó de controle, use  <strong>*appliance_domain*-SQLCTL01</strong> e a porta **17001**. Usando  <strong>*appliance_domain*-SQLCTL01</strong>, o servidor DNS de dispositivo se conectará o servidor à rede InfiniBand Active Directory. Para configurar seu servidor não seja de dispositivo para usá-la, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).<br /><br />O administrador do dispositivo se conecta ao nó de controle para executar operações de gerenciamento. Por exemplo, o administrador do dispositivo executa as seguintes operações do nó de controle:<br /><br />Configurar o Analytics Platform System com o **dwconfig.exe** ferramenta de configuração.|  
|Nó de computação|As conexões de nó são direcionadas ao nó de controle de computação. Os endereços IP de nós de computação nunca são inseridos em comandos do aplicativo como parâmetros.<br /><br />Para carregamento, backup, cópia de tabela remota e o Hadoop, o SQL Server PDW enviar ou receber dados diretamente em paralelo entre os nós de computação e os nós não seja de dispositivo ou servidores. Esses aplicativos se conectar com o SQL Server PDW conectando-se ao nó de controle e, em seguida, o nó de controle direciona o SQL Server PDW para estabelecer a comunicação entre os nós de computação e o servidor não seja de dispositivo.<br /><br />Por exemplo, essas operações de transferência de dados ocorram em paralelo com conexões diretas com os nós de computação:<br /><br />Carregamento do servidor de carregamento para o SQL Server PDW.<br /><br />Fazendo o backup de um banco de dados do SQL Server PDW para o servidor de backup.<br /><br />Restaurando um banco de dados do servidor de backup para o SQL Server PDW.<br /><br />Consultando dados do Hadoop do SQL Server PDW.<br /><br />Exportando dados do SQL Server PDW para uma tabela externa do Hadoop.<br /><br />Copiando uma tabela do SQL Server PDW para um banco de dados do SQL Server do SMP remoto.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>Conectando à Ethernet e redes InfiniBand  
Servidores remotos podem se conectar por meio da rede de InfiniBand de dispositivo ou por meio da rede Ethernet. Para questões de desempenho, carregando servidores, servidores de backup, servidores e receber dados via **CREATE REMOTE TABLE AS SELECT** instruções, normalmente, transferir dados pela rede InfiniBand appliance.  
  
Você pode configurar os servidores não seja de dispositivo para pertencer a seu próprio domínio ou grupo de trabalho do cliente e, em seguida, usar sua própria rede de cliente para se conectar aos servidores e a transferência de dados para eles. Além disso, os servidores não seja de dispositivo conectados ao dispositivo de InfiniBand tem a opção para transferir dados entre si pela rede InfiniBand do dispositivo. tenha cuidado com isso porque ele pode diminuir o desempenho do SQL Server PDW.  
  
Por exemplo, essa instrução adiciona credenciais de rede para a execução de backups por meio do InfiniBand para um servidor de backup que tenha um endereço IP InfiniBand 192.168.0.1. É o domínio de dispositivo *mypdw*, e a instrução é executada do servidor de backup. Antes de executar essa instrução, você precisará preencher seus próprios parâmetros.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
Por exemplo, um comando de carregamento será iniciado com o seguinte:  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
