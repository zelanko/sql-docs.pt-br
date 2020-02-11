---
title: Armazenamento do gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e1eab3ad745a83a8a55545570e020c1f1af732ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62628885"
---
# <a name="policy-based-management-storage"></a>Armazenamento do Gerenciamento Baseado em Políticas
  As políticas são armazenadas no banco de dados msdb. Após a alteração de uma política ou condição, deve ser feito backup do msdb. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="storing-policies"></a>Armazenando políticas  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui políticas que podem ser usadas para monitorar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, essas políticas não são instaladas no [!INCLUDE[ssDE](../../includes/ssde-md.md)]; no entanto, eles podem ser importados do local de instalação padrão de C:\Arquivos de programas (x86) \Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033.  
  
 Você pode criar políticas diretamente usando o menu **Arquivo/Novo** e salvá-las em um arquivo. Isso permite criar políticas quando você não estiver conectado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 O histórico de políticas avaliadas na instância atual do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é mantido em tabelas do sistema de msdb. O histórico de políticas aplicadas a outras instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou aplicadas ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não é retido.  
  
  
