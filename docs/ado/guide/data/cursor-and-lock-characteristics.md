---
title: "Cursor e características de bloqueio | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a1313c42582efee8330abb89a03645dc1491217
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

