---
title: Instalação de hardware - Analytics Platform System | Microsoft Docs
description: Este artigo descreve como mover, descompacte e instale o hardware de seu dispositivo de PDW do SQL Server. Este artigo é apenas informativo e se destina a ajudá-lo a entender o processo. Seu dispositivo deve ser desembalado, instalado e verificado antes que ele é transformado em você. A participação do cliente é necessária para os itens, como dados de acesso, energia elétrica e conexões Ethernet center.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c864a560bb37d27a5bb8ef306ac66815e8b5149c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960874"
---
# <a name="hardware-installation-for-analytics-platform-system-appliance"></a>Instalação do hardware de dispositivo do Analytics Platform System
Este artigo descreve como mover, descompacte e instale o hardware de seu dispositivo de PDW do SQL Server. Este artigo é apenas informativo e se destina a ajudá-lo a entender o processo. Seu dispositivo deve ser desembalado, instalado e verificado antes que ele é transformado em você. A participação do cliente é necessária para os itens, como dados de acesso, energia elétrica e conexões Ethernet center.  
  
## <a name="BeforeMoving"></a>Antes de mover todos os componentes da plataforma de carga  
Execute as seguintes tarefas antes de mover, descompactar ou qualquer um dos componentes do dispositivo em rack.  
  
|Tarefa|Descrição|  
|--------|---------------|  
|Verifique se que todos os componentes chegaram|Use a lista de materiais (BOM) para verificar se todos os componentes chegaram e estão em suas paletes na plataforma de recebimento para seu data center.|  
|Verifique se o data center atende a todos os requisitos para o dispositivo|Inicie esta tarefa revisando as especificações de hardware e cabeamento diagramas fornecendo ao IHV. As próximas etapas fornecem informações específicas sobre rack requisitos de conectividade e espaço.|  
|Verifique se o data center tem espaço em rack adequado|Verifique se o data center tem espaço suficiente para todos os racks de dispositivo.<br /><br />Verifique se o espaço em rack está vazia e pronto para receber os racks de dispositivo.|  
|Verificar se o data center atende aos requisitos de conectividade|Verifique se o data center atende os requisitos de cabeamento nos diagramas de cabeamento.<br /><br />Verifique se que haja espaço para todos os cabos e cabos de alimentação depois que os nós de dispositivo são montados em rack.|  
|Verificar se os andares entre encaixe e racks atendem aos requisitos de peso|Verifique se que piso todos entre os paletes e racks pode suportar o peso de nós do dispositivo, especialmente em data centers com piso elevado.<br /><br />Entre em contato com seu IHV para obter informações sobre o peso de cada componente.|  
|Proteger o data center rack|Proteger o data center rack no local usando equipamentos adicionais conforme necessário para seu local de centro de dados, como pulseiras terremoto em áreas geográficas propensas a terremotos.|  
|Preparar para obter assistência com transportando os componentes|Determine antecipadamente que tipo de Ajuda, equipamento e ferramentas que você precisará lidar com cada componente e com segurança sem causar danos.|  
  
## <a name="Moving"></a>Mover os Racks de plataforma de carga para o Data Center  
Cada palete contém todos os componentes de rack de um dispositivo, incluindo nós, cabos, cabos, etc.  
  
Use a lista de verificação a seguir para mover cada rack de dispositivo do palete na plataforma de carga para seu local de rack no data center. Mover o rack controle primeiro e, em seguida, mover os outros racks de dados do dispositivo.  
  
> [!WARNING]  
> Falha ao executar essas etapas exatamente como descrito pode resultar em danos físicos, danos ao seu dispositivo de PDW do SQL Server ou outros problemas.  
>   
> Nunca tentar de comparação de precisão ou mover um nó de dispositivo ou outro componente pesado sem assistência ou equipamento adequado. Entre em contato com seu IHV para obter informações sobre o peso de cada componente para que você possa determinar antecipadamente que tipo de Ajuda, equipamento e ferramentas que você precisará lidar com cada componente e com segurança sem causar danos.  
  
|Tarefa|Descrição|  
|--------|---------------|  
|Verifique se o palete é nível|Antes de começar a mover ou desempacote o palete, certifique-se de que ele está em nível zero.|  
|Unbolt um nó do palete|Começando na parte superior do palete, unbolt o nó superior do palete.|  
|Mover o nó a um carrinho de mão ou um carrinho de compras que pode suportar o peso|Use Rampas e técnicas adequadas levantando/mover para mover o nó a um carrinho de mão ou um carrinho de compras que pode suportar o peso.|  
|O nó de transporte no Centro de dados|Use técnicas adequadas levantando/mover para mover o nó para a posição no data center rack.|  
|Proteger o nó no data center rack|Proteger o nó em vigor no data center em rack.|  
|Repita essas etapas para o próximo nó ou componente|Repita essas etapas para mover o próximo nó ou outro componente de dispositivo para o data center.|  
  
## <a name="AfterMoving"></a>Instalar componentes adicionais  
Use a seguinte lista de verificação para instalar os componentes adicionais.  
  
|Tarefa|Descrição||  
|--------|---------------|-|  
|Descompactar e comutadores de rede e PDUs em rack|Use os diagramas de rack para colocar os comutadores de rede e as PDUs no local apropriado no rack.||  
|Conecte os cabos Infiniband e Ethernet de acordo com os rótulos de cabo|Consulte o diagrama de fiação. Cada cabo tem um rótulo em cada extremidade que especifica em que ele precisa ser conectado.||  
|Conecte todos os cabos de alimentação|Consulte o diagrama de fiação.||  
|Ativar a fonte de energia aos racks e PDUs|Conecte-se a fonte de energia aos racks e de racks para PDUs. **Não liga qualquer um dos outros componentes do dispositivo no momento.**||  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
