---
title: "Instalação do hardware (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f612b9-f320-4391-952b-d3696cfbe2e2
caps.latest.revision: "17"
ms.openlocfilehash: ea0935ed3af9dcea187098e39df2d0219f98fd7a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="hardware-installation"></a>Instalação do hardware
Este tópico descreve como mover, descompacte e instalar o hardware de seu dispositivo de PDW do SQL Server. Este tópico é apenas informativo e destina-se para ajudá-lo a entender o processo. Seu dispositivo deve ser descompactado, instalado e verificado antes que ela é transformada para você. A participação do cliente é necessária para itens como dados center acesso, energia elétrica e conexões Ethernet.  
  
## <a name="BeforeMoving"></a>Antes de mover todos os componentes de plataforma de carga  
Execute as seguintes tarefas antes de mover, descompactar ou qualquer um dos componentes do dispositivo em rack.  
  
|Tarefa|Description|  
|--------|---------------|  
|Verifique se que todos os componentes foram recebidos|Use a lista de materiais (BOM) para verificar se todos os componentes foram recebidos e estão em suas paletes no recebimento encaixe para seu data center.|  
|Verifique se o data center atende todos os requisitos para o dispositivo|Tarefa iniciada por revisar as especificações de hardware e o cabeamento diagramas fornecendo por seu IHVS. As próximas etapas fornecem informações específicas sobre rack requisitos de espaço e conectividade.|  
|Verifique se o data center tem espaço adequado de rack|Verifique se o data center tem espaço suficiente para todos os racks de dispositivo.<br /><br />Verifique se o espaço no rack está vazio e pronto para receber os racks de dispositivo.|  
|Verificar se o data center atende aos requisitos de conectividade|Verifique se o data center atende os requisitos de cabeamento nos diagramas de cabeamento.<br /><br />Verifique se que haja espaço para todos os cabos e os cabos de alimentação depois que os nós de dispositivo são montados em rack.|  
|Verificar se o pisos entre os racks e de encaixe atendem aos requisitos de peso|Verifique se todos os pisos entre os paletes e os racks podem suportam o peso de nós do dispositivo, especialmente em data centers com piso elevado.<br /><br />Entre em contato com seu IHVS para obter informações sobre o peso de cada componente.|  
|Proteger o data center rack|Proteger o data center rack usando equipamentos adicionais conforme necessário para seu local de centro de dados, como pulseiras terremoto em áreas geográficas propensas a terremotos.|  
|Preparar para obter assistência com transportando os componentes|Determine antecipadamente quais assistência, equipamento e ferramentas que você precisa lidar com cada componente com segurança e sem causar danos.|  
  
## <a name="Moving"></a>Mover os Racks de plataforma de carga para o Data Center  
Cada paleta contém todos os componentes de rack de um dispositivo, incluindo nós, cabos, cabos, etc.  
  
Use a lista de verificação a seguir para mover cada rack de dispositivo da paleta na plataforma de carga para seu local de rack no data center. Primeiro mova o rack de controle e, em seguida, mover os outros racks de dados do dispositivo.  
  
> [!WARNING]  
> Falha ao executar essas etapas exatamente conforme descrito pode resultar em danos físicos, danos ao seu dispositivo de PDW do SQL Server ou outros problemas.  
>   
> Nunca tentar levantar ou mover um nó de dispositivo ou de outro componente pesada sem assistência ou equipamento necessário. Entre em contato com seu IHVS para obter informações sobre o peso de cada componente para que você possa determinar antecipadamente que tipo de Ajuda, equipamento e ferramentas que você precisará lidar com cada componente com segurança e sem causar danos.  
  
|Tarefa|Description|  
|--------|---------------|  
|Verifique se a paleta é um nível|Antes de começar a mover ou descompactar a paleta, certifique-se de que ele está no início de nível.|  
|Unbolt um nó a partir de paleta|Iniciando na parte superior da paleta, unbolt o nó superior da paleta.|  
|Mover o nó a um carrinho de mão ou carrinho que pode suportar o peso|Usar Rampas e técnicas de levantar/movimentação apropriadas para mover o nó a um carrinho de mão ou carrinho que pode suportar o peso.|  
|O nó de transporte para o Centro de dados|Use técnicas de levantar/movimentação apropriadas para mover o nó para a posição do rack de centro de dados.|  
|Proteger o nó no data center rack|Proteger o nó no local no data center em rack.|  
|Repita essas etapas para o próximo nó ou componente|Repita essas etapas para mover o próximo nó ou outro componente do dispositivo para o data center.|  
  
## <a name="AfterMoving"></a>Instalar componentes adicionais  
Use a seguinte lista de verificação para instalar os componentes adicionais.  
  
|Tarefa|Description||  
|--------|---------------|-|  
|Desempacotar e comutadores de rede e PDUs de rack|Use os diagramas de rack para colocar os comutadores de rede e PDUs no local apropriado no rack.||  
|Conecte os cabos Infiniband e Ethernet de acordo com os rótulos de cabo|Consulte o diagrama de cabeamento. Cada cabo tem um rótulo em cada extremidade que especifica onde ele precisa ser conectado.||  
|Conecte todos os cabos de alimentação|Consulte o diagrama de cabeamento.||  
|Ativar a fonte de energia para os racks e PDUs|Conecte-se a fonte de alimentação dos racks e racks de PDUs. **Não liga qualquer um dos outros componentes do dispositivo no momento.**||  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
