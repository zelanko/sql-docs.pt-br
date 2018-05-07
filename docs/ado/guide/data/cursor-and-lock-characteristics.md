---
title: Cursor e características de bloqueio | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5350ff2f01fe8ea3d515026f198e4ad27e28eb50
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="cursor-and-lock-characteristics"></a>Cursor e características de bloqueio
Enquanto as características de um cursor dependem dos recursos do provedor, as seguintes vantagens e desvantagens geralmente se aplicam a vários tipos de cursores e bloqueios.  
  
|Tipo de cursor ou bloqueio|Vantagens|Desvantagens|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Requisitos de recursos baixa|-Não é possível rolar para trás<br />-Nenhuma simultaneidade de dados|  
|**adOpenStatic**|-Rolável|-Nenhuma simultaneidade de dados|  
|**adOpenKeyset**|-Alguns simultaneidade de dados<br />-Rolável|-Mais altos requisitos de recursos<br />-Não disponível no cenário desconectado|  
|**adOpenDynamic**|-Simultaneidade de dados alta<br />-Rolável|-Mais altos requisitos de recursos<br />-Não disponível no cenário desconectado|  
|**adLockReadOnly**|-Requisitos de recursos baixa<br />-Altamente escalonável|-Data não pode ser atualizada por meio do cursor|  
|**adLockBatchOptimistic**|-Atualizações em lotes<br />-Permite cenários desconectados<br />-Outros usuários acessem dados|-Dados podem ser alterados por vários usuários ao mesmo tempo|  
|**adLockPessimistic**|-Data não pode ser alterado por outros usuários enquanto bloqueado|-Impede que outros usuários acessem dados enquanto bloqueado|  
|**adLockOptimistic**|-Outros usuários acessem dados|-Dados podem ser alterados por vários usuários ao mesmo tempo|
