---
title: Validar guias de plano depois da atualização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3f3f8fd278d1141417adec4f1ef6a1faced386c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151209"
---
# <a name="validate-plan-guides-after-upgrade"></a>Validar guias de plano depois da atualização
  Recomendamos que as definições do guia de plano sejam reavaliadas e testadas quando o aplicativo for atualizado para uma nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os requisitos de ajuste de desempenho e o comportamento da correlação do guia de plano podem variar. Embora um guia inválido não cause a falha da consulta, o plano é compilado sem usar o guia de plano e pode não ser a melhor escolha. Depois de atualizar o banco de dados para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], nós recomendamos que as seguintes tarefas sejam executadas:  
  
-   Valide os guias de plano por meio da função [sys.fn_validate_plan_guide](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql) .  
  
-   Use eventos estendidos para monitorar os planos mal-encaminhados por algum tempo usando o evento [Plan Guide Unsuccessful](../event-classes/plan-guide-unsuccessful-event-class.md) .  
  
  
