---
title: Partições remotas | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 328008dd8c7500bb8a798edaee83f893f7d5bd05
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="partitions---remote-partitions"></a>Partições - partições remotas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Os dados de uma partição remota são armazenados em uma instância diferente do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que a instância que contém as definições (metadados) da partição e seu cubo pai. Uma partição remota é gerenciada na mesma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] onde a partição e seu cubo pai são definidos.  
  
> [!NOTE]  
>  Para armazenar uma partição remota, o computador deve ter uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instalado e estar executando o mesmo nível de service pack da instância em que a partição foi definida. As partições remotas em instâncias de uma versão anterior do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não oferecem suporte.  
  
 Quando as partições remotas são incluídas em um grupo de medidas, a memória e a utilização da CPU do cubo são distribuídas ao longo das partições nesse grupo de medidas. Por exemplo, quando uma partição remota é processada, sozinha ou como parte do processamento de um cubo pai, a maior parte da utilização da memória e da CPU para a partição ocorre na instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Um cubo que contém partições remotas pode conter dimensões habilitadas para gravação; porém, isso pode afetar o desempenho do cubo. Para obter mais informações sobre dimensões habilitadas para gravação, consulte [Write-Enabled dimensões](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="storage-modes-for-remote-partitions"></a>Modos de armazenamento para partições remotas  
 As partições remotas podem usar qualquer dos tipos de armazenamento usados por partições locais: OLAP multidimensional (MOLAP), OLAP híbrido (HOLAP) ou OLAP relacional (ROLAP). As partições remotas também podem usar cache pró-ativo. Dependendo do modo de armazenamento de uma partição remota, os dados a seguir são armazenados na instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|||  
|-|-|  
|Tipo de armazenamento|data|  
|MOLAP|As agregações da partição e uma cópia dos dados de origem da partição|  
|HOLAP|As agregações das partições|  
|ROLAP|Nenhum dado da partição|  
  
 Se o grupo de medidas contiver várias partições MOLAP ou HOLAP armazenadas em várias instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o cubo distribui os dados nos dados do grupo de medidas entre as instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="merging-remote-partitions"></a>Mesclando partições remotas  
 As partições remotas podem ser mescladas somente com outras partições remotas armazenadas na mesma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obter mais informações sobre a mesclagem de partições, consulte [mesclar partições no Analysis Services &#40;SSAS - Multidimensional&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
## <a name="archiving-and-restoring-remote-partitions"></a>Arquivando e restaurando partições remotas  
 Os dados em partições remotas podem ser arquivados ou restaurados quando o banco de dados que armazena a partição remota for arquivado ou restaurado. Se você restaurar um banco de dados sem restaurar uma partição remota, você deve processar a partição remota antes de usar os dados na partição. Para obter mais informações sobre arquivamento e restauração de bancos de dados, consulte [Backup e restauração do Analysis Services Databases](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar e gerenciar uma partição remota & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [Processamento do Analysis Services objetos](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)  
  
  
