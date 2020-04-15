---
title: Cursors mistos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a91dacf8ea9c0ed0db2c3b64634ddd53b854a534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307431"
---
# <a name="mixed-cursors"></a>Cursores mistos

Um cursor misto é uma combinação de um cursor orientado por keyset e um cursor dinâmico. Ele é usado quando o conjunto de resultados é muito grande para economizar razoavelmente chaves para todo o conjunto de resultados. Os cursores mistos são implementados criando um conjunto de tecla menor do que todo o conjunto de resultados, mas maior do que o conjunto de linhas.  
  
 Enquanto o aplicativo rolar dentro do conjunto de chaves, o comportamento é orientado por conjuntos de chaves. Quando o aplicativo rola para fora do conjunto de chaves, o comportamento é dinâmico: o cursor busca as linhas solicitadas e cria um novo conjunto de chaves. Depois que o novo conjunto de chaves é criado, o comportamento reverte para keyset-driven dentro desse conjunto de chaves.  
  
 Por exemplo, suponha que um conjunto de resultados tenha 1.000 linhas e use um cursor misto com um tamanho de keyset de 100 e um tamanho de conjunto de linhas de 10. Quando o primeiro conjunto de linhas é buscado, o cursor cria um conjunto de teclas que consiste nas teclas das primeiras 100 linhas. Em seguida, retorna as primeiras 10 linhas, conforme solicitado.  
  
 Agora suponha que outro aplicativo exclua as linhas 11 e 101. Se o cursor tentar recuperar a linha 11, ele encontrará uma lacuna porque tem uma chave para esta linha, mas não existe nenhuma linha; este é um comportamento orientado por chave. Se o cursor tentar recuperar a linha 101, o cursor não detectará que a linha está faltando porque não tem uma chave para a linha. Em vez disso, ele vai recuperar o que era anteriormente linha 102. Este é um comportamento dinâmico do cursor.  
  
 Um cursor misto é equivalente a um cursor orientado por chave quando o tamanho do conjunto de tecla é igual ao tamanho do conjunto de resultados. Um cursor misto é equivalente a um cursor dinâmico quando o tamanho do conjunto de chaves é igual a 1.
