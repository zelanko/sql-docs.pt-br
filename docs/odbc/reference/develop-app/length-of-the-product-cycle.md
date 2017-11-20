---
title: Comprimento do ciclo de produto | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c363ecd47545868e2d40afabdce9bbef6f78031
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="length-of-the-product-cycle"></a>Comprimento do ciclo do produto
A pergunta final sobre interoperabilidade é o tempo. Desenvolvendo um aplicativo interoperável geralmente demora mais do que desenvolver um noninteroperable. O motivo é que o aplicativo deve verificar recursos do DBMS, executar as mesmas tarefas diferente para diferentes DBMSs, contornar a funcionalidade com suporte por alguns DBMSs, mas outros não e assim por diante.  
  
 Além do tempo de desenvolvimento, o tempo de vida do produto deve ser considerado. Se o aplicativo foi projetado para ser usado uma vez, como um aplicativo que transfere dados ao migrar de um DBMS para outro, não faz sentido em tornando interoperável. O aplicativo será usado uma vez e descartado.  
  
 Se o aplicativo continuará a existir por um longo tempo, seria mais fácil de manter como um aplicativo interoperável. Isso é verdadeiro mesmo para aplicativos personalizados que têm um DBMS único como um destino. O motivo é que o código interoperável usa um subconjunto limitado dos recursos de banco de dados. O driver é necessária para manter os recursos disponíveis, mesmo em caso de alterações do DBMS subjacente. Assim, código de interoperabilidade pode deslocar a sobrecarga de cópia com as alterações para o DBMS do desenvolvedor de aplicativos para o desenvolvedor de driver.

