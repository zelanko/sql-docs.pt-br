---
title: Suporte para alta disponibilidade, recuperação de desastres para o Microsoft Drivers for PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb0af342ac2ccbe916fba9edb497e8197b2fe7f5
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783828"
---
# <a name="support-for-high-availability-disaster-recovery"></a>Suporte a alta disponibilidade e recuperação de desastres
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico aborda o suporte a [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] (adicionado na versão 3.0) para alta disponibilidade, recuperação de desastre – [!INCLUDE[ssHADR](../../includes/sshadr_md.md)].  O suporte ao [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] foi adicionado no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Para obter mais informações sobre o [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Na versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], você pode especificar o ouvinte do grupo de disponibilidade de um AG (grupo de disponibilidade) (alta disponibilidade, recuperação de desastre) na propriedade de conexão. Se um aplicativo [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] estiver conectado a um banco de dados AlwaysOn que efetua failover, a conexão original será interrompida e o aplicativo deverá abrir uma nova conexão para continuar o trabalho após o failover.  
  
Se você não estiver se conectando a um ouvinte de grupo de disponibilidade, e se vários endereços IP forem associados com um nome de host, o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] vai iterar em sequência por todos os endereços IP associados à entrada DNS. Isso pode demorar muito se o primeiro endereço IP retornado pelo servidor DNS não estiver associado a nenhuma NIC (placa de interface de rede). Ao conectar-se a um ouvinte de grupo de disponibilidade, o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] tenta estabelecer conexões com todos os endereços IP paralelamente e, se uma conexão tentar continuar, o driver descartará qualquer tentativa de conexão pendente.  
  
> [!NOTE]  
> O aumento do tempo limite de conexão e a implementação de lógica de repetição de conexão aumentarão a probabilidade de um aplicativo se conectar a um grupo de disponibilidade. Além disso, como uma conexão pode falhar devido a um failover de grupo de disponibilidade, você deve implementar lógica de repetição de conexão, repetindo uma conexão com falha até se reconectar.  
  
## <a name="connecting-with-multisubnetfailover"></a>Conectando-se ao MultiSubnetFailover  
A propriedade de conexão **MultiSubnetFailover** indica que o aplicativo está sendo implantado em um grupo de disponibilidade ou instância de cluster de failover e que o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] tentará se conectar ao banco de dados na instância primária do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentando se conectar a todos os endereços IP do grupo de disponibilidade. Quando **MultiSubnetFailover=true** é especificado para uma conexão, o cliente repete as tentativas de conexão TCP mais rápido do que os intervalos de retransmissão TCP padrão do sistema operacional. Isto permite uma reconexão mais rápida depois de failover de um Grupo de disponibilidade AlwaysOn ou uma Instância de Cluster de Failover AlwaysOn e é aplicável a Grupos de disponibilidade único e de várias sub-redes e Instâncias de Cluster de Failover.  
  
Sempre especifique **MultiSubnetFailover=True** quando for se conectar a um ouvinte de grupo de disponibilidade do SQL Server 2012 ou uma instância de cluster de failover do SQL Server 2012. **MultiSubnetFailover** permite o failover mais rápido para todos os grupos de disponibilidade e as instâncias de cluster de failover do SQL Server 2012 e reduz significativamente o tempo de failover para topologias AlwaysOn de uma ou várias sub-redes. Durante um failover de várias sub-redes, o cliente tentará conexões em paralelo. Durante um failover de sub-rede, o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] repetirá agressivamente a conexão TCP.  
  
Para obter mais informações sobre palavras-chave de cadeia de caracteres de conexão no [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], consulte [opções de Conexão](../../connect/php/connection-options.md).  
  
A especificação de **MultiSubnetFailover=true** durante a conexão a algo que não seja um ouvinte de grupo de disponibilidade ou uma Instância de Cluster de Failover pode resultar em um impacto de desempenho negativo e não há suporte para isso.  
  
Use as diretrizes a seguir para conectar-se a um servidor em um grupo de disponibilidade:  
  
-   Use a propriedade de conexão **MultiSubnetFailover** quando estiver se conectando a uma ou várias sub-redes; isso melhorará o desempenho em ambos os casos.  
  
-   Para conectar-se a um grupo de disponibilidade, especifique o ouvinte do grupo de disponibilidade como o servidor em sua cadeia de conexão.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada com mais de 64 endereços IP causará uma falha de conexão.  
  
-   O comportamento de um aplicativo que usa a propriedade de conexão **MultiSubnetFailover** não é afetado com base no tipo de autenticação: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticação, Autenticação Kerberos ou Autenticação do Windows.  
  
-   Aumente o valor de **loginTimeout** para acomodar o tempo de failover e reduzir as tentativas de repetição de conexão do aplicativo.  
  
-   Não há suporte a transações distribuídas.  
  
Se o roteamento somente leitura não estiver em ação, conectar-se a um local de réplica secundária em um grupo de disponibilidade apresentará falha nas seguintes situações:  
  
- Se o local de réplica secundário não for configurado para aceitar conexões.  
  
- Se um aplicativo usar **ApplicationIntent=ReadWrite** (discutido abaixo) e o local de réplica secundária estiver configurado para acesso somente leitura.  
  
Uma conexão falhará se uma réplica primária for configurada para rejeitar cargas de trabalho somente leitura e a cadeia de conexão contiver **ApplicationIntent=ReadOnly**.  

## <a name="transparent-network-ip-resolution-tnir"></a>Resolução IP de Rede Transparente (TNIR)

Resolução de IP de rede transparente (TNIR) é uma revisão do recurso MultiSubnetFailover existente. Ele afeta a sequência de conexão do driver quando o primeiro resolvida IP do nome do host não responde e há vários IPs associados com o nome do host. Junto com MultiSubnetFailover eles fornecem as sequências de conexão de quatro a seguir: 

- TNIR habilitado e desabilitado MultiSubnetFailover: um IP for tentado, seguido por todos os IPs em paralelo
- TNIR habilitada & MultiSubnetFailover habilitado: todos os IPs são tentadas em paralelo
- Desabilitado TNIR & MultiSubnetFailover desabilitado: todos os IPs são tentadas após o outro
- Desabilitado TNIR & MultiSubnetFailover habilitado: todos os IPs são tentadas em paralelo

TNIR é habilitado por padrão e MultiSubnetFailover é desabilitada por padrão.

Este é um exemplo de habilitação TNIR e MultiSubnetFailover usando o driver PDO_SQLSRV:

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$connectionString = "sqlsrv:Server=$serverName; TransparentNetworkIPResolution=Enabled; MultiSubnetFailover=yes";
try {
    $conn = new PDO($connectionString, $username, $password, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
    // your code 
    // more of your code
    // when done, close the connection
    unset($conn);
} catch(PDOException $e) {
    print_r($e->errorInfo);
}
?>
```

## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Atualizando para usar clusters de várias sub-redes a partir do espelhamento de banco de dados  
Um erro de conexão ocorrerá se as palavras-chave de conexão **MultiSubnetFailover** e **Failover_Partner** estiverem presentes na cadeia de conexão. Um erro também ocorrerá se a palavra-chave **MultiSubnetFailover** for usada e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornar uma resposta de parceiro de failover indicando que ela faz parte de um par de espelhamento de banco de dados.  
  
Se você atualizar um aplicativo [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] que atualmente usa o espelhamento de banco de dados em um cenário de várias sub-redes, deverá remover a propriedade de conexão **Failover_Partner** e substituí-la por **MultiSubnetFailover** definido como **Yes** e substituir o nome do servidor da cadeia de conexão por um ouvinte de grupo de disponibilidade. Se uma cadeia de conexão usa **Failover_Partner** e **MultiSubnetFailover=true**, o driver gerará um erro. No entanto, se uma cadeia de conexão usar **Failover_Partner** e **MultiSubnetFailover=false** (ou **ApplicationIntent=ReadWrite**), o aplicativo usará o espelhamento de banco de dados.  
  
O driver retornará um erro se o espelhamento de banco de dados for usado no banco de dados primário no AG e se **MultiSubnetFailover=true** for usado na cadeia de conexão que se conecta a um banco de dados primário, em vez de ao ouvinte de um grupo de disponibilidade.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>Consulte Também  
[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)  
  
