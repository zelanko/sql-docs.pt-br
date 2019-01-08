---
title: As configurações de hardware - Analytics Platform System | Microsoft Docs
description: O hardware de dispositivo do Analytics Platform System (APS) foi projetado com unidades escalonáveis, de modo que você compra a quantidade certa de armazenamento e processamento de acordo com suas necessidades de negócios. O dispositivo dimensiona o armazenamento para o Parallel Data Warehouse de alguns terabytes até 6 petabytes de dados.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2a252e5f2aebd8d51b9b0eb1f353ded504155c2e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507942"
---
# <a name="hardware-configurations---analytics-platform-system"></a>Configurações de hardware - Analytics Platform System
O hardware do Analytics Platform System (APS) foi projetado com unidades escalonáveis, de modo que você compra a quantidade certa de armazenamento e processamento de acordo com suas necessidades de negócios. O dispositivo de escala para SQL Server Parallel Data Wareouse (PDW) de alguns Terabytes até 6 Petabytes de dados de armazenamento.  
  
## <a name="contents"></a>Sumário  
  
-   [Configurações de um Rack](#section1)  
  
-   [Configurações de vários racks](#section2)  

  
## <a name="section1"></a>Configurações de um Rack  
O primeiro rack o dispositivo contém os componentes necessários para executar o PDW. A configuração mínima do dispositivo é uma unidade de escala de Base e de rede além de um Rack. Esses diagramas mostram maneiras que pode ser configurado primeiro rack do dispositivo. Você pode ter entre 2 e 9 nós de computação no primeiro rack, dependendo do fornecedor de hardware.  
  
### <a name="first-rack-configurations---dell"></a>Primeiro Rack configurações - DELL  
A configuração mínima para um dispositivo DELL tem 3 nós de computação. Você pode adicionar até 2 unidades de escala de dados do primeiro rack para um total de 9 nós de computação.  
  
![Configurações do primeiro rack Dell](media/first-rack-configurations-dell.png "configurações do primeiro rack Dell")  
  
### <a name="first-rack-configurations---hpe"></a>Configurações - HPE pela primeira vez em Rack  
A configuração mínima para um dispositivo HPE tem 2 nós de computação. Você pode adicionar até 3 unidades de escala de dados do primeiro rack para um total de 8 nós de computação.  
  
![HPE primeiro rack configurações para o HPE](media/first-rack-configurations-hpe.png "HPE primeiro rack configurações")  
  
## <a name="section2"></a>Configurações de vários racks  
Para adicionar capacidade ao PDW, você pode adicionar unidades de escala de dados, juntamente com componentes de rede & Rack adicionais conforme necessário para fornecer a capacidade adequada, rede e infraestrutura em rack. Cada rede & Rack adicional requer um host passivo.  
  
Cada fornecedor de hardware Especifica o número de unidades de escala de dados que você pode adicionar recebe a capacidade do seu dispositivo. É recomendável adicionar suficiente unidades de escala de dados para ver pelo menos um upgrade de 20 por cento em desempenho. Por exemplo, a unidade em um dispositivo que já tenha 20 unidades de escala de dados adicionando uma escala de dados pode resultar em um ganho de desempenho. O ganho líquido seria que vale a pena o custo e esforço.  
  
### <a name="scale-out-example---hpe"></a>Escalar horizontalmente exemplo - HPE  
Este diagrama mostra um dispositivo de 3 rack HP que contém 20 nós de computação.  
  
![Dispositivo HPE com 20 nós de computação](media/scale-out-hpe.png "appliance HPE com 20 nós de computação")  
  
### <a name="scale-out-example---dell-quanta"></a>Exemplo – DELL, Quanta de expansão  
Este diagrama mostra um dispositivo de 3 rack DELL ou Quanta que contém nós de computação 21.  
  
![Dispositivo Dell conosco de computação 21](media/scale-out-dell.png "appliance Dell conosco de computação 21")  
 
