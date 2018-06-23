---
title: Alterações recentes em gerenciamento de recursos das ferramentas do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 33e204958f9cea2db092f2a9c4b7d20648e4182c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019877"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>Alterações de quebra feitas em recursos das Ferramentas de Gerenciamento do SQL Server 2014
  Este tópico descreve alterações de quebra feitas em recursos das ferramentas de gerenciamento. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Talvez você tenha esses problemas ao atualizar. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
## <a name="breaking-changes-in-includesssql14includessssql14-mdmd"></a>Últimas alterações do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Informações que virão posteriormente.  
  
## <a name="breaking-changes-in-includesssql11includessssql11-mdmd"></a>Últimas alterações do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="you-cannot-use-includesssql11includessssql11-mdmd-management-tools-to-create-a-utility-control-point-on-a-includesskilimanjaroincludessskilimanjaro-mdmd-instance-of-sql-server"></a>Você não pode usar as Ferramentas de Gerenciamento do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] para criar um ponto de controle de utilitário em uma instância do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] do SQL Server  
 Para criar um ponto de controle de utilitário em uma instância do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]use as Ferramentas de Gerenciamento do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] .  
  
### <a name="smo-has-been-reversioned-in-includesssql11includessssql11-mdmd"></a>O SMO foi revertido no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 O código desenvolvido com o SMO do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] ou de versões anteriores talvez não seja criado no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] sem pequenas modificações. Para obter mais informações, consulte [Backward Compatibility in SMO](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md).  
  
## <a name="see-also"></a>Consulte também  
 [Compatibilidade com versões anteriores](../../2014/getting-started/backward-compatibility.md)  
  
  