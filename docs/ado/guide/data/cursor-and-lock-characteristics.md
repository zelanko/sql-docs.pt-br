---
title: Características de bloqueio e de cursor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3a206a21cf7c6680a656c89c48b8f52d1069d78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702120"
---
# <a name="cursor-and-lock-characteristics"></a>Características de cursor e de bloqueio
Embora as características de um cursor dependem de recursos do provedor, as seguintes vantagens e desvantagens geralmente se aplicam a vários tipos de cursores e bloqueios.  
  
|Tipo de cursor ou de bloqueio|Vantagens|Desvantagens|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Requisitos de recursos baixa|-Não é possível rolar para trás<br />-Simultaneidade sem dados|  
|**adOpenStatic**|-Rolável|-Simultaneidade sem dados|  
|**adOpenKeyset**|-Simultaneidade alguns dados<br />-Rolável|-Mais altos requisitos de recursos<br />-Não disponível no cenário desconectado|  
|**adOpenDynamic**|– Simultaneidade de dados alta<br />-Rolável|-Mais altos requisitos de recursos<br />-Não disponível no cenário desconectado|  
|**adLockReadOnly**|-Requisitos de recursos baixa<br />-Altamente escalonável|-Data não é atualizável pelo cursor|  
|**adLockBatchOptimistic**|-Lote atualizações<br />-Permite cenários desconectados<br />-Outros usuários possam acessar dados|-Dados podem ser alterados por vários usuários ao mesmo tempo|  
|**adLockPessimistic**|-Data não pode ser alterado por outros usuários enquanto bloqueado|-Impede que outros usuários acessem dados enquanto estiver bloqueado|  
|**adLockOptimistic**|-Outros usuários possam acessar dados|-Dados podem ser alterados por vários usuários ao mesmo tempo|
