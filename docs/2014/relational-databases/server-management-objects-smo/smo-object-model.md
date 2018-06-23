---
title: Modelo de objeto SMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], object model
- SQL Server Management Objects, object model
ms.assetid: bd6e59b6-ca46-42c0-adb2-c9d64cf6e00b
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bbaf5430252c296313723509b0195cdf5573ced5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008855"
---
# <a name="smo-object-model"></a>Modelo de objeto SMO
  O modelo de objeto SMO é composto de uma hierarquia de objetos. O objeto <xref:Microsoft.SqlServer.Management.Smo.Server> é o objeto de nível superior e todos os objetos de classe de instância residem sob o objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
 A classe <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> é uma classe de nível superior com uma hierarquia de objetos separada. O <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> objeto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviços e configurações de rede disponíveis por meio do provedor de WMI.  
  
 Além dos objetos <xref:Microsoft.SqlServer.Management.Smo.Server> e <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>, há várias classes de utilitário que representam tarefas ou operações, como <xref:Microsoft.SqlServer.Management.Smo.Transfer>, <xref:Microsoft.SqlServer.Management.Smo.Backup> ou <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
 O modelo de objeto SMO é composto de vários namespaces. Para obter mais informações, consulte o [Namespaces do SMO](smo-object-model-namespaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [Diagrama de modelo de objeto do SMO](smo-object-model-diagram.md)   
 [Namespaces do SMO](smo-object-model-namespaces.md)   
 [Provedor WMI para conceitos de gerenciamento de configuração](../wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  