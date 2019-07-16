---
title: Componentes de hardware - Analytics Platform System | Microsoft Docs
description: Analytics Platform System (APS) usa componentes escalonáveis, de modo que você pode comprar a quantidade certa de armazenamento e processamento de acordo com suas necessidades de negócios. Ao solicitar pontos de acesso, você precisará de uma combinação desses componentes de hardware de núcleo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0f7f3bd8f4d5500a59675d40ff7f50d1afd9a199
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960884"
---
# <a name="hardware-components-for-analytics-platform-system"></a>Componentes de hardware para o Analytics Platform System

Analytics Platform System (APS) usa componentes escalonáveis, de modo que você pode comprar a quantidade certa de armazenamento e processamento de acordo com suas necessidades de negócios. Ao solicitar pontos de acesso, você precisará de uma combinação desses componentes de hardware de núcleo. Fornecedores de hardware específicos podem usar as convenções de nomenclatura diferentes ou ter componentes adicionais.  
 
  
## <a name="rackandnetwork"></a>Rack e rede 
 
Componentes APS são armazenados em um ou mais racks que se encaixam em seu data center. Cada rack vem com dois switches Ethernet, dois comutadores InfiniBand e unidades de distribuição de alimentação (PDUs).  
  
![Rede e rack](media/rack-and-network.png "APS em rack e de rede")  
  
## <a name="datascaleunit"></a>Unidade de escala de dados
 
Uma unidade de escala de dados contém os hosts de dados e o armazenamento anexado (direto) para processar e armazenar dados de usuário. Para adicionar capacidade você adicionar unidades de escala de dados de acordo com as configurações que são compatíveis com o fornecedor do hardware. À medida que cresce o número de unidades de escala de dados, você precisará adicionar o Rack adicional e componentes de rede, conforme necessário, para fornecer mais energia, rede e infraestrutura em rack.  
  
### <a name="data-host"></a>Host de dados  

Um host de dados é um servidor dedicado ao processamento de dados de usuário. Parallel Data Warehouse (PDW) executa um nó de computação em cada host de dados. Para dispositivos de HPE, a unidade de escala de dados tem dois hosts de dados. Para dispositivos de Dell e Quanta, a unidade de escala de dados tem três hosts de dados.  
  
### <a name="direct-attached-storage"></a>Armazenamento com conexão direta
 
O armazenamento com conexão direta (DAS) é um pool de discos conectados aos hosts de dados. Todos os hosts de dados podem acessar qualquer um dos discos. Como parte de compartilhar nada arquitetura, os nós de computação em execução nos hosts de dados não compartilha discos individuais. No entanto, para alta disponibilidade, o acesso de armazenamento é compartilhado e cada um dos hosts de dados pode acessar qualquer um dos discos.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Escala de unidade arquitetura de dados - DELL e Quanta
  
![Unidade de escalabilidade](media/scalability-unit-dell.png "unidade de escalabilidade da Dell")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Arquitetura de unidade de escala de dados - HPE 
 
![Unidade de escalabilidade HPE](media/scalability-unit-hpe.png "unidade HPE escalabilidade")  
  
### <a name="data-scale-unit-description"></a>Descrição de unidade de escala de dados

Uma unidade de escala de dados tem um servidor (host) para cada nó de computação e a matriz de um disco conectado diretamente anexado com SAS Serial Attached SCSI (). Dentro do gabinete do armazenamento, a matriz de disco é dividida em duas metades, que têm fontes de alimentação redundantes. Espaços de armazenamento do Windows Server gerencia dados de usuário, a duplicação de dados entre pares de disco espelhado RAID 1. Os discos em cada par de disco são armazenados em diferentes metades da matriz de disco.  
  
A matriz de disco também contém discos de espera ativa e um disco do sistema. Se um disco falhar, os espaços de armazenamento usa boa cópia dos dados no disco está funcionando para recriar uma cópia duplicada dos dados em um sobressalente ativo. Isso é um recurso de auto-recuperação importante que ajuda a proteger contra perda de dados.  
  
O número total de discos para os nós de computação:  
  
-   A DELL tem 96 discos = (3 servidores) * (16 discos por servidor) \* (2 para discos redundantes).  
  
-   HPE tem 64 discos = (2 servidores) * (16 discos por servidor) \* (2 para discos redundantes).  
  
-   Além disso, cada matriz de disco tem discos de espera ativa e um disco do sistema.  
  
**Para alta disponibilidade**, quando um nó de computação faz failover, ele pode ainda funcionam e acessar seus dados de usuário por meio do host na unidade de escala de dados. Pelo menos um dos hosts físicos conectados diretos deve estar funcionando ou acesso a dados para o armazenamento é perdido.  
  
**Para tamanhos de disco**, o armazenamento com conexão direta pode ter 1, 2 ou 3 unidades de disco de terabytes. Todas as unidades de escala de dados devem ter os discos do mesmo tamanho.  
  
## <a name="basescaleunit"></a>Unidade de escala de base 
 
A unidade de escala de Base contém o número mínimo de dupla personalidade power hosts, hosts de dados e armazenamento com conexão direta que é necessário para o dispositivo. Ele inclui os seguintes componentes. 
  
### <a name="orchestration-host"></a>Host de orquestração  
Este servidor executa o cérebro do PDW.
  
### <a name="passive-host"></a>Host passivo  
Esse servidor oferece alta disponibilidade. Ele está online e pronto para executar trabalhos, caso haja uma falha na orquestração ou host de dados. O host de orquestração, host passivo e servidores de unidade de escala de dados são configurados como um cluster de failover do Windows. Cada rack no dispositivo requer um host passivo.  
  
### <a name="optional-passive-host"></a>Host passivo opcional  
Para adicionar ainda mais redundância, você tem a opção de adicionar um segundo host passivo para a unidade de escala de Base.  
  
### <a name="data-scale-unit"></a>Unidade de escala de dados  
A unidade de escala de Base inclui uma unidade de escala de dados que é colocada na parte inferior do rack.  
  
Este diagrama mostra a unidade de escala de Base mais o Rack e a rede. Essa é a configuração mínima para um dispositivo do Analytics Platform System.  
  
![Unidade de escala de base](media/base-scale-unit.png "unidade de escala de Base")  
 
