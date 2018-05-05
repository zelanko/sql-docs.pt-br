---
title: Deslocamentos de associação de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0ebc6ffe4b02f04ece2528443f5d8c2ba3af014
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-binding-offsets"></a>Deslocamentos de associação de parâmetros
Um aplicativo pode especificar que um deslocamento é adicionado ao associados a endereços de buffer do parâmetro e o comprimento/indicador correspondente buffer endereços quando **SQLExecDirect** ou **SQLExecute** é chamado. O resultado dessas adições determina os endereços usados nessas operações.  
  
 Deslocamentos de ligação permitem que um aplicativo alterar associações sem chamar **SQLBindParameter** para parâmetros associados anteriormente. Uma chamada para **SQLBindParameter** reassociar um parâmetro altera o endereço do buffer e o ponteiro de comprimento/indicador. Reassociação com um deslocamento, por outro lado, simplesmente adiciona um deslocamento para o endereço de buffers de parâmetro associadas existente e o endereço do buffer de comprimento/indicador. Quando os deslocamentos são usados, as associações são um "modelo" de como os buffers de aplicativo são dispostos e o aplicativo pode mover esta "template" para diferentes áreas de memória, alterando o deslocamento. Um novo deslocamento pode ser especificado a qualquer momento e sempre é adicionado para os valores de limite originalmente.  
  
 Para especificar um deslocamento de associação, o aplicativo define o atributo de instrução SQL_ATTR_PARAM_BIND_OFFSET_PTR para o endereço de um buffer sqlinteger que contém. Antes do aplicativo chama uma função que usa as associações, coloca um deslocamento em bytes nesse buffer, contanto que o endereço de buffers de parâmetro, nem o endereço do buffer de comprimento/indicador é 0 e o parâmetro associado está na instrução SQL. A soma do endereço e o deslocamento deve ser um endereço válido. (Isso significa que um ou ambos os o deslocamento e o endereço para o qual o deslocamento é adicionado podem ser inválidas, como soma é um endereço válido).  
  
> [!NOTE]  
>  Deslocamentos de associação não são suportados pelo ODBC 2. *x* drivers.
