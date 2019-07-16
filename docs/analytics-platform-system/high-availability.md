---
title: Alta disponibilidade no Analytics Platform System | Microsoft Docs
description: Saiba como o Analytics Platform System (APS) foi projetado para alta disponibilidade.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cdf1837bd3b3b1cdf8e189ae591cd6fbff58387a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960862"
---
# <a name="analytics-platform-system-high-availability"></a>Alta disponibilidade do Analytics Platform System
Saiba como o Analytics Platform System (APS) foi projetado para alta disponibilidade.  
  
## <a name="high-availability-architecture"></a>Arquitetura de alta disponibilidade  
![Arquitetura de dispositivo](media/appliance-architecture.png "arquitetura de dispositivo")  
  
## <a name="network"></a>Rede  
Disponibilidade da rede, o dispositivo de APS tem duas redes InfiniBand. Se uma das redes InfiniBand ficar inativo, o outro é ainda estão disponíveis. Além disso, Active Directory replicou os controladores de domínio para resolver as solicitações de entrada para a rede InfiniBand correta.  
  
Para obter mais informações, consulte [adaptadores de rede InfiniBand configurar](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Armazenamento  
Para manter os dados seguros, APS usa RAID 1 espelhamento para manter duas cópias de todos os dados de usuário. Quando um disco falhar, o sistema de hardware recria os dados em um disco de reposição e define um alerta que há uma falha de disco.  
  
Para manter os dados disponíveis online, o APS usa espaços de armazenamento do Windows e volumes compartilhados do cluster para gerenciar os discos de dados de usuário no armazenamento anexado direto. Há um pool de armazenamento por unidade de escala de dados organizado em Volumes Compartilhados do Cluster que estão disponíveis para os hosts do nó de computação por meio de pontos de montagem.  
  
Para garantir que o pool de armazenamento permanece online, cada host na unidade de escala de dados tem uma máquina virtual ISCSI que não faz failover. Essa arquitetura é importante porque, se um host falhar, os dados ainda pode ser acessados por meio de outros hosts na unidade de escala de dados.  
  
## <a name="hosts"></a>Hosts  
Para obter disponibilidade de host, todos os hosts são configurados em um Cluster de Failover do Windows. Cada rack tem um host passivo. Opcionalmente, primeiro rack, que controla o SQL Server Parallel Data Warehouse (PDW) e a malha de dispositivo, pode ter um segundo host passivo. Se um host falhar, as máquinas virtuais são configuradas para failover, irão falhar para um host de passivo disponíveis.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>Malha de dispositivo e nós do PDW  
Para alta disponibilidade de nós PDW e a malha de dispositivo de APS usa a virtualização. Cada um dos componentes da malha do dispositivo e PDW executado em uma máquina virtual.  
  
Cada máquina virtual é definida como uma função no cluster de failover do Windows. Quando uma máquina virtual falhar, o cluster reinicia-o em um host de passivo disponível. As máquinas virtuais são implantadas usando o System Center Virtual Machine Manager. Quando ocorre um failover, a máquina virtual em execução no host passivo é ainda poderão acessar seus dados de usuário por meio da rede InfiniBand.  
  
O nó de controle e as máquinas virtuais de nó de computação são configuradas como um cluster de nó único. O cluster de nó único gerencia as redes InfiniBand como um recurso de cluster para garantir que o cluster sempre está usando o Active Directory IP InfiniBand. O cluster de nó único gerencia os processos do PDW que são executados dentro da máquina virtual. Por exemplo, o cluster de nó único tem SQL Server e o serviço de movimentação de dados (DMS) como recursos para que ele pode iniciá-los na ordem correta. O nó de controle VM também controla a ordem de inicialização para as outras VMs que são executados no host de orquestração.  
  
