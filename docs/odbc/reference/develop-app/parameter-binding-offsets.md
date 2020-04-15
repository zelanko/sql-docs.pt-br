---
title: Deslocamentos de vinculação de parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de67b230883f3cf8a582e73ce82e8c4bd7d21ad0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282477"
---
# <a name="parameter-binding-offsets"></a>Deslocamentos de associação de parâmetro
Um aplicativo pode especificar que uma compensação é adicionada aos endereços de buffer de parâmetros vinculados e aos endereços de buffer de comprimento/indicador correspondentes quando **SQLExecDirect** ou **SQLExecute** é chamado. O resultado dessas adições determina os endereços utilizados nessas operações.  
  
 As compensações de vinculação permitem que um aplicativo altere as vinculações sem chamar **sqlBindParameter** para parâmetros vinculados anteriormente. Uma chamada para **SQLBindParameter** para revincular um parâmetro altera o endereço buffer e o ponteiro comprimento/indicador. A revinculação com um deslocamento, por outro lado, simplesmente adiciona uma compensação ao endereço de buffer de parâmetro situado e ao endereço de buffer de comprimento/indicador existente. Quando as compensações são usadas, as vinculações são um "modelo" de como os buffers do aplicativo são definidos e o aplicativo pode mover esse "modelo" para diferentes áreas de memória alterando o deslocamento. Um novo deslocamento pode ser especificado a qualquer momento e é sempre adicionado aos valores originalmente vinculados.  
  
 Para especificar uma compensação de vinculação, o aplicativo define o atributo de declaração SQL_ATTR_PARAM_BIND_OFFSET_PTR para o endereço de um buffer SQLINTEGER. Antes que o aplicativo chame uma função que usa as vinculações, ele coloca uma compensação em bytes neste buffer, desde que nem o endereço buffer de parâmetro nem o endereço de buffer de comprimento/indicador seja 0, e o parâmetro vinculado esteja na declaração SQL. A soma do endereço e do deslocamento deve ser um endereço válido. (Isso significa que tanto o deslocamento quanto o endereço ao qual o deslocamento é adicionado podem ser inválidos, desde que sua soma seja um endereço válido.)  
  
> [!NOTE]  
>  As compensações de vinculação não são suportadas pelo ODBC 2. *x* drivers.
