---
title: Componentes de hardware - Analytics Platform System | Microsoft Docs
description: Analytics Platform System (APS) usa componentes escalonáveis, de forma que você pode comprar a quantidade certa de processamento e armazenamento de acordo com seus requisitos de negócios. Ao fazer o pedido APS, você precisará de uma combinação desses componentes de hardware principal.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 9bb7b67a896164fe29611da2091e02c700c46970
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="hardware-components-for-analytics-platform-system"></a>Componentes de hardware para Analytics Platform System

Analytics Platform System (APS) usa componentes escalonáveis, de forma que você pode comprar a quantidade certa de processamento e armazenamento de acordo com seus requisitos de negócios. Ao fazer o pedido APS, você precisará de uma combinação desses componentes de hardware principal. Fornecedores de hardware específico podem usar as convenções de nomenclatura diferentes ou ter componentes adicionais.  
 
  
## <a name="rackandnetwork"></a>Rack e rede 
 
Todos os componentes APS são armazenados em um ou mais racks que se encaixam em seu data center. Cada rack vem com dois switches Ethernet, dois comutadores InfiniBand e unidades de distribuição de alimentação (PDUs).  
  
![Rack e rede](media/rack-and-network.png "APS rack e de rede")  
  
## <a name="datascaleunit"></a>Unidade de escala de dados
 
Uma unidade de escala de dados contém os hosts de dados e o armazenamento anexado direto (DAS) para processar e armazenar dados de usuário. Para adicionar capacidade, você adicionar unidades de escala de dados de acordo com as configurações que são suportadas pelo seu fornecedor de hardware. À medida que aumenta o número de unidades de escala de dados, você precisa adicionar Rack adicional & componentes de rede, conforme necessário, para fornecer mais energia, rede e infraestrutura do rack.  
  
### <a name="data-host"></a>Host de dados  

Um host de dados é um servidor dedicado ao processamento de dados de usuário. Parallel Data Warehouse (PDW) executa um nó de computação em cada host de dados. Para dispositivos de HPE, a unidade de escala de dados tem dois hosts de dados. Para dispositivos Dell e Quanta, a unidade de escala de dados tem três hosts de dados.  
  
### <a name="direct-attached-storage"></a>Armazenamento anexado direto
 
O armazenamento com conexão direta (DAS) é um pool de discos conectados aos hosts de dados. Todos os hosts de dados podem acessar qualquer um dos discos. Como parte do nada compartilhado arquitetura, os nós de computação em execução em hosts de dados não compartilha discos individuais. No entanto, para alta disponibilidade, o acesso ao armazenamento compartilhado e cada um dos hosts de dados pode acessar qualquer um dos discos.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Escala unidade arquitetura de dados - DELL e Quanta
  
![Unidade de escalabilidade](media/scalability-unit-dell.png "unidade Dell escalabilidade")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Arquitetura de unidade de escala de dados - HPE 
 
![Unidade de escalabilidade HPE](media/scalability-unit-hpe.png "unidade HPE escalabilidade")  
  
### <a name="data-scale-unit-description"></a>Descrição de unidade de escala de dados

Uma unidade de escala de dados tem um servidor (host) para cada nó de computação e a matriz de um disco de conexão direta que é anexado com SCSI SAS (Serial Attached). Dentro do gabinete de armazenamento, a matriz de disco é dividida em duas metades que têm fontes de alimentação redundantes. Espaços de armazenamento do Windows Server gerencia os dados de usuário, duplicação de dados entre pares de disco espelhado RAID 1. Os discos em cada par de disco são armazenados em diferentes partes da matriz de disco.  
  
A matriz de disco também contém discos de espera ativa e um disco do sistema. Se um disco falhar, os espaços de armazenamento usa boa cópia dos dados no disco está funcionando para recriar uma cópia dos dados em um sobressalente ativo. Este é um recurso importante de auto-reparo que ajuda a proteger contra perda de dados.  
  
O número total de discos para os nós de computação:  
  
-   DELL tem 96 discos = (3 servidores) * (16 discos por servidor) \* (2 para discos redundantes).  
  
-   HPE tem 64 discos = (2 servidores) * (16 discos por servidor) \* (2 para discos redundantes).  
  
-   Além disso, cada matriz de disco tem um disco de sistema e discos de espera ativa.  
  
**Para alta disponibilidade**, quando uma nó de failover de computação pode ainda funcionam e acessar os dados do usuário através do host na unidade de escala de dados. Pelo menos um dos hosts físicos conectados diretos deve estar funcionando ou acesso a dados para o armazenamento é perdido.  
  
**Para tamanhos de disco**, o armazenamento anexado direto pode ter 1, 2 ou 3 unidades de disco Terabyte. Todas as unidades de escala de dados devem ter os discos do mesmo tamanho.  
  
## <a name="basescaleunit"></a>Unidade base de escala 
 
A unidade de escala de Base contém o número mínimo de energia cérebro hosts, hosts de dados e armazenamento com conexão direta que é necessário para o dispositivo. Ele inclui os seguintes componentes.  
  
### <a name="orchestration-host"></a>host de orquestração  
Este servidor é executado o cérebro do PDW.
  
### <a name="passive-host"></a>host passivo  
Esse servidor oferece alta disponibilidade. Ele está online e pronto para executar trabalhos, caso haja uma falha na orquestração ou host de dados. O host de orquestração, host passivo e servidores de unidade de escala de dados são configurados como um cluster de failover do Windows. Cada rack em que o dispositivo requer um host de passivo.  
  
### <a name="optional-passive-host"></a>host passivo opcional  
Para adicionar mais redundância, você tem a opção de adicionar um segundo host passivo para a unidade de escala de Base.  
  
### <a name="data-scale-unit"></a>Unidade de escala de dados  
A unidade de escala de Base inclui uma unidade de escala de dados que é colocada na parte inferior do rack.  
  
Este diagrama mostra a unidade de escala de Base mais o Rack e a rede. Essa é a configuração mínima para um dispositivo de sistema de plataforma de análise.  
  
![Unidade de escala base](media/base-scale-unit.png "unidade de escala de Base")  
 
