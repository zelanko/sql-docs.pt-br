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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1eaa07ce22436bc8bfae215c0431480081ee0f06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086348"
---
# <a name="multithreading"></a>Multithreading
Em sistemas operacionais de vários threads, os drivers devem ser thread-safe. Ou seja, deve ser possível que aplicativos usem o mesmo identificador em mais de um thread. Como isso é feito é específica do driver, e é provável que os drivers serão serializar qualquer tentativa de usar o mesmo identificador simultaneamente em dois threads diferentes.  
  
 Aplicativos geralmente usam vários threads em vez de processamento assíncrono. O aplicativo cria um thread separado, chama uma função ODBC nele e, em seguida, continua o processamento no thread principal. Em vez de precisar sondar continuamente a função assíncrona, como é o caso quando o atributo SQL_ATTR_ASYNC_ENABLE da instrução é usado, o aplicativo pode simplesmente deixar que o thread recém-criado concluir.  
  
 Funções que aceitam um identificador de instrução e estão em execução em um thread podem ser canceladas, chamando **SQLCancel** com a mesma instrução tratar de outro thread. Embora os drivers não devem serializar o uso de **SQLCancel** dessa maneira, não há nenhuma garantia que a chamada **SQLCancel** , na verdade, cancelará a função em execução em outro thread.
