---
title: Características de cursor e Lock | Microsoft Docs
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
ms.openlocfilehash: c4d6f86539e1abc7ee74087b130e0186322346e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925672"
---
# <a name="cursor-and-lock-characteristics"></a>Características de cursor e de bloqueio
Embora as características de um cursor dependam dos recursos do provedor, as vantagens e desvantagens a seguir geralmente se aplicam aos vários tipos de cursores e bloqueios.  
  
|Cursor ou tipo de bloqueio|Vantagens|Desvantagens|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Requisitos de recursos baixos|-Não é possível rolar para trás<br />-Sem simultaneidade de dados|  
|**adOpenStatic**|-Rolável|-Sem simultaneidade de dados|  
|**adOpenKeyset**|-Certa simultaneidade de dados<br />-Rolável|-Requisitos de recursos mais altos<br />-Não disponível no cenário desconectado|  
|**adOpenDynamic**|-Simultaneidade de dados alta<br />-Rolável|-Requisitos de recursos mais altos<br />-Não disponível no cenário desconectado|  
|**adLockReadOnly**|-Requisitos de recursos baixos<br />-Altamente escalonável|-Dados não atualizáveis por meio do cursor|  
|**adLockBatchOptimistic**|-Atualizações do lote<br />– Permite cenários desconectados<br />-Outros usuários podem acessar dados|-Os dados podem ser alterados por vários usuários ao mesmo tempo|  
|**adLockPessimistic**|-Os dados não podem ser alterados por outros usuários enquanto estiverem bloqueados|-Impede que outros usuários acessem dados enquanto estiverem bloqueados|  
|**adLockOptimistic**|-Outros usuários podem acessar dados|-Os dados podem ser alterados por vários usuários ao mesmo tempo|
