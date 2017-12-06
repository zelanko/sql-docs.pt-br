---
title: Grupo de disponibilidade AlwaysOn para SQL Server no Linux | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.workload: On Demand
ms.openlocfilehash: 2b9d80b92fd189340c5c15504ab37a8c0022df85
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="availability-groups-for-sql-server-on-linux"></a>Grupos de disponibilidade para o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Um grupo de disponibilidade do SQL Server Always On é uma alta disponibilidade (HA), a recuperação de desastres (DR) e solução de expansão. Ele fornece alta disponibilidade para grupos de bancos de dados no armazenamento anexado direto. Ele suporta vários secundários para alta disponibilidade integrada e DR, detecção de falha automático, failover rápido transparente e balanceamento de carga de leitura. Este conjunto amplo de recursos permite que você obter disponibilidade ideal SLAs para suas cargas de trabalho.

Grupos de disponibilidade do SQL Server foram introduzidos no SQL Server 2012 e foram aprimorados com cada versão. Esse recurso agora está disponível no Linux. Para acomodar as cargas de trabalho do SQL Server com os requisitos de continuidade de negócios rigorosos, grupos de disponibilidade é executada em todas suporte [distribuições do sistema operacional Linux](sql-server-linux-release-notes.md). Além disso, todos os recursos que tornam uma solução de recuperação de desastres de alta disponibilidade flexível, integrada e eficiente de grupos de disponibilidade também estão disponíveis no Linux. Eles incluem: 

- **Failover de vários bancos de dados** um grupo de disponibilidade dá suporte a um ambiente de failover para um conjunto de bancos de dados do usuário, conhecidos como bancos de dados de disponibilidade.
- **Rápida detecção de falha e failover** como um recurso em um cluster de alta disponibilidade, um grupo de disponibilidade se beneficia de inteligência de cluster internos para detecção de failover imediato e ação de failover.
- **Failover transparente usando o recurso IP virtual** permite que o cliente para usar a cadeia de caracteres de conexão única para o primário no caso de failover. Requer a integração com um Gerenciador de cluster.
- **Vários secundários síncronos e assíncronos** um grupo de disponibilidade dá suporte a até oito réplicas secundárias. Com réplicas síncronas a réplica primária espera para confirmar a transação, que a réplica primária espera para transações a serem gravadas em disco no log de transações. A réplica primária não espera para gravações assíncronas réplicas síncronas.  
- **Failover manual ou automático** Failover para uma réplica secundária síncrona pode ser acionado automaticamente pelo cluster ou sob demanda pelo administrador do banco de dados.
- **Secundárias ativas disponíveis para cargas de trabalho de leitura e de backup** uma ou mais réplicas secundárias podem ser configuradas para dar suporte ao acesso somente leitura aos bancos de dados secundários e/ou para permitir backups de bancos de dados secundários.
- **A propagação automática** do SQL Server cria automaticamente as réplicas secundárias para cada banco de dados no grupo de disponibilidade.
- **Roteamento somente leitura** do SQL Server encaminha as conexões de entrada para um ouvinte de grupo de disponibilidade para uma réplica secundária que está configurado para permitir cargas de trabalho somente leitura. 
- **Gatilho de failover e monitoramento de integridade de nível de banco de dados** diagnóstico e monitoramento de nível de banco de dados aprimorados. 
- **Configurações de recuperação de desastres** com grupos de disponibilidade distribuída ou a configuração do grupo de disponibilidade de várias sub-redes. 
- **Recursos de dimensionamento de leitura** no SQL Server 2017 você pode criar um grupo de disponibilidade com ou sem alta disponibilidade para operações somente leitura de expansão. 


Para obter detalhes sobre grupos de disponibilidade do SQL Server, consulte [grupos de disponibilidade do SQL Server Always On](http://msdn.microsoft.com/library/hh510230.aspx).

## <a name="availability-group-terminology"></a>Terminologia do grupo de disponibilidade

Um grupo de disponibilidade dá suporte a um ambiente de failover para um conjunto discreto de bancos de dados de usuário - conhecidos como bancos de dados de disponibilidade - que fazem failover juntos. Um grupo de disponibilidade dá suporte a um conjunto de bancos de dados primários de leitura-gravação e uma a oito conjuntos de bancos de dados secundários correspondentes. Opcionalmente, é possível tornar disponíveis os bancos de dados secundários para acesso somente leitura e/ou algumas operações de backup. Um grupo de disponibilidade define um conjunto de dois ou mais parceiros de failover, conhecidos como réplicas de disponibilidade. Réplicas de disponibilidade são componentes do grupo de disponibilidade. Para obter detalhes, consulte [visão geral do AlwaysOn em grupos de disponibilidade (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Os termos a seguir descrevem as principais partes de uma solução de grupo de disponibilidade do SQL Server:

 grupo de disponibilidade  
 Um contêiner para um conjunto de bancos de dados, *bancos de dados de disponibilidade*, que executam failover juntos.  
  
 banco de dados de disponibilidade  
 Um banco de dados que pertence a um grupo de disponibilidade. Para cada banco de dados de disponibilidade, o grupo de disponibilidade mantém uma única cópia de leitura/gravação (o *banco de dados primário*) e de uma a oito cópias somente leitura (*bancos de dados secundários*).  
  
 banco de dados primário  
 A cópia de leitura-gravação de um banco de dados de disponibilidade.  
  
 banco de dados secundário  
 Uma cópia somente leitura de um banco de dados de disponibilidade.  
  
 réplica de disponibilidade  
 Uma instanciação de um grupo de disponibilidade que é hospedado por uma instância específica do SQL Server e mantém uma cópia local de cada banco de dados de disponibilidade que pertence ao grupo de disponibilidade. Existem dois tipos de réplica de disponibilidade: uma única *réplica primária* e uma a oito *réplicas secundárias*.  
  
 réplica primária  
 A réplica de disponibilidade que torna disponíveis os bancos de dados primários para conexões de leitura/gravação de clientes e, também, envia registros do log de transações para cada banco de dados primário a toda réplica secundária.  
  
 réplica secundária  
 Uma réplica de disponibilidade que mantém uma cópia secundária de cada banco de dados de disponibilidade e serve como destinos potenciais de failover para o grupo de disponibilidade. Opcionalmente, uma réplica secundária pode incluir o suporte ao acesso somente leitura para que bancos de dados secundários possam oferecer suporte à criação de backups em bancos de dados secundários.  
  
 ouvinte do grupo de disponibilidade  
 Um nome de servidor ao qual os clientes podem se conectar para acessar um banco de dados em uma réplica primária ou secundária de um grupo de disponibilidade. Os ouvintes de grupo de disponibilidade direcionam conexões de entrada para a réplica primária ou para uma réplica secundária somente leitura.  


## <a name="new-in-sql-server-2017-for-availability-groups"></a>Novo no SQL Server 2017 para grupos de disponibilidade

SQL Server 2017 apresenta novos recursos para grupos de disponibilidade.

**CLUSTER_TYPE** usar com `CREATE AVAILABILITY GROUP`. Identifica o tipo de Gerenciador de cluster de servidor que gerencia um grupo de disponibilidade. Pode ser um dos seguintes tipos:

   - **WSFC** Winows cluster de failover de servidor. No Windows, é o valor padrão para CLUSTER_TYPE.
   - **EXTERNA** um Gerenciador de cluster é não failover cluster do Windows server - por exemplo, no Linux com Pacemaker.
   - **NENHUM** nenhum Gerenciador de cluster. Usado para um grupo de disponibilidade de escala de leitura.

Para obter mais informações sobre essas opções, consulte [criar grupo de disponibilidade](http://msdn.microsoft.com/library/ff878399.aspx) ou [ALTER AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878601.aspx).

**Garantia de confirmação em réplicas secundárias síncronas**

Use `required_synchronized_secondaries_to_commit`with `CREATE AVAILABILITY GROUP` or `ALTER AVAILABILITY GROUP`. Quando `required_synchronized_secondaries_to_commit` é definido como um valor maior que 0, as transações em que a réplica primária, bancos de dados aguardará até que a transação é confirmada no número especificado de **secundário síncrono** logs de transação do banco de dados de réplica. Se suficiente réplicas secundárias síncronas não estão online, todas as conexões à réplica primária serão rejeitadas até que continue a comunicação com réplicas secundárias suficientes.

**Grupos de disponibilidade de escala de leitura**

Crie um grupo de disponibilidade sem um cluster para oferecer suporte a cargas de trabalho de leitura de escala. Consulte [grupos de disponibilidade de escala de leitura](../database-engine/availability-groups/windows/read-scale-availability-groups.md).

## <a name="next-steps"></a>Próximas etapas

[Configurar o grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md)

[Configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux](sql-server-linux-availability-group-configure-rs.md)

[Adicionar grupo de disponibilidade do recurso de Cluster em RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[Adicionar grupo de disponibilidade do recurso de Cluster em SLES](sql-server-linux-availability-group-cluster-sles.md)

[Adicionar grupo de disponibilidade do recurso de Cluster no Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)
