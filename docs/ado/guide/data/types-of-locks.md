---
title: Tipos de bloqueios | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b66b87b0c741bf943cc2558862a0e1853c386b5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510729"
---
# <a name="types-of-locks"></a>Tipos de bloqueios
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 Indica as atualizações em lotes otimista. Necessário para o modo de atualização em lotes.  
  
 Muitos aplicativos buscar um número de linhas de uma vez e, em seguida, precisam fazer atualizações coordenadas que incluem todo o conjunto de linhas a serem inseridos, atualizados ou excluídos. Com cursores de lote, apenas um round trip para o servidor é necessária, melhorando o desempenho de atualização e diminuindo o tráfego de rede. Usando uma biblioteca de cursores em lotes, você pode criar um cursor estático e, em seguida, se desconectar da fonte de dados. Neste ponto você pode fazer alterações em linhas e, subsequentemente, reconectar-se e postar as alterações à fonte de dados em um lote.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 Indica que o provedor usa bloqueio otimista: bloqueando registros somente quando você chama o **atualização** método. Isso significa que há uma chance de que outro usuário pode alterar os dados entre o momento em que você editar o registro e quando você chama **atualização**, que cria conflitos. Usar esse tipo de bloqueio em situações em que as chances de uma colisão de baixa ou colisões em que podem ser resolvidas prontamente.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 Indica o bloqueio pessimista, registro por registro. O provedor faz o que é necessário para garantir que a edição bem-sucedida dos registros, geralmente por um bloqueio de registros na fonte de dados imediatamente antes de editar. Obviamente, isso significa que os registros não estão disponíveis para outros usuários depois que você começa a editar, até que você libere o bloqueio chamando **atualização.** Use esse tipo de bloqueio em um sistema onde você não pode ter alterações simultâneas aos dados, como em um sistema de reserva.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 Indica os registros de somente leitura. Você não pode alterar os dados. Um bloqueio somente leitura é o tipo "rápido" de bloqueio, porque ele não requer o servidor para manter um bloqueio de registros.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 Não especifica um tipo de bloqueio.
