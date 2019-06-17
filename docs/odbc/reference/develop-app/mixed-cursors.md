---
title: Misto cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef8d5142397b4169513cf262ba4126ccba1fc1c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785838"
---
# <a name="mixed-cursors"></a>Cursores mistos

Um cursor misto é uma combinação de um cursor controlado por conjunto de chaves e um cursor dinâmico. Ele é usado quando o conjunto de resultados for muito grande para ser razoavelmente salvar chaves para o conjunto de resultados inteiro. Cursores mistos são implementados com a criação de um conjunto de chaves é menor do que o conjunto de resultados inteiro, mas maior do que o conjunto de linhas.  
  
 Desde que o aplicativo rola dentro do conjunto de chaves, o comportamento é controlado por conjunto de chaves. Quando o aplicativo rola fora do conjunto de chaves, o comportamento é dinâmico: O cursor busca as linhas solicitadas e cria um novo conjunto de chaves. Depois que o novo conjunto de chaves é criado, o comportamento será revertido para cursores controlados por dentro desse conjunto de chaves.  
  
 Por exemplo, suponha que um conjunto de resultados tem 1.000 linhas e usa um cursor misto com um tamanho de conjunto de chaves de 100 e um tamanho de conjunto de linhas de 10. Quando o primeiro conjunto de linhas for encontrado, o cursor cria um conjunto de chaves consistindo de chaves para as primeiras 100 linhas. Em seguida, ele retorna as primeiras 10 linhas, conforme solicitado.  
  
 Agora vamos supor que o outro o aplicativo exclui linhas 11 e 101. Se o cursor tenta recuperar a linha 11, ele encontrará uma lacuna porque ele tem uma chave para essa linha, mas não há nenhuma linha; Isso é controlado por comportamento. Se o cursor tenta recuperar a linha 101, o cursor não detectará que a linha está falta porque não tem uma chave para a linha. Em vez disso, ele irá recuperar o que era anteriormente linha 102. Esse é o comportamento de cursor dinâmico.  
  
 Um cursor misto é equivalente a um cursor controlado por quando o tamanho do conjunto de chaves é igual ao tamanho de conjunto de resultados. Um cursor misto é equivalente a um cursor dinâmico quando o tamanho do conjunto de chaves é igual a 1.
