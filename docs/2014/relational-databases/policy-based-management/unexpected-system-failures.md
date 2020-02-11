---
title: Falhas inesperadas do sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 951b49c0356ae27cb58041af5186becfd12853bb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62677063"
---
# <a name="unexpected-system-failures"></a>Falhas inesperadas do sistema
  Esta regra verifica o SYSTEM Event 6008 no log de eventos do computador. Esse evento indica um desligamento do sistema inesperado. O sistema pode estar instável e não fornecer a estabilidade e a integridade necessárias para hospedar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Resolva imediatamente a causa dos reinícios inesperados do servidor ou move a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outro computador.  
  
  
