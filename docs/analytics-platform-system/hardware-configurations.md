---
title: "Configurações de hardware (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "O hardware Analytics Platform System (APS) foi projetado com unidades escalonáveis, para que você comprar a quantidade certa de processamento e armazenamento de acordo com seus requisitos de negócios."
ms.date: 01/05/2017
ms.topic: article
ms.assetid: f95945b7-97ae-4ab9-bae5-c792a516acea
caps.latest.revision: "9"
ms.openlocfilehash: 1a98d1f853b293eb417182868ee1cb67cf328f53
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="hardware-configurations"></a>Configurações de hardware
O hardware Analytics Platform System (APS) foi projetado com unidades escalonáveis, para que você comprar a quantidade certa de processamento e armazenamento de acordo com seus requisitos de negócios. O dispositivo pode ser dimensionado armazenamento para SQL Server Parallel Data Wareouse (PDW) de alguns Terabytes até Petabytes em 6 de dados.  
  
## <a name="contents"></a>Sumário  
  
-   [Configurações de um Rack](#section1)  
  
-   [Configurações de vários racks](#section2)  

  
## <a name="section1"></a>Configurações de um Rack  
O rack primeiro o dispositivo contém os componentes necessários para executar o PDW. A configuração mínima do dispositivo é uma unidade de escala de Base e de rede além de um Rack. Esses diagramas mostram maneiras que pode ser configurado primeiro rack do dispositivo. Você pode ter entre 2 e 9 nós de computação no primeiro rack, dependendo do fornecedor do hardware.  
  
### <a name="first-rack-configurations---dell"></a>Primeiro Rack configurações - DELL  
A configuração mínima para um dispositivo DELL tem 3 nós de computação. Você pode adicionar até 2 unidades de escala de dados para o primeiro rack para um total de nós de computação 9.  
  
![Configurações do primeiro rack Dell](media/first-rack-configurations-dell.png "configurações do primeiro rack Dell")  
  
### <a name="first-rack-configurations---hpe"></a>Primeiro Rack configurações - HPE  
A configuração mínima para um dispositivo HPE tem 2 nós de computação. Você pode adicionar até 3 unidades de escala de dados para o primeiro rack para um total de 8 nós de computação.  
  
![HPE primeiro rack configurações para HPE](media/first-rack-configurations-hpe.png "HPE primeiro as configurações de rack")  
  
## <a name="section2"></a>Configurações de vários racks  
Para adicionar capacidade ao PDW adicionar unidades de escala de dados, juntamente com componentes de rede & Rack adicionais conforme necessário para fornecer a potência adequada, rede e infraestrutura do rack. Cada rede & Rack adicional requer um host de passivo.  
  
Cada fornecedor de hardware Especifica o número de unidades de escala de dados que você pode adicionar recebe a capacidade do seu dispositivo. É recomendável adicionar suficiente unidades de escala de dados para ver pelo menos um upgrade de 20 por cento no desempenho. Por exemplo, a unidade em um dispositivo que já tem 20 unidades de escala de dados adicionando uma escala de dados pode resultar em um ganho de desempenho muito importantes. O ganho da rede não seria vale a pena o custo e o esforço.  
  
### <a name="scale-out-example---hpe"></a>Expansão de exemplo - HPE  
Este diagrama mostra um dispositivo de 3 rack HP com 20 nós de computação.  
  
![Dispositivo HPE com 20 nós de computação](media/scale-out-hpe.png "dispositivo HPE com 20 nós de computação")  
  
### <a name="scale-out-example--dell-quanta"></a>Exemplo – DELL, Quanta em expansão  
Este diagrama mostra um dispositivo de 3 rack DELL ou Quanta que contém nós de computação 21.  
  
![Dispositivo Dell conosco de computação 21](media/scale-out-dell.png "dispositivo Dell com 21 nós de computação")  
 
