---
title: Falhas inesperadas do sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 84fe7ae204c14a0ecaebb3141d4f08175bfee793
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727269"
---
# <a name="unexpected-system-failures"></a>Falhas inesperadas do sistema
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra verifica o SYSTEM Event 6008 no log de eventos do computador. Esse evento indica um desligamento do sistema inesperado. O sistema pode estar instável e não fornecer a estabilidade e a integridade necessárias para hospedar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Resolva imediatamente a causa dos reinícios inesperados do servidor ou move a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outro computador.  
  
  
