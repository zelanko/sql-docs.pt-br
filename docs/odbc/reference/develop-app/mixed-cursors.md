---
title: Misto cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52018d329255d05df03e1dc9e070225a84dbd97d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mixed-cursors"></a>Cursores mistos
Um cursor misto é uma combinação de um cursor controlado por conjunto de chaves e um cursor dinâmico. Ele é usado quando o conjunto de resultados for muito grande para ser razoavelmente salvar as chaves para o conjunto de resultados inteiro. Mistos cursores são implementados por meio da criação de um conjunto de chaves, mas menor do que o conjunto de resultados inteiro maior do que o conjunto de linhas.  
  
 Como o aplicativo rola no conjunto de chaves, o comportamento é controlado por. Quando o aplicativo rola fora do conjunto de chaves, o comportamento é dinâmico: O cursor busque as linhas solicitadas e cria um novo conjunto de chaves. Depois que o novo conjunto de chaves é criado, o comportamento será revertido para cursores controlados por dentro desse conjunto de chaves.  
  
 Por exemplo, suponha que um conjunto de resultados tem 1.000 linhas e usa um cursor misto com um tamanho de conjunto de chaves de 100 e um tamanho de conjunto de linhas de 10. Quando o primeiro conjunto de linhas for encontrado, o cursor cria um conjunto de chaves consistindo de chaves para as primeiras 100 linhas. Ele então retorna as primeiras 10 linhas, conforme solicitado.  
  
 Agora suponha que outro aplicativo linhas de exclusões 11 e 101. Se o cursor tenta recuperar a linha 11, ele será exibido um buraco porque ele tem uma chave para essa linha, mas não há nenhuma linha; Isso é controlado por comportamento. Se o cursor tenta recuperar a linha 101, o cursor não detectará que a linha está falta porque ele não tem uma chave para a linha. Em vez disso, ele recuperará o que era anteriormente linha 102. Esse é o comportamento de cursor dinâmico.  
  
 Um cursor misto é equivalente a um cursor controlado por conjunto de chaves quando o tamanho do conjunto de chaves é igual ao tamanho do conjunto de resultados. Um cursor misto é equivalente a um cursor dinâmico quando o tamanho do conjunto de chaves é igual a 1.
