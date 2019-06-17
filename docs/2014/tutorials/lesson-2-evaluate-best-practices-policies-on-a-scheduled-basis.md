---
title: 'Lição 2: Avaliar as políticas de práticas recomendadas de forma programada | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 37ffad63-d6db-4609-8deb-786200659554
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 29513ec37a946b9ec613ccc483048396149dd15a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042591"
---
# <a name="lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis"></a>Lição 2: Avaliar políticas de melhores práticas de forma agendada
  Você pode configurar avaliações agendadas de políticas de práticas recomendadas em uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para configurar políticas de práticas recomendadas para executarem de forma agendada, você deve importar as políticas na instância de destino.  
  
 Para implantar políticas agendadas em vários servidores, você pode importar as políticas para uma instância, configurar as agendas para cada política, exportar as políticas agendadas para uma pasta e, em seguida, implantar as políticas agendadas em instâncias de destino por meio de Servidores Registrados.  
  
> [!IMPORTANT]  
>  As instâncias de destino devem ser executadas no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] ou em uma versão posterior. A automação exige que as políticas sejam armazenadas localmente na instância, o que não tem suporte em versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
 Nesta lição, você fará o seguinte:  
  
-   Importe as políticas de práticas recomendadas em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Configure as políticas para serem executadas em um agendamento.  
  
-   Implantar as políticas agendadas de práticas recomendadas em múltiplas instâncias por meio de Servidores Registrados.  
  
 Eis os tópicos desta lição:  
  
-   [Importar as políticas para uma única instância](../../2014/tutorials/import-the-policies-to-a-single-instance.md)  
  
-   [Agendar as políticas](../../2014/tutorials/schedule-the-policies.md)  
  
-   [Implantar diretivas agendadas em várias instâncias](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
## <a name="see-also"></a>Consulte também  
 [Administrar vários servidores usando os Servidores Centrais de Gerenciamento](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
