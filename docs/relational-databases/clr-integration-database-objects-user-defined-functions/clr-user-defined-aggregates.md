---
title: Agregações CLR definidas pelo usuário | Microsoft Docs
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
ms.openlocfilehash: 2e654e1e14aa09e5414a100e6d06c64eba93dab7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68009803"
---
# <a name="clr-user-defined-aggregates"></a>Agregações CLR definidas pelo usuário
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Funções agregadas executam um cálculo em um conjunto de valores e retornam um único valor. Tradicionalmente, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece supoute somente a funções de agregação internas, como **SUM** ou **MAX**, que operam em um conjunto de valores escalares de entrada e geram um único valor de agregação a partir desse conjunto A integração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o CLR (common language runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework agora permite que os desenvolvedores criem funções de agregação personalizadas no código gerenciado e tornem essas funções acessíveis ao [!INCLUDE[tsql](../../includes/tsql-md.md)] ou a outro código gerenciado.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Requisitos para agregações CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 Fornece uma visão geral dos requisitos para implementar as funções de agregação definida pelo usuário CLR.  
  
 [Invocando funções de agregação CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 Explica como invocar agregações definidas pelo usuário.  
  
  
