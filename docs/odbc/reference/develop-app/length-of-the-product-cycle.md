---
title: Duração do ciclo do produto | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d235146ffe1b4699f0064c5772407bcf40ae962
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306189"
---
# <a name="length-of-the-product-cycle"></a>Comprimento do ciclo do produto
A última questão sobre interoperabilidade é o tempo. Desenvolver uma aplicação interoperável geralmente leva mais tempo do que desenvolver uma não interoperável. A razão é que o aplicativo deve verificar os recursos do DBMS, executar as mesmas tarefas de forma diferente para DBMSs diferentes, trabalhar em torno da funcionalidade suportada por alguns DBMSs, mas não outros, e assim por diante.  
  
 Além do tempo de desenvolvimento, a vida útil do produto deve ser considerada. Se o aplicativo for projetado para ser usado uma vez, como um aplicativo que transfere dados ao migrar de um DBMS para outro, não há sentido em torná-lo interoperável. A aplicação será usada uma vez e descartada.  
  
 Se o aplicativo existir por um longo tempo, pode ser mais fácil manter como uma aplicação interoperável. Isso é verdade até mesmo para aplicativos personalizados que têm um único DBMS como alvo. A razão é que o código interoperável usa um subconjunto limitado de recursos de banco de dados. O driver é obrigado a manter esses recursos disponíveis, mesmo diante das alterações no DBMS subjacente. Assim, o código interoperável pode transferir a carga de lidar com alterações no DBMS do desenvolvedor de aplicativos para o desenvolvedor do driver.
