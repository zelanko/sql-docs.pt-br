---
title: Componentes de hardware
description: O sistema de plataforma de análise (APS) usa componentes escalonáveis para que você possa comprar a quantidade certa de processamento e armazenamento de acordo com seus requisitos de negócios. Ao ordenar APS, você precisará de uma combinação desses componentes principais de hardware.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: db9966315d60fd4de1de7ae6805620d3f2144e6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401140"
---
# <a name="hardware-components-for-analytics-platform-system"></a>Componentes de hardware para o Analytics Platform System

O sistema de plataforma de análise (APS) usa componentes escalonáveis para que você possa comprar a quantidade certa de processamento e armazenamento de acordo com seus requisitos de negócios. Ao ordenar APS, você precisará de uma combinação desses componentes principais de hardware. Fornecedores de hardware específicos podem usar diferentes convenções de nomenclatura ou ter componentes adicionais.  
 
  
## <a name="rack-and-network"></a><a name="rackandnetwork"></a>Rack e rede 
 
Os componentes do APS são todos armazenados em um ou mais racks que se ajustam ao seu data center. Cada rack vem com unidades de distribuição de energia (PDUs), dois interruptores InfiniBand e dois comutadores Ethernet.  
  
![Rack e rede](media/rack-and-network.png "Rack e rede do APS")  
  
## <a name="data-scale-unit"></a><a name="datascaleunit"></a>Unidade de escala de dados
 
Uma unidade de escala de dados contém os hosts de dados e o DAS (armazenamento de conexão direta) para processamento e armazenamento de dados do usuário. Para adicionar capacidade, você adiciona unidades de escala de dados de acordo com as configurações com suporte pelo seu fornecedor de hardware. À medida que aumenta o número de unidades de escala de dados, você precisa adicionar mais componentes de rede & de rack, conforme necessário, para fornecer mais energia, rede e infraestrutura de rack.  
  
### <a name="data-host"></a>Host de dados  

Um host de dados é um servidor dedicado ao processamento de dados do usuário. O PDW (data warehouse paralelo) executa um nó de computação em cada host de dados. Para dispositivos HPE, a unidade de escala de dados tem dois hosts de dados. Para dispositivos Dell e Quantity, a unidade de escala de dados tem três hosts de dados.  
  
### <a name="direct-attached-storage"></a>Armazenamento anexado direto
 
O DAS (armazenamento anexado direto) é um pool de discos conectados aos hosts de dados. Todos os hosts de dados podem acessar qualquer um dos discos. Como parte da arquitetura nada compartilhada, os nós de computação em execução nos hosts de dados não compartilham discos individuais. No entanto, para alta disponibilidade, o acesso de armazenamento é compartilhado e cada um dos hosts de dados pode acessar qualquer um dos discos.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Arquitetura da unidade de escala de dados-DELL e Quantity
  
![Unidade de escalabilidade](media/scalability-unit-dell.png "Unidade de escalabilidade da Dell")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Arquitetura de unidade de escala de dados-HPE 
 
![Unidade de escalabilidade HPE](media/scalability-unit-hpe.png "Unidade de escalabilidade HPE")  
  
### <a name="data-scale-unit-description"></a>Descrição da unidade de escala de dados

Uma unidade de escala de dados tem um servidor (host) para cada nó de computação e uma matriz de discos com conexão direta que é anexada a SAS (Serial Attached SCSI). No gabinete de armazenamento, a matriz de disco é dividida em duas metades, cada uma com fontes de alimentação redundantes. Os espaços de armazenamento do Windows Server gerenciam dados do usuário duplicando os dados entre pares de disco espelhados RAID 1. Os discos em cada par de discos são armazenados em diferentes metades da matriz de discos.  
  
A matriz de discos também contém discos de hot spare e um disco de sistema. Se um disco falhar, os espaços de armazenamento usarão a boa cópia dos dados no disco em funcionamento para recriar uma cópia duplicada dos dados em um hot spare. Esse é um recurso de auto-recuperação importante que ajuda a proteger contra perda de dados.  
  
O número total de discos para os nós de computação:  
  
-   A DELL tem 96 discos = (3 servidores) * (16 discos por servidor \* ) (2 para discos redundantes).  
  
-   HPE tem 64 discos = (2 servidores) * (16 discos por servidor) \* (2 para discos redundantes).  
  
-   Além disso, cada matriz de discos tem discos sobressalentes ativos e um disco do sistema.  
  
**Para alta disponibilidade**, quando um nó de computação faz failover, ele ainda pode funcionar e acessar seus dados de usuário por meio do outro host na unidade de escala de dados. Pelo menos um dos hosts físicos conectados diretamente deve estar funcionando ou o acesso a dados para o armazenamento é perdido.  
  
**Para tamanhos de disco**, o armazenamento de conexão direta pode ter unidades de disco de 1, 2 ou 3 terabytes. Todas as unidades de escala de dados devem ter discos do mesmo tamanho.  
  
## <a name="base-scale-unit"></a><a name="basescaleunit"></a>Unidade de escala de base 
 
A unidade de escala de base contém o número mínimo de hosts de energia cérebro, hosts de dados e armazenamento de conexão direta que é necessário para o dispositivo. Ele inclui os componentes a seguir. 
  
### <a name="orchestration-host"></a>Host de orquestração  
Este servidor executa o cérebro do PDW.
  
### <a name="passive-host"></a>Host passivo  
Esse servidor fornece alta disponibilidade. Ele está online e pronto para executar trabalhos caso haja uma falha na orquestração ou no host de dados. O host de orquestração, o host passivo e os servidores de unidade de escala de dados são configurados como um cluster de failover do Windows. Cada rack do dispositivo requer um host passivo.  
  
### <a name="optional-passive-host"></a>Host passivo opcional  
Para adicionar mais redundância, você tem a opção de adicionar um segundo host passivo à unidade de escala base.  
  
### <a name="data-scale-unit"></a>Unidade de escala de dados  
A unidade de escala de base inclui uma unidade de escala de dados que é colocada na parte inferior do rack.  
  
Este diagrama mostra a unidade de escala de base mais o rack e a rede. Esta é a configuração mínima para um dispositivo de sistema de plataforma de análise.  
  
![Unidade de escala de base](media/base-scale-unit.png "Unidade de escala de base")  
 
