---
title: Validar guias de plano depois da atualização | Microsoft Docs
description: Quando você atualiza seu aplicativo para uma nova versão do SQL Server, recomendamos que reavalie e teste as definições do guia de plano.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: bb7b3981c76e5bf8059d13afc74f3181d4b60cea
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86456802"
---
# <a name="validate-plan-guides-after-upgrade"></a>Validar guias de plano depois da atualização
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Recomendamos que as definições do guia de plano sejam reavaliadas e testadas quando o aplicativo for atualizado para uma nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os requisitos de ajuste de desempenho e o comportamento da correlação do guia de plano podem variar. Embora um guia inválido não cause a falha da consulta, o plano é compilado sem usar o guia de plano e pode não ser a melhor escolha. Depois de atualizar o banco de dados para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], nós recomendamos que as seguintes tarefas sejam executadas:  
  
-   Valide os guias de plano por meio da função [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md) .  
  
-   Use eventos estendidos para monitorar os planos mal-encaminhados por algum tempo usando o evento [Plan Guide Unsuccessful](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md) .  
  
  
