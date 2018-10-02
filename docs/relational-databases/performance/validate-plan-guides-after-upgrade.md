---
title: Validar guias de plano depois da atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43c7297f490c913663c8d08f62cabb7a21cca86d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636935"
---
# <a name="validate-plan-guides-after-upgrade"></a>Validar guias de plano depois da atualização
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Recomendamos que as definições do guia de plano sejam reavaliadas e testadas quando o aplicativo for atualizado para uma nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os requisitos de ajuste de desempenho e o comportamento da correlação do guia de plano podem variar. Embora um guia inválido não cause a falha da consulta, o plano é compilado sem usar o guia de plano e pode não ser a melhor escolha. Depois de atualizar o banco de dados para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], nós recomendamos que as seguintes tarefas sejam executadas:  
  
-   Valide os guias de plano por meio da função [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md) .  
  
-   Use eventos estendidos para monitorar os planos mal-encaminhados por algum tempo usando o evento [Plan Guide Unsuccessful](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md) .  
  
  
