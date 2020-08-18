---
description: MSSQLSERVER_1205
title: MSSQLSERVER_1205 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d45f2095a679c8549ebbb42852ab6e2316596852
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88336132"
---
# <a name="mssqlserver_1205"></a>MSSQLSERVER_1205
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|1205|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LK_VICTIM|  
|Texto da mensagem|A transação (ID do processo %d) entrou em deadlock em %.*ls recursos com outro processo e foi escolhida como a vítima do deadlock. Execute a transação novamente.|  
  
## <a name="explanation"></a>Explicação  
Os recursos podem ser acessados em ordem conflitante em transações separadas, causando um deadlock. Por exemplo:  
  
-   Transaction1 atualiza **Table1.Row1**, enquanto Transaction2 atualiza **Table2.Row2**.  
  
-   Transaction1 tenta atualizar **Table2.Row2**, mas é bloqueada, porque Transaction2 ainda não foi confirmada.  
  
-   Transaction2 agora tenta atualizar **Table1.Row1**, mas é bloqueada porque Transaction1 ainda não foi confirmada.  
  
-   Um deadlock acontece porque a Transação1 está esperando a conclusão da Transação2, mas a Transação2 está esperando a conclusão da Transação1.  
  
O sistema detecta o deadlock, escolhe uma das transações envolvidas como 'vítima' e emite a mensagem, revertendo a transação da vítima.  
  
## <a name="user-action"></a>Ação do usuário  
Execute a transação novamente. Você também pode revisar o aplicativo para evitar deadlocks. A transação escolhida como vítima pode ser testada novamente e, provavelmente, terá êxito, dependendo de quais operações estiverem sendo executadas simultaneamente.  
  
Para impedir ou evitar a ocorrência de deadlocks, faça com que todas as transações acessem as linhas na mesma ordem (**Table1** e, depois, **Table2**); desse modo, embora possa acontecer um bloqueio, não ocorrerá um deadlock.  
  
