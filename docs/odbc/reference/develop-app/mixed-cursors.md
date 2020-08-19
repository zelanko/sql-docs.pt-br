---
description: Cursores mistos
title: Cursores mistos | Microsoft Docs
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
ms.openlocfilehash: 5b15aaee9d74319daa1a211610ce283d247fda2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424598"
---
# <a name="mixed-cursors"></a>Cursores mistos

Um cursor misto é uma combinação de um cursor controlado por conjunto de chaves e um cursor dinâmico. Ele é usado quando o conjunto de resultados é muito grande para salvar as chaves razoavelmente para todo o conjunto de resultados. Cursores mistos são implementados pela criação de um conjunto de chaves que seja menor do que o definido de resultados inteiro, mas maior do que o conjunto de linhas.  
  
 Desde que o aplicativo Role no conjunto de chaves, o comportamento é controlado por conjunto de chaves. Quando o aplicativo rola para fora do conjunto de chaves, o comportamento é dinâmico: o cursor busca as linhas solicitadas e cria um novo conjunto de chaves. Depois que o novo conjunto de chaves é criado, o comportamento é revertido para controlado por conjunto de chaves nesse conjunto.  
  
 Por exemplo, suponha que um conjunto de resultados tenha 1.000 linhas e use um cursor misto com um tamanho de conjunto de chaves de 100 e um tamanho de conjuntos de linhas de 10. Quando o primeiro conjunto de linhas é buscado, o cursor cria um conjunto de chaves que consiste nas chaves para as primeiras 100 linhas. Em seguida, ele retorna as primeiras 10 linhas, conforme solicitado.  
  
 Agora suponha que outro aplicativo exclua as linhas 11 e 101. Se o cursor tentar recuperar a linha 11, ele encontrará uma lacuna porque ela tem uma chave para essa linha, mas nenhuma linha existe; Esse é o comportamento controlado por conjunto de chaves. Se o cursor tentar recuperar a linha 101, o cursor não detectará que a linha está ausente porque não tem uma chave para a linha. Em vez disso, ele recuperará o que antes era a linha 102. Esse é o comportamento de cursor dinâmico.  
  
 Um cursor misto é equivalente a um cursor controlado por conjunto de chaves quando o tamanho do conjunto de chaves é igual ao tamanho definido do resultado. Um cursor misto é equivalente a um cursor dinâmico quando o tamanho do conjunto de chaves é igual a 1.
