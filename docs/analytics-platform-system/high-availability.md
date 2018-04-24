---
title: Alta disponibilidade em Analytics Platform System | Microsoft Docs
description: Saiba como Analytics Platform System (APS) foi projetado para alta disponibilidade.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5c8a562ab105e1bc40b590916d0881757036aeff
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="analytics-platform-system-high-availability"></a>Alta disponibilidade do sistema de plataforma de análise
Saiba como Analytics Platform System (APS) foi projetado para alta disponibilidade.  
  
## <a name="high-availability-architecture"></a>Arquitetura de alta disponibilidade  
![Arquitetura de dispositivo](media/appliance-architecture.png "arquitetura de dispositivo")  
  
## <a name="network"></a>Rede  
Disponibilidade da rede, o dispositivo de APS tem duas redes InfiniBand. Se uma das redes InfiniBand falhar, outro ainda está disponível. Além disso, o Active Directory replicou os controladores de domínio para resolver solicitações de entrada para a rede InfiniBand correta.  
  
Para obter mais informações, consulte [adaptadores de rede InfiniBand configurar](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Armazenamento  
Para manter os dados protegidos, APS usa RAID 1 espelhamento para manter as duas cópias de todos os dados de usuário. Quando um disco falhar, o sistema de hardware recria os dados em um disco de reposição e define um alerta se há uma falha de disco.  
  
Para manter os dados disponíveis online, o APS usa espaços de armazenamento do Windows e volumes compartilhados do cluster para gerenciar os discos de dados de usuário no armazenamento anexado direto. Há um pool de armazenamento por unidade de escala de dados organizado em Volumes Compartilhados do Cluster que estão disponíveis para os hosts do nó de computação por meio de pontos de montagem.  
  
Para garantir que o pool de armazenamento permanece online, cada host na unidade de escala de dados tem uma máquina virtual ISCSI que não o failover não. Essa arquitetura é importante porque, se um host falhar, os dados ainda pode ser acessados por meio de outros hosts na unidade de escala de dados.  
  
## <a name="hosts"></a>hosts  
Disponibilidade de host, todos os hosts são configurados em um Cluster de Failover do Windows. Cada rack tem um host de passivo. Opcionalmente, o primeiro rack, que controla o SQL Server Parallel Data Warehouse (PDW) e da malha de dispositivo, pode ter um segundo host passivo. Se um host falhar, máquinas virtuais que são configuradas para failover, serão failover para um host passivo disponíveis.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>Malha de dispositivo e nós PDW  
Para alta disponibilidade de nós PDW e a malha de dispositivo, APS usa a virtualização. Cada um dos componentes de malha PDW e o dispositivo executado em uma máquina virtual.  
  
Cada máquina virtual é definida como uma função do cluster de failover do Windows. Quando uma máquina virtual falhar, o cluster reinicia em um host passivo disponível. As máquinas virtuais são implantadas usando o System Center Virtual Machine Manager. Quando ocorre um failover, a máquina virtual em execução no host passivo é ainda podem acessar seus dados de usuário por meio da rede InfiniBand.  
  
O nó de controle e VMs do nó de computação são configurados como um cluster de nó único. O cluster de nó único gerencia as redes InfiniBand como um recurso de cluster para garantir que o cluster está sempre usando o IP InfiniBand active. O cluster de nó único gerencia os processos PDW que são executados na máquina virtual. Por exemplo, o cluster de nó único tem SQL Server e o serviço de movimentação de dados (DMS) como recursos de forma que ele pode iniciá-los na ordem correta. Nó de controle VM também controla a ordem de inicialização para as outras VMs que são executados no host de orquestração.  
  
