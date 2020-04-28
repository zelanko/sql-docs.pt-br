---
title: Conectar-se a nós de dispositivo
description: Este artigo explica as várias maneiras de se conectar a cada nó do dispositivo de sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e1182d174e3281fda944c0b6490b114d4b6f2244
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401241"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>Conectar-se a nós de dispositivo no Analytics Platform System
Este artigo explica as várias maneiras de se conectar a cada nó do dispositivo de sistema de plataforma de análise.  
  
## <a name="connecting-with-hadoop"></a>Conectando-se ao Hadoop  
Antes de usar o Hadoop com SQL Server PDW, peça ao administrador do dispositivo para instalar o Java Runtime Environment no SQL Server PDW. Para obter instruções, consulte [Configurar a conectividade do polybase com dados externos &#40;o sistema de plataforma de análise&#41;](configure-polybase-connectivity-to-external-data.md) no guia de operações do dispositivo.  
  
## <a name="connecting-to-appliance-nodes"></a><a name="ConnectingToIndividualNodes"></a>Conectando a nós de dispositivo  
Cada um dos nós de dispositivo é acessado diretamente somente em cenários de uso específicos e por tipos de usuário específicos. A tabela a seguir lista cada nó de dispositivo e os cenários sob os quais os usuários se conectarão diretamente a esse nó.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> Alterar as configurações de banco de dados ou tabela em nós de controle ou de computação sem o consentimento explícito da equipe de produto ou de suporte ao cliente do APS pode tornar seu dispositivo APS sem suporte.
  
|||  
|-|-|  
|**Nó**|**Cenários de acesso**|  
|Nó de controle|Use um navegador da Web para acessar o console de administração, que é executado no nó de controle. Para obter mais informações, consulte [monitorar o dispositivo usando o console de administração &#40;&#41;do sistema de plataforma de análise ](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Todos os aplicativos e ferramentas cliente conectam-se ao nó de controle, independentemente de a conexão estar usando Ethernet ou InfiniBand.<br /><br />Para configurar uma conexão Ethernet para o nó de controle, use o endereço IP do cluster do nó de controle e a porta **17001**. Por exemplo, "192.168.0.1, 17001".<br /><br />Para configurar uma conexão InfiniBand com o nó de controle, use <strong> *appliance_domain*-SQLCTL01 e a</strong> porta **17001**. Usando <strong> *appliance_domain*-SQLCTL01</strong>, o servidor DNS do dispositivo conectará o servidor à rede InfiniBand ativa. Para configurar seu servidor que não seja de dispositivo para usar isso, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).<br /><br />O administrador do dispositivo se conecta ao nó de controle para executar operações de gerenciamento. Por exemplo, o administrador do dispositivo executa as seguintes operações do nó de controle:<br /><br />Configure o sistema de plataforma de análise com a ferramenta de configuração **dwconfig. exe** .|  
|Nó de computação|As conexões do nó de computação são direcionadas pelo nó de controle. Os endereços IP dos nós de computação nunca são inseridos nos comandos do aplicativo como parâmetros.<br /><br />Para carregamento, backup, cópia de tabela remota e Hadoop, SQL Server PDW envia ou recebe dados diretamente em paralelo entre os nós de computação e os nós ou servidores que não são de dispositivo. Esses aplicativos se conectam com SQL Server PDW conectando-se ao nó de controle e, em seguida, o nó de controle direciona SQL Server PDW para estabelecer a comunicação entre os nós de computação e o servidor de não dispositivo.<br /><br />Por exemplo, essas operações de transferência de dados acontecem em paralelo com conexões diretas com os nós de computação:<br /><br />Carregando do servidor de carregamento para SQL Server PDW.<br /><br />Fazer backup de um banco de dados do SQL Server PDW para o servidor de backup.<br /><br />Restaurar um banco de dados do servidor de backup para SQL Server PDW.<br /><br />Consultando dados do Hadoop de SQL Server PDW.<br /><br />Exportando dados de SQL Server PDW para uma tabela externa do Hadoop.<br /><br />Copiar uma tabela de SQL Server PDW para um banco de dados do SMP SQL Server remoto.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>Conectando-se às redes Ethernet e InfiniBand  
Os servidores remotos podem se conectar por meio da rede InfiniBand do dispositivo ou pela rede Ethernet. Por motivos de desempenho, servidores de carregamento, servidores de backup e servidores que recebem dados por meio de instruções de **criação de tabela remota como SELECT** , geralmente transferem dados por meio da rede InfiniBand do dispositivo.  
  
Você pode configurar servidores que não são de dispositivo para pertencer a seu próprio grupo de trabalho ou domínio do cliente e, em seguida, usar sua própria rede do cliente para se conectar a esses servidores e transferir dados para eles. Além disso, os servidores que não são dispositivos conectados ao dispositivo InfiniBand têm a opção de transferir dados entre si pela rede InfiniBand do dispositivo; tenha cuidado com isso porque isso pode reduzir o desempenho do SQL Server PDW.  
  
Por exemplo, essa instrução adiciona credenciais de rede para executar backups por meio de InfiniBand para um servidor de backup que tem um endereço IP de InfiniBand 192.168.0.1. O domínio do dispositivo é *mypdw*e a instrução é executada no servidor de backup. Antes de executar essa instrução, você precisa preencher seus próprios parâmetros.  
  
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
  
