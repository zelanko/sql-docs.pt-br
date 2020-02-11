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
ms.openlocfilehash: d0dbddc71b0d647246d10dad16ad72d533df16de
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023353"
---
# <a name="parameter-binding-offsets"></a>Deslocamentos de associação de parâmetro
Um aplicativo pode especificar que um deslocamento seja adicionado aos endereços de buffer de parâmetro associados e aos endereços de buffer de comprimento/indicador correspondentes quando **SQLExecDirect** ou **SQLExecute** for chamado. O resultado dessas adições determina os endereços usados nessas operações.  
  
 Os deslocamentos de ligação permitem que um aplicativo altere as associações sem chamar **SQLBindParameter** para os parâmetros associados anteriormente. Uma chamada para **SQLBindParameter** para reassociar um parâmetro altera o endereço do buffer e o ponteiro de comprimento/indicador. A reassociação com um deslocamento, por outro lado, simplesmente adiciona um deslocamento ao endereço do buffer do parâmetro associado existente e ao endereço do buffer de comprimento/indicador. Quando os deslocamentos são usados, as associações são um "modelo" de como os buffers de aplicativo são dispostos e o aplicativo pode mover esse "modelo" para diferentes áreas de memória alterando o deslocamento. Um novo deslocamento pode ser especificado a qualquer momento e sempre é adicionado aos valores associados originalmente.  
  
 Para especificar um deslocamento de ligação, o aplicativo define o atributo SQL_ATTR_PARAM_BIND_OFFSET_PTR instrução como o endereço de um buffer sqlinteiro. Antes que o aplicativo chame uma função que usa as associações, ele coloca um deslocamento em bytes nesse buffer, desde que nem o endereço do buffer do parâmetro nem o endereço do buffer de comprimento/indicador seja 0 e o parâmetro associado esteja na instrução SQL. A soma do endereço e o deslocamento devem ser um endereço válido. (Isso significa que ou tanto o deslocamento quanto o endereço para o qual o deslocamento é adicionado podem ser inválidos, desde que sua soma seja um endereço válido.)  
  
> [!NOTE]  
>  Os deslocamentos de ligação não são suportados pelo ODBC 2. drivers *x* .
