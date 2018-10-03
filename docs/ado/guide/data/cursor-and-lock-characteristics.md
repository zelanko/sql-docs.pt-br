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
manager: craigg
ms.openlocfilehash: a8507be55ae84a3a03fd75871106bc39e0631d89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678424"
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
