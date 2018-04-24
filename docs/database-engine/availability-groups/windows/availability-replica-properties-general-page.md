---
title: Propriedades da réplica de disponibilidade (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.availabilityreplicaproperties.general.f1
ms.assetid: 8318fefb-e045-4fab-8507-e1951fc7cec6
caps.latest.revision: 14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7604d8688669ded8bfa496924cb87f581f23fb79
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="availability-replica-properties-general-page"></a>Propriedades de réplica de disponibilidade (página Geral)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta caixa de diálogo para exibir as propriedades de uma réplica de disponibilidade.  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para exibir as propriedades da réplica de disponibilidade**  
  
-   [Exibir as propriedades da réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome do grupo de disponibilidade**  
 O nome do grupo de disponibilidade. Esse é um nome especificado pelo usuário que deve ser exclusivo no WSFC (Windows Server Failover Cluster).  
  
 **Instância de servidor**  
 O nome de servidor da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda essa réplica e, para uma instância não padrão, seu nome de instância.  
  
 **Função**  
 **Primária**  
 Atualmente a réplica primária.  
  
 **Secundário**  
 Atualmente uma réplica secundária.  
  
 **Resolvendo**  
 Atualmente, a função de réplica está no processo de ser resolvida para a função primária ou secundária.  
  
 **Modo de disponibilidade**  
 O modo de disponibilidade da réplica. Pode ser:  
  
 **Confirmação assíncrona**  
 A réplica primária pode confirmar transações sem esperar que a réplica secundária grave o log no disco.  
  
 **Confirmação síncrona**  
 A réplica primária espera para confirmar uma determinada transação até que a réplica secundária tenha gravado a transação em disco.  
  
 Para obter mais informações, consulte [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
 **Failover mode**  
 O modo de failover da réplica, um dos seguintes:  
  
 **Automático**  
 Failover automático. A réplica é um destino para failovers automáticos. Essa opção terá suporte apenas se o modo de disponibilidade estiver definido como confirmação síncrona.  
  
 **Manual**  
 Failover manual. O failover da réplica pode ser feito apenas manualmente pelo administrador do banco de dados.  
  
 **Conexões na função primária**  
 O tipo de conexões de cliente com suporte quando a réplica possui a função primária.  
  
 **Permitir todas as conexões**  
 Todas as conexões são permitidas com os bancos de dados na réplica primária. Essa é a configuração padrão.  
  
 **Permitir conexões de leitura/gravação**  
 Conexões em que a propriedade de conexão Application Intent é definida como **ReadOnly** não são permitidas. Quando a propriedade Application Intent está definida como **ReadWrite** ou a propriedade de conexão de intenção de aplicativo não está definida, a conexão é permitida.  
  
 **Secundária Legível**  
 Se uma réplica de disponibilidade que está executando a função primária (isto é, está atuando como uma réplica secundária) pode aceitar conexões de clientes, um dos seguintes:  
  
 **Não**  
 Nenhuma conexão direta é permitida para bancos de dados secundários desta réplica. Eles não estão disponíveis para acesso de leitura. Essa é a configuração padrão.  
  
 **Tentativa de leitura somente**  
 Somente conexões diretas somente leitura são permitidas para bancos de dados secundários desta réplica. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
 **Sim**  
 Todas as conexões são permitidas para os bancos de dados secundários desta réplica, mas somente para acesso de leitura. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
 Para obter mais informações, consulte [Secundárias ativas: réplicas secundárias legíveis &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 **Tempo limite da sessão (segundos)**  
 O período de tempo limite, em segundos. O período de tempo limite é o tempo máximo que a réplica espera para receber uma mensagem de outra réplica antes de considerar que a conexão entre a réplica primária e secundária falhou. O tempo limite da sessão detecta se réplicas secundárias estão conectadas à réplica primária. Ao detectar uma falha de conexão com uma réplica secundária, a réplica primária considera a réplica secundária como NOT_SYNCHRONIZED. Ao detectar uma falha de conexão com a réplica primária, uma réplica secundária simplesmente tenta se conectar outra vez.  
  
> [!NOTE]  
>  Os tempos limites de sessão não causam failovers automáticos.  
  
 **URL do Ponto de Extremidade**  
 Representação de cadeia de caracteres do ponto de extremidade de espelhamento de banco de dados especificado pelo usuário usado pelas conexões entre réplicas primária e secundária para sincronização de dados. Para obter informações sobre a sintaxe das URLs de ponto de extremidade, veja [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
