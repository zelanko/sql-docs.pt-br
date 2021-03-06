---
description: Tipos de bloqueios
title: Tipos de bloqueios | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
author: rothja
ms.author: jroth
ms.openlocfilehash: 55087e96c0855f24153dee9bc279d9abf58d3f04
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979257"
---
# <a name="types-of-locks"></a>Tipos de bloqueios
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 Indica atualizações de lote otimistas. Necessário para o modo de atualização do lote.  
  
 Muitos aplicativos buscam um número de linhas de uma vez e precisam fazer atualizações coordenadas que incluem todo o conjunto de linhas a serem inseridas, atualizadas ou excluídas. Com cursores de lote, apenas uma viagem de ida e volta para o servidor é necessária, melhorando assim o desempenho da atualização e diminuindo o tráfego de rede. Usando uma biblioteca de cursores do lote, você pode criar um cursor estático e, em seguida, desconectar-se da fonte de dados. Neste ponto, você pode fazer alterações nas linhas e, subsequentemente, reconectar e postar as alterações na fonte de dados em um lote.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 Indica que o provedor usa registros de bloqueio de bloqueio otimista somente quando você chama o método **Update** . Isso significa que há uma chance de que outro usuário possa alterar os dados entre a hora em que você editar o registro e ao chamar **Update**, que cria conflitos. Use esse tipo de bloqueio em situações em que as chances de uma colisão sejam baixas ou onde as colisões possam ser prontamente resolvidas.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 Indica o bloqueio pessimista, registro por registro. O provedor faz o que é necessário para garantir a edição bem-sucedida dos registros, geralmente bloqueando os registros na fonte de dados imediatamente antes da edição. É claro que isso significa que os registros não estão disponíveis para outros usuários depois que você começa a editar, até que você libere o bloqueio chamando **Update.** Use esse tipo de bloqueio em um sistema no qual não é possível ter as alterações simultâneas nos dados, como em um sistema de reserva.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 Indica registros somente leitura. Você não pode alterar os dados. Um bloqueio somente leitura é o tipo "mais rápido" de bloqueio porque ele não requer que o servidor mantenha um bloqueio nos registros.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 Não especifica um tipo de bloqueio.
