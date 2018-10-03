---
title: Deslocamentos de associação de parâmetro | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1fd069336a52b0a27ae927880f749c02d2c1d43
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765880"
---
# <a name="parameter-binding-offsets"></a>Deslocamentos de associação de parâmetro
Um aplicativo pode especificar que um deslocamento é adicionado ao associados a endereços de buffer do parâmetro e o comprimento/indicador correspondente buffer endereços quando **SQLExecDirect** ou **SQLExecute** é chamado. O resultado dessas adições determina os endereços usados nessas operações.  
  
 Deslocamentos de ligação permitem que um aplicativo alterar associações sem chamar **SQLBindParameter** para parâmetros associados anteriormente. Uma chamada para **SQLBindParameter** reassociar um parâmetro altera o endereço do buffer e o ponteiro de comprimento/indicador. Nova associação com um deslocamento, por outro lado, simplesmente adiciona um deslocamento para o endereço de buffers de parâmetro associado existente e o endereço do buffer de comprimento/indicador. Quando deslocamentos são usados, as associações são um "modelo" de como os buffers do aplicativo são dispostos e o aplicativo pode mover esse "modelo" para diferentes áreas de memória, alterando o deslocamento. Um novo deslocamento pode ser especificado a qualquer momento e sempre é adicionado para os valores de limite originalmente.  
  
 Para especificar um deslocamento de ligação, o aplicativo define o atributo da instrução SQL_ATTR_PARAM_BIND_OFFSET_PTR para o endereço de um buffer sqlinteger que contém. Antes do aplicativo chama uma função que usa as associações, ele coloca um deslocamento em bytes nesse buffer, desde que nem o endereço do buffer de parâmetro nem o endereço do buffer de comprimento/indicador é 0, e o parâmetro associado é na instrução SQL. A soma do endereço e o deslocamento deve ser um endereço válido. (Isso significa que um ou ambos os o deslocamento e o endereço ao qual o deslocamento é adicionado podem ser inválidos, desde que sua soma é um endereço válido).  
  
> [!NOTE]  
>  Deslocamentos de associação não são suportados pelo ODBC 2. *x* drivers.
