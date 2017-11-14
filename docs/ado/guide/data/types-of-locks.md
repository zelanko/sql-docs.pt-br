---
title: Tipos de bloqueios | Microsoft Docs
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
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41c06eb813c41c26cc2e96ed1f32b159f0b58362
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-locks"></a>Tipos de bloqueios
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 Indica as atualizações em lotes otimista. Necessário para o modo de atualização em lotes.  
  
 Muitos aplicativos buscar um número de linhas de uma vez e, em seguida, precisam verificar as atualizações de coordenadas que incluem todo o conjunto de linhas a serem inseridas, atualizadas ou excluídas. Com cursores de lote, apenas uma resposta para o servidor for necessária, que melhora o desempenho de atualização e reduz o tráfego de rede. Usando uma biblioteca de cursores em lotes, você pode criar um cursor estático e, em seguida, desconecte a fonte de dados. Agora você pode fazer alterações em linhas e subsequentemente reconectar e postar as alterações para a fonte de dados em um lote.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 Indica se o provedor usa bloqueio otimista — bloqueando registros somente quando você chamar o **atualização** método. Isso significa que há uma possibilidade de que outro usuário pode alterar os dados entre o momento em que você editar o registro e quando você chama **atualização**, que cria conflitos. Use esse tipo de bloqueio em situações nas quais as chances de uma colisão serão baixas ou onde colisões podem ser resolvidas imediatamente.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 Indica o bloqueio pessimista, registro por registro. O provedor não o que é necessário para garantir a edição bem-sucedida dos registros, normalmente por um bloqueio de registros na fonte de dados imediatamente antes de editar. Obviamente, isso significa que os registros não estão disponíveis para outros usuários depois que você começar a editar, até que você libere o bloqueio chamando **atualização.** Use este tipo de bloqueio em um sistema onde você não pode ter alterações simultâneas a dados, como em um sistema de reserva.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 Indica os registros de somente leitura. Você não pode alterar os dados. Um bloqueio de somente leitura é "rápido" tipo de bloqueio, porque ele não exigir que o servidor para manter um bloqueio em registros.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 Não especifique um tipo de bloqueio.

