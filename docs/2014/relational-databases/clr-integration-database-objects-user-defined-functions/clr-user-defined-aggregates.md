---
title: Agregações CLR definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dd22a27772c7bcad2d3c98027dbc91d6d6859509
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008666"
---
# <a name="clr-user-defined-aggregates"></a>Agregações CLR definidas pelo usuário
  As funções de agregação executam um cálculo em um conjunto de valores e retornam um único valor. Tradicionalmente, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem suporte somente funções de agregação internas, como `SUM` ou `MAX`, que operam em um conjunto de valores escalares de entrada e gerar um único valor de agregação de conjunto. A integração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o CLR (common language runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework agora permite que os desenvolvedores criem funções de agregação personalizadas no código gerenciado e tornem essas funções acessíveis ao [!INCLUDE[tsql](../../includes/tsql-md.md)] ou a outro código gerenciado.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Requisitos para agregações CLR definidas pelo usuário](clr-user-defined-aggregates-requirements.md)  
 Fornece uma visão geral dos requisitos para implementar as funções de agregação definida pelo usuário CLR.  
  
 [Invocando funções de agregação CLR definidas pelo usuário](clr-user-defined-aggregate-invoking-functions.md)  
 Explica como invocar agregações definidas pelo usuário.  
  
  