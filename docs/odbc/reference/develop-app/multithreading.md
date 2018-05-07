---
title: Multithread | Microsoft Docs
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
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cf1543a039c0928068209d1d79064b074fdc2f8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="multithreading"></a>Multithread
Em sistemas operacionais de vários threads, os drivers devem ser thread-safe. Ou seja, deve ser possível para os aplicativos usem o mesmo identificador em mais de um thread. Como isso é obtido é específico do driver, e é provável que os drivers serializará qualquer tentativa de usar o mesmo identificador simultaneamente em dois threads diferentes.  
  
 Aplicativos geralmente usam vários threads, em vez do processamento assíncrono. O aplicativo cria um thread separado, ele chama uma função ODBC e continua o processamento no thread principal. Em vez de precisar sondar continuamente a função assíncrona, como é o caso quando o atributo de instrução SQL_ATTR_ASYNC_ENABLE for usado, o aplicativo pode simplesmente permite que o thread recém-criado concluir.  
  
 Funções que aceitam um identificador de instrução e estão em execução em um thread podem ser canceladas chamando **SQLCancel** com a mesma instrução tratar de outro thread. Embora os drivers não devem serializar o uso de **SQLCancel** dessa maneira, não há nenhuma garantia que a chamada **SQLCancel** realmente cancelará a função em execução em outro thread.
