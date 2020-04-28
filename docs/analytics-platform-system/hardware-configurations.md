---
title: Configuração de hardware
description: O hardware do dispositivo do sistema de plataforma de análise (APS) é arquitetado com unidades escalonáveis para que você compre a quantidade certa de processamento e armazenamento de acordo com seus requisitos de negócios. O dispositivo dimensiona o armazenamento para data warehouse paralelo de alguns terabytes a mais de 6 petabytes de dados.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee16045931da345f06c141597ccd25d19a36dea7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401130"
---
# <a name="hardware-configurations---analytics-platform-system"></a>Configurações de hardware – Analytics Platform System
O hardware do sistema de plataforma de análise (APS) é arquitetado com unidades escalonáveis para que você compre a quantidade certa de processamento e armazenamento de acordo com seus requisitos de negócios. O dispositivo dimensiona o armazenamento para SQL Server PDW (Parallel Data Wareouse) de alguns terabytes a mais de 6 petabytes de dados.  
  
## <a name="contents"></a>Conteúdo  
  
-   [Configurações de um rack](#section1)  
  
-   [Configurações de vários racks](#section2)  

  
## <a name="one-rack-configurations"></a><a name="section1"></a>Configurações de um rack  
O primeiro rack do dispositivo contém os componentes necessários para executar o PDW. A configuração mínima do dispositivo é um rack e uma rede, além de uma unidade de escala de base. Esses diagramas mostram maneiras que o primeiro rack do dispositivo pode ser configurado. Você pode ter entre 2 e 9 nós de computação no primeiro rack, dependendo do fornecedor do hardware.  
  
### <a name="first-rack-configurations---dell"></a>Primeiras configurações de rack-DELL  
A configuração mínima para um dispositivo DELL tem 3 nós de computação. Você pode adicionar até 2 unidades de escala de dados ao primeiro rack para um total de 9 nós de computação.  
  
![Configurações do primeiro rack da Dell](media/first-rack-configurations-dell.png "Configurações do primeiro rack da Dell")  
  
### <a name="first-rack-configurations---hpe"></a>Primeiras configurações de rack-HPE  
A configuração mínima para um dispositivo HPE tem 2 nós de computação. Você pode adicionar até três unidades de escala de dados ao primeiro rack para um total de 8 nós de computação.  
  
![Configurações do primeiro rack do HPE para HPE](media/first-rack-configurations-hpe.png "Configurações do primeiro rack do HPE")  
  
## <a name="multi-rack-configurations"></a><a name="section2"></a>Configurações de vários racks  
Para adicionar capacidade ao PDW, você pode adicionar unidades de escala de dados, juntamente com o rack adicional & componentes de rede, conforme necessário, para fornecer a energia, a rede e a infraestrutura de rack apropriadas. Cada rack adicional & rede requer um host passivo.  
  
Cada fornecedor de hardware especifica o número de unidades de escala de dados que você pode adicionar, dada a capacidade de seu dispositivo. É recomendável adicionar unidades de escala de dados suficientes para ver pelo menos um upgrade de 20% no desempenho. Por exemplo, a adição de uma unidade de escala de dados a um dispositivo que já tem 20 unidades de escala de dados pode resultar em um lucro de desempenho insignificante. O lucro líquido não valeria o custo e o esforço.  
  
### <a name="scale-out-example---hpe"></a>Exemplo de scale out – HPE  
Este diagrama mostra um dispositivo HP de 3 rack que contém 20 nós de computação.  
  
![Dispositivo HPE com 20 nós de computação](media/scale-out-hpe.png "Dispositivo HPE com 20 nós de computação")  
  
### <a name="scale-out-example---dell-quanta"></a>Exemplo de Scale Out – DELL, Quantity  
Este diagrama mostra um dispositivo DELL ou quanta de três racks que contém 21 nós de computação.  
  
![Dispositivo Dell com 21 nós de computação](media/scale-out-dell.png "Dispositivo Dell com 21 nós de computação")  
 
