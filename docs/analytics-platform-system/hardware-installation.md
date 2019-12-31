---
title: Instalação do hardware
description: Este artigo descreve como mover, desempacotar e instalar o hardware para seu dispositivo de SQL Server PDW. Este artigo é apenas informativo e destina-se a ajudá-lo a entender o processo. Seu dispositivo deve ser desempacotado, instalado e verificado antes de ser ativado para você. A participação do cliente é necessária para itens como acesso data center, energia elétrica e conexões Ethernet.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 60e27e2251cd2f613ca00266d76d4aaaf3b5c442
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401121"
---
# <a name="hardware-installation-for-analytics-platform-system-aps-appliance"></a>Instalação de hardware para o dispositivo do Analytics Platform System (APS)
Este artigo descreve como mover, desempacotar e instalar o hardware para seu dispositivo de SQL Server PDW. Este artigo é apenas informativo e destina-se a ajudá-lo a entender o processo. Seu dispositivo deve ser desempacotado, instalado e verificado antes de ser ativado para você. A participação do cliente é necessária para itens como acesso data center, energia elétrica e conexões Ethernet.  
  
## <a name="BeforeMoving"></a>Antes de mover qualquer componente do encaixe de carregamento  
Execute as seguintes tarefas antes de mover, descompactar ou colocar em rack qualquer um dos componentes do dispositivo.  
  
|Tarefa|Descrição|  
|--------|---------------|  
|Verificar se todos os componentes chegaram|Use a BOM (lista de materiais) para verificar se todos os componentes chegaram e estão em seus paletes no encaixe de recebimento para seu data center.|  
|Verifique se o data center atende a todos os requisitos do dispositivo|Inicie essa tarefa examinando as especificações de hardware e os diagramas de cabeamento fornecidos por seu IHV. As próximas etapas fornecem informações específicas sobre os requisitos de conectividade e espaço do rack.|  
|Verifique se o data center tem espaço em rack adequado|Verifique se o data center tem espaço suficiente para todos os racks de dispositivo.<br /><br />Verifique se o espaço do rack está vazio e pronto para receber os racks do dispositivo.|  
|Verificar se o data center atende aos requisitos de conectividade|Verifique se o data center atende aos requisitos de cabeamento nos diagramas de cabeamento.<br /><br />Verifique se haverá espaço para todos os cabos e cabo de alimentação depois que os nós do dispositivo forem montados em rack.|  
|Verifique se os andares entre o Dock e os racks atendem aos requisitos de peso|Verifique se todos os piso entre os paletes e os racks podem dar suporte ao peso dos nós de dispositivo, especialmente em data centers com andares elevados.<br /><br />Entre em contato com seu IHV para obter informações sobre o peso de cada componente.|  
|Proteger o rack de data center|Proteja o rack de data center em vigor usando equipamentos adicionais conforme necessário para seu local de data center, como pulseiras de terremoto em áreas geográficas sujeitas a terremotos.|  
|Preparar para obter assistência com o transporte dos componentes|Determine com antecedência qual é a assistência, o equipamento e as ferramentas necessárias para lidar com cada componente de forma segura e sem causar danos.|  
  
## <a name="Moving"></a>Mover os racks do encaixe de carregamento para o Data Center  
Cada palete contém todos os componentes para um rack de dispositivo, incluindo nós, cabos, fios, etc.  
  
Use a lista de verificação a seguir para mover cada rack de dispositivo do palete no encaixe de carregamento para o local do seu rack na data center. Mova o rack de controle primeiro e, em seguida, mova os outros racks de dados do dispositivo.  
  
> [!WARNING]  
> A falha em executar essas etapas exatamente conforme descrito pode resultar em danos bodilys, dano ao seu dispositivo SQL Server PDW ou outros problemas.  
>   
> Nunca tente levantar ou mover um nó de dispositivo ou outro componente pesado sem assistência ou equipamento adequado. Entre em contato com seu IHV para obter informações sobre o peso de cada componente para que você possa determinar com antecedência qual assistência, equipamento e ferramentas será necessário para lidar com cada componente com segurança e sem causar danos.  
  
|Tarefa|Descrição|  
|--------|---------------|  
|Verifique se o palete é nível|Antes de começar a mover ou descompactar o palete, verifique se ele está no nível de base.|  
|Desparafuso de um nó do palete|Começando na parte superior do palete, deslado o nó superior do palete.|  
|Mova o nó para um Dolly ou carrinho que possa dar suporte ao peso|Use rampas e técnicas de elevação/movimentação adequadas para mover o nó para um Dolly ou carrinho que possa dar suporte ao peso.|  
|Transportar o nó para o data center|Use técnicas de elevação/movimentação adequadas para mover o nó para a posição no rack de data center.|  
|Proteger o nó no rack de data center|Proteja o nó em vigor no data center rack.|  
|Repita essas etapas para o próximo nó ou componente|Repita essas etapas para mover o próximo nó ou outro componente de dispositivo para o data center.|  
  
## <a name="AfterMoving"></a>Instalar componentes adicionais  
Use a lista de verificação a seguir para instalar os componentes adicionais.  
  
|Tarefa|Descrição||  
|--------|---------------|-|  
|Opções e PDUs de rede de rack e desempacotamento|Use os diagramas de rack para colocar os comutadores de rede e a PDUs no local correto do rack.||  
|Conecte os cabos InfiniBand e Ethernet de acordo com os rótulos de cabo|Consulte o diagrama de cabeamento. Cada cabo tem um rótulo em cada extremidade que especifica onde ele precisa ser conectado.||  
|Conectar todos os cabos de alimentação|Consulte o diagrama de cabeamento.||  
|Ligue a fonte de alimentação aos racks e à PDUs|Conecte a fonte de alimentação aos racks e dos racks à PDUs. **Não ligue nenhum dos outros componentes do dispositivo no momento.**||  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
