---
title: Comprimento do ciclo do produto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 203ad92dd6abfc71b0fdeddc466752612e666cee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100450"
---
# <a name="length-of-the-product-cycle"></a>Comprimento do ciclo do produto
A última pergunta sobre a interoperabilidade é a hora. Desenvolver um aplicativo interoperável geralmente leva mais tempo do que desenvolver um noninteroperable. O motivo é que o aplicativo deve verificar os recursos do DBMS, executar as mesmas tarefas de forma diferente para diferentes DBMSs, contornar a funcionalidade com suporte de alguns DBMSs, mas não para outros e assim por diante.  
  
 Além do tempo de desenvolvimento, o tempo de vida do produto deve ser considerado. Se o aplicativo foi projetado para ser usado uma vez, como um aplicativo que transfere dados ao migrar de um DBMS para outro, não há nenhum ponto de torná-lo interoperável. O aplicativo será usado uma vez e descartado.  
  
 Se o aplicativo continuará a existir por muito tempo, ele pode ser mais fácil de manter como um aplicativo interoperável. Isso é verdadeiro mesmo para aplicativos personalizados que têm um DBMS único como um destino. O motivo é que o código interoperável usa um subconjunto limitado de recursos de banco de dados. O driver é necessária para manter esses recursos disponíveis, mesmo em caso de alterações para o DBMS subjacente. Assim, código interoperável pode deslocam a carga de cópia com as alterações para o DBMS do desenvolvedor de aplicativos para o desenvolvedor de driver.
