---
title: Alta disponibilidade
description: Saiba como o Analytics Platform System (APS) é arquitetado para alta disponibilidade.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6246ed25909a2e366d8bbafcd912a4fd923cc84a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401098"
---
# <a name="analytics-platform-system-high-availability"></a>Alta disponibilidade do sistema de plataforma de análise
Saiba como o Analytics Platform System (APS) é arquitetado para alta disponibilidade.  
  
## <a name="high-availability-architecture"></a>Arquitetura da Alta Disponibilidade  
![Arquitetura do dispositivo](media/appliance-architecture.png "Arquitetura do dispositivo")  
  
## <a name="network"></a>Rede  
Para disponibilidade de rede, o dispositivo APS tem duas redes InfiniBand. Se uma das redes InfiniBand falhar, a outra ainda estará disponível. Além disso, Active Directory tiver replicado controladores de domínio para resolver solicitações de entrada para a rede InfiniBand correta.  
  
Para obter mais informações, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Armazenamento  
Para manter os dados seguros, o APS usa o espelhamento RAID 1 para manter duas cópias de todos os dados do usuário. Quando um disco falha, o sistema de hardware recria os dados em um disco sobressalente e define um alerta de que há uma falha no disco.  
  
Para manter os dados disponíveis online, os APS usam espaços de armazenamento do Windows e volumes compartilhados clusterizados para gerenciar os discos de dados do usuário no armazenamento de conexão direta. Há um pool de armazenamento por unidade de escala de dados organizado em volumes compartilhados do cluster que estão disponíveis para os hosts do nó de computação por meio de pontos de montagem.  
  
Para garantir que o pool de armazenamento permaneça online, cada host na unidade de escala de dados tem uma máquina virtual ISCSI que não faz failover. Essa arquitetura é importante porque, se um host falhar, os dados ainda estarão acessíveis por meio de outros hosts na unidade de escala de dados.  
  
## <a name="hosts"></a>Hosts  
Para a disponibilidade do host, todos os hosts são configurados em um cluster de failover do Windows. Todo rack tem um host passivo. Opcionalmente, o primeiro rack, que controla SQL Server PDW (data warehouse paralelo) e a malha do dispositivo, pode ter um segundo host passivo. Se um host falhar, as máquinas virtuais configuradas para failover executarão o failover para um host passivo disponível.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>Nós de PDW e malha de dispositivo  
Para alta disponibilidade dos nós do PDW e da malha do dispositivo, o APS usa a virtualização. Cada um dos componentes do PDW e do Appliance Fabric é executado em uma máquina virtual.  
  
Cada máquina virtual é definida como uma função no cluster de failover do Windows. Quando uma máquina virtual falha, o cluster a reinicia em um host passivo disponível. As máquinas virtuais são implantadas usando System Center Virtual Machine Manager. Quando ocorre um failover, a máquina virtual em execução no host passivo ainda é capaz de acessar seus dados de usuário por meio da rede InfiniBand.  
  
As máquinas virtuais do nó de controle e do nó de computação são cada uma configurada como um cluster de nó único. O cluster de nó único gerencia as redes InfiniBand como um recurso de cluster para garantir que o cluster esteja sempre usando o IP de InfiniBand ativo. O cluster de nó único gerencia os processos do PDW executados na máquina virtual. Por exemplo, o cluster de nó único tem SQL Server e serviço de movimentação de dados (DMS) como recursos para que possa iniciá-los na ordem correta. A VM do nó de controle também controla a ordem de inicialização para as outras VMs que são executadas no host de orquestração.  
  
