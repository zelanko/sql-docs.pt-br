---
title: Definir comando de reprocessamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a7eb5fd19ca538c4f25077926567011ae133e54
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300826"
---
# <a name="set-reprocess-command"></a>Comando SET REPROCESS
Especifica quantas vezes ou por quanto tempo bloquear um arquivo ou registro após uma tentativa de bloqueio sem êxito.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>Argumentos  
 PARA *nAttempts*[segundos]  
 Especifica o número de vezes ou o número de segundos para tentar bloquear um registro ou arquivo após uma tentativa de falha inicial. O valor padrão é 0; o valor máximo é 32.000.  
  
 SEGUNDOS especifica que o Visual FoxPro tenta bloquear um arquivo ou registro por *nAttempts* segundos. Ele está disponível somente quando *nAttempts* é maior que zero.  
  
 Por exemplo, se *nAttempts* for 30, o Visual FoxPro tentará bloquear um registro ou um arquivo até 30 vezes. Se você também incluir segundos (definir o reprocessamento para 30 segundos), o Visual FoxPro tentará, continuamente, bloquear um registro ou um arquivo por até 30 segundos.  
  
 Se uma rotina ON ERROR estiver em vigor e se as tentativas por um comando para bloquear o registro ou o arquivo não forem bem-sucedidas, a rotina ON ERROR será executada. No entanto, se uma função tentar o bloqueio, uma rotina ON ERROR não será executada e a função retornará false (. F.).  
  
 Se uma rotina ON ERROR não estiver em vigor, um comando tentará bloquear o registro ou o arquivo, e o bloqueio não poderá ser colocado, um erro será gerado. Se uma função tentar posicionar o bloqueio, o alerta não será exibido e a função retornará false (. F.).  
  
 Se *nAttempts* for 0 (o valor padrão) e você emitir um comando ou função que tente bloquear um registro ou arquivo, o Visual FoxPro tentará bloquear o registro ou o arquivo indefinidamente. Se o registro ou o arquivo ficar disponível para bloqueio enquanto você aguarda, o bloqueio é colocado e a mensagem do sistema é apagada. Se uma função tentar posicionar o bloqueio, a função retornará true (. T.).  
  
 Se uma rotina ON ERROR estiver em vigor e um comando estiver tentando bloquear o registro ou o arquivo, a rotina ON ERROR terá precedência sobre tentativas adicionais de bloquear o registro ou o arquivo. A rotina ON ERROR é executada imediatamente. O Visual FoxPro não tenta registro adicional ou bloqueios de arquivo e não exibe a mensagem do sistema.  
  
 Se *nAttempts* for 1, o Visual FoxPro tentará bloquear o registro ou o arquivo indefinidamente e uma rotina On Error não será executada.  
  
 Se um bloqueio tiver sido colocado por outro usuário no registro ou arquivo que você está tentando bloquear, você deverá aguardar até que o usuário libere o bloqueio.  
  
 PARA AUTOMÁTICO  
 Especifica que o Visual FoxPro tenta bloquear o registro ou o arquivo indefinidamente. (SET Reprocess TO-2 é um comando equivalente.)  
  
## <a name="remarks"></a>Comentários  
 A primeira tentativa de bloquear um registro ou arquivo nem sempre é bem-sucedida. Frequentemente, um registro ou arquivo é bloqueado por outro usuário na rede. DEFINIR o reprocessamento determina se o Visual FoxPro faz tentativas adicionais de bloquear o registro ou o arquivo quando a tentativa inicial não for bem-sucedida. Você pode especificar quantas vezes tentativas adicionais são feitas ou por quanto tempo as tentativas são feitas. Uma rotina ON ERROR afeta a forma como as tentativas de bloqueio malsucedidas são tratadas.
