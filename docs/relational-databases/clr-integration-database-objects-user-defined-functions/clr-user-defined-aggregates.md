---
title: Agregações CLR definidas pelo usuário | Microsoft Docs
description: SQL Server integração CLR permite que você crie funções de agregação personalizadas em código gerenciado, que executam um cálculo em um conjunto de valores e retornam um valor.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
author: rothja
ms.author: jroth
ms.openlocfilehash: 9267e1e1e0b051dbbd8581b694aafacd2e5ce8a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488269"
---
# <a name="clr-user-defined-aggregates"></a>Agregações CLR definidas pelo usuário
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Funções agregadas executam um cálculo em um conjunto de valores e retornam um único valor. Tradicionalmente, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece supoute somente a funções de agregação internas, como **SUM** ou **MAX**, que operam em um conjunto de valores escalares de entrada e geram um único valor de agregação a partir desse conjunto A integração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o CLR (common language runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework agora permite que os desenvolvedores criem funções de agregação personalizadas no código gerenciado e tornem essas funções acessíveis ao [!INCLUDE[tsql](../../includes/tsql-md.md)] ou a outro código gerenciado.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Requisitos para agregações CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 Fornece uma visão geral dos requisitos para implementar as funções de agregação definida pelo usuário CLR.  
  
 [Invocando funções de agregação CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 Explica como invocar agregações definidas pelo usuário.  
  
  
