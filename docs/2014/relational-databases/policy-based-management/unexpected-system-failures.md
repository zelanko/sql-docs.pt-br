---
title: Falhas inesperadas do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58ccdb66ad026f2a27594f58ea091c2cf0888e15
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37318336"
---
# <a name="unexpected-system-failures"></a>Falhas inesperadas do sistema
  Esta regra verifica o SYSTEM Event 6008 no log de eventos do computador. Esse evento indica um desligamento do sistema inesperado. O sistema pode estar instável e não fornecer a estabilidade e a integridade necessárias para hospedar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Resolva imediatamente a causa dos reinícios inesperados do servidor ou move a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outro computador.  
  
  
