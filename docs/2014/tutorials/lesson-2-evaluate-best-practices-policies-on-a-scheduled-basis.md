---
title: 'Lição 2: avaliar as políticas de práticas recomendadas em uma base agendada | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 37ffad63-d6db-4609-8deb-786200659554
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9bbd1ffb75402e475e5d55a9661967be2fcd57c0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063954"
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
  
## <a name="see-also"></a>Consulte Também  
 [Administrar vários servidores usando os Servidores Centrais de Gerenciamento](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
