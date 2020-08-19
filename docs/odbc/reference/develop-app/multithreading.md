---
description: Multithreading
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
ms.openlocfilehash: 470a3d3a4d76ae038e3c80b9aa9b93dfd1d0ed79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429238"
---
# <a name="multithreading"></a>Multithreading
Em sistemas operacionais multithread, os drivers devem ser thread-safe. Ou seja, deve ser possível que os aplicativos usem o mesmo identificador em mais de um thread. Como isso é feito é específico do driver e é provável que os drivers serializarão qualquer tentativa de usar simultaneamente o mesmo identificador em dois threads diferentes.  
  
 Aplicativos geralmente usam vários threads em vez de processamento assíncrono. O aplicativo cria um thread separado, chama uma função ODBC nele e continua o processamento no thread principal. Em vez de ter que sondar continuamente a função assíncrona, como é o caso quando o atributo de instrução de SQL_ATTR_ASYNC_ENABLE é usado, o aplicativo pode simplesmente permitir que o thread recém-criado seja concluído.  
  
 As funções que aceitam um identificador de instrução e estão em execução em um thread podem ser canceladas chamando **SQLCancel** com o mesmo identificador de instrução de outro thread. Embora os drivers não devam serializar o uso de **SQLCancel** dessa maneira, não há nenhuma garantia de que chamar **SQLCancel** irá realmente cancelar a função em execução no outro thread.
