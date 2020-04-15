---
title: Multithreading | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10d1b401ac780d24184c4c2337199e99973e916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302405"
---
# <a name="multithreading"></a>Multithreading
Em sistemas operacionais multithread, os drivers devem ser seguros para rosca. Ou seja, deve ser possível que as aplicações usem a mesma alça em mais de um segmento. Como isso é alcançado é específico do driver, e é provável que os drivers serializem qualquer tentativa de usar simultaneamente a mesma alça em dois segmentos diferentes.  
  
 Os aplicativos geralmente usam vários threads em vez de processamento assíncrono. O aplicativo cria um segmento separado, chama uma função ODBC nele e, em seguida, continua o processamento no segmento principal. Em vez de ter que fazer uma pesquisa contínua da função assíncrona, como é o caso quando o atributo de declaração SQL_ATTR_ASYNC_ENABLE é usado, o aplicativo pode simplesmente deixar o segmento recém-criado terminar.  
  
 Funções que aceitam uma alça de declaração e estão sendo executados em um segmento podem ser canceladas ligando para **o SQLCancel** com a mesma alça de declaração de outro segmento. Embora os drivers não deva serializar o uso do **SQLCancel** desta maneira, não há garantia de que chamar **o SQLCancel** realmente cancelará a função em execução no outro segmento.
