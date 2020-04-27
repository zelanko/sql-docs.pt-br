---
title: Partições remotas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- archiving remote partitions [Analysis Services]
- partitions [Analysis Services], remote
- restoring remote partitions [Analysis Services]
- backing up remote partitions [Analysis Services]
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- MasterDataSourceID property
- remote partitions [Analysis Services]
ms.assetid: 63f5d9f5-c6b6-4ceb-94fe-7b6c396d10bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d092c33c8c350dc19b749fd3b31ccf1b8c73eac6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727307"
---
# <a name="remote-partitions"></a>Partições remotas
  Os dados de uma partição remota são armazenados em uma instância diferente da Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do que a instância do que contém as definições (metadados) da partição e seu cubo pai. Uma partição remota é gerenciada na mesma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] onde a partição e seu cubo pai são definidos.  
  
> [!NOTE]  
>  Para armazenar uma partição remota, o computador deve ter uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instalada e estar executando o mesmo nível de Service Pack que a instância em que a partição foi definida. As partições remotas em instâncias de uma versão anterior do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não oferecem suporte.  
  
 Quando as partições remotas são incluídas em um grupo de medidas, a memória e a utilização da CPU do cubo são distribuídas ao longo das partições nesse grupo de medidas. Por exemplo, quando uma partição remota é processada, sozinha ou como parte do processamento de um cubo pai, a maior parte da utilização da memória e da CPU para a partição ocorre na instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Um cubo que contém partições remotas pode conter dimensões habilitadas para gravação; porém, isso pode afetar o desempenho do cubo. Para obter mais informações sobre dimensões habilitadas para gravação, consulte [dimensões habilitadas para gravação](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="storage-modes-for-remote-partitions"></a>Modos de armazenamento para partições remotas  
 As partições remotas podem usar qualquer dos tipos de armazenamento usados por partições locais: OLAP multidimensional (MOLAP), OLAP híbrido (HOLAP) ou OLAP relacional (ROLAP). As partições remotas também podem usar cache pró-ativo. Dependendo do modo de armazenamento de uma partição remota, os dados a seguir são armazenados na instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|||  
|-|-|  
|Tipo de armazenamento|Dados|  
|MOLAP|As agregações da partição e uma cópia dos dados de origem da partição|  
|HOLAP|As agregações das partições|  
|ROLAP|Nenhum dado da partição|  
  
 Se o grupo de medidas contiver várias partições MOLAP ou HOLAP armazenadas em várias instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o cubo distribui os dados nos dados do grupo de medidas entre as instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="merging-remote-partitions"></a>Mesclando partições remotas  
 As partições remotas podem ser mescladas somente com outras partições remotas armazenadas na mesma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações sobre como mesclar partições, consulte [mesclar partições em Analysis Services &#40;SSAS-&#41;multidimensional ](../multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
## <a name="archiving-and-restoring-remote-partitions"></a>Arquivando e restaurando partições remotas  
 Os dados em partições remotas podem ser arquivados ou restaurados quando o banco de dados que armazena a partição remota for arquivado ou restaurado. Se você restaurar um banco de dados sem restaurar uma partição remota, você deve processar a partição remota antes de usar os dados na partição. Para obter mais informações sobre arquivamento e restauração de bancos de dados, consulte [backup e restauração de bancos de dados Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar e gerenciar uma partição remota &#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [Processando objetos do Analysis Services](../multidimensional-models/processing-analysis-services-objects.md)  
  
  
