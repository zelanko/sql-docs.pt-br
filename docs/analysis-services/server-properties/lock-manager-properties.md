---
title: Propriedades do Gerenciador de bloqueio do Analysis Services | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a5383fe83963a9b388413b9b829b4fac7fc11788
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071583"
---
# <a name="lock-manager-properties"></a>Propriedades do gerenciador de bloqueio
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor do gerenciador de bloqueio, listadas na tabela a seguir. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** Modo de servidor multidimensional e Tabular  
  
## <a name="properties"></a>Propriedades  
 **DefaultLockTimeoutMS**  
 Uma propriedade de inteiro de 32 bits assinada que define o tempo limite de bloqueio padrão em milissegundos para solicitações de bloqueio internas.  
  
 O valor padrão para essa propriedade é -1, o que indica que não há nenhum tempo limite para solicitações de bloqueio interno.  
  
 **LockWaitGranularityMS**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DeadlockDetectionGranularityMS**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do servidor no Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
