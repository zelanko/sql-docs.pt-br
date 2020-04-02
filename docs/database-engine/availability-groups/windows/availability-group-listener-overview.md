---
title: O que é um ouvinte de grupo de disponibilidade?
description: 'Uma visão geral do ouvinte do grupo de disponibilidade Always On e como ele funciona para direcionar o tráfego automaticamente para o servidor pretendido. '
ms.custom: seodec18
ms.date: 02/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 19718f762a7352865c5b9741ee42ec8cfe965eb8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79434519"
---
# <a name="what-is-an-availability-group-listener"></a>O que é um ouvinte de grupo de disponibilidade?  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Um ouvinte do grupo de disponibilidade é um VNN (nome de rede virtual) ao qual os clientes podem se conectar para acessar um banco de dados em uma réplica primária ou secundária de um grupo de disponibilidade Always On. Um ouvinte permite que um cliente conecte-se a uma réplica sem precisar saber o nome da instância física do SQL Server. Como o ouvinte roteia o tráfego, a cadeia de conexão do cliente não precisa ser modificada após a ocorrência de um failover. 

Um ouvinte de grupo de disponibilidade consiste em um nome de ouvinte DNS, designação de porta de ouvinte ou um ou mais endereços IP. Apenas o protocolo TCP tem suporte do ouvinte de grupo de disponibilidade.  O nome DNS do ouvinte deve ser exclusivo no domínio e no NetBIOS.  Quando você cria um ouvinte, ele se torna um recurso em um cluster com um VNN (nome de rede virtual), um VIP (IP virtual) e dependência de grupo de disponibilidade associados. Um cliente usa o DNS para resolver o VNN em vários endereços IP e depois tenta se conectar a cada endereço, até uma solicitação de conexão ser bem-sucedida ou até a solicitação de conexão atingir seu tempo limite.  
  
Se o roteamento somente leitura estiver configurado para uma ou mais [réplicas secundárias para leitura](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md), as conexões do cliente com intenção de leitura ao ouvinte serão automaticamente redirecionadas para uma réplica secundária para leitura. 
  
Este artigo apresenta uma visão geral de um ouvinte de grupo de disponibilidade. Você também pode [configurar o ouvinte](create-or-configure-an-availability-group-listener-sql-server.md) e, em seguida, aprender a [conectar-se ao ouvinte](listeners-client-connectivity-application-failover.md).
  
  
##  <a name="listener-parameters"></a><a name="AGlConfig"></a> Parâmetros do ouvinte  

 Um ouvinte de grupo de disponibilidade usa o seguinte:
  
 **Um nome DNS exclusivo**  
 Isso também é conhecido como um VNN (nome de rede virtual). As regras de nomeação do Active Directory para nomes de host DNS se aplicam. Para obter mais informações, consulte o artigo da Base de Dados de Conhecimento [Convenções de nomenclatura no Active Directory para computadores, domínios, sites e unidades organizacionais](https://support.microsoft.com/kb/909264) .  
  
**Um ou mais endereços IP virtuais (VIPs)**  
 VIPs são configurados para uma ou mais sub-redes para as quais o grupo de disponibilidade faz failover.  
  
**Configuração do endereço IP**  
 Para um ouvinte de grupo de disponibilidade específico, o endereço IP pode usar o protocolo DHCP ou um ou mais endereços IP estáticos. O uso do DHCP pode causar atrasos de conectividade durante o failover e, portanto, não é recomendado em ambientes de produção. Os grupos de disponibilidade que se estendem por várias sub-redes ou usam configurações de rede híbrida devem usar um endereço IP estático. 
 
  
##  <a name="listener-port"></a><a name="SelectListenerPort"></a> Porta do ouvinte 
 Ao configurar um ouvinte de grupo de disponibilidade, você precisa designar uma porta.  Você pode configurar a porta padrão como 1433 para simplicidade das cadeias de conexão de cliente. Ao usar 1433, você não precisa designar um número de porta em uma cadeia de conexão. Além disso, como cada ouvinte de grupo de disponibilidade terá um nome de rede virtual separado, cada ouvinte de grupo de disponibilidade configurado em um único WSFC poderá ser configurado para fazer referência à mesma porta padrão de 1433.  
  
 Você também pode designar uma porta de ouvinte sem padrão. Porém isso significa que você também precisará especificar uma porta de destino explicitamente em sua cadeia de conexão ao conectar-se ao ouvinte de grupo de disponibilidade.  Você também precisará da permissão de abertura no firewall para a porta sem padrão.  
  
 Se você usar a porta padrão de 1433 para VNNs de ouvinte de grupo de disponibilidade, você ainda precisará garantir que nenhum outro serviço no nó de cluster esteja usando essa porta; caso contrário, isso causará um conflito de porta.  
  
 Se uma das instâncias do SQL Server já estiver escutando na porta TCP 1433 por meio do ouvinte da instância e não houver nenhum outro serviço (inclusive instâncias adicionais do SQL Server) no computador que escuta na porta 1433, isso não provocará um conflito de porta com o ouvinte de grupo de disponibilidade.  Isso ocorre porque o ouvinte de grupo de disponibilidade pode compartilhar a mesma porta TCP no mesmo processo de serviço.  No entanto, não devem ser configuradas várias instâncias do SQL Server (lado a lado) para escutar na mesma porta.  
  
  
##  <a name="behavior-of-client-connections-on-failover"></a><a name="CCBehaviorOnFailover"></a> Comportamento de conexões de cliente em failover  

 Quando ocorrer um failover de grupo de disponibilidade, as conexões persistentes ao grupo de disponibilidade são terminadas e o cliente deve estabelecer uma nova conexão para continuar trabalhando com o mesmo banco de dados primário ou banco de dados secundário somente leitura.  Enquanto um failover estiver ocorrendo no lado do servidor, a conectividade com o grupo de disponibilidade pode falhar, forçando o aplicativo cliente a repetir a conexão até que o primário seja colocado completamente online.  
  
 Se o grupo de disponibilidade voltar a ficar online durante a tentativa de conexão de um aplicativo cliente, mas antes do tempo limite da conexão, o driver cliente poderá conectar-se com êxito durante uma de suas tentativas internas e não ocorrerá nenhum erro no aplicativo nesse caso.  


## <a name="next-steps"></a>Próximas etapas

Agora que você está familiarizado com o modo como um ouvinte de grupo de disponibilidade funciona, [crie o ouvinte](create-or-configure-an-availability-group-listener-sql-server.md) e, em seguida, configure seu aplicativo para [conectar-se ao ouvinte](listeners-client-connectivity-application-failover.md). Você também pode examinar várias [estratégias de monitoramento do grupo de disponibilidade](monitoring-of-availability-groups-sql-server.md) para garantir a integridade do seu grupo de disponibilidade. 

Para obter mais informações sobre grupos de disponibilidade, confira a [Visão geral dos grupos de disponibilidade Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md). 
  

  
  
