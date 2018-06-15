---
title: Tarefas de driver | Microsoft Docs
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
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b8ea61df89eb6f4e21a57e71a4277d56b16add5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915701"
---
# <a name="driver-tasks"></a>Tarefas de driver
As tarefas específicas realizadas por drivers incluem:  
  
-   A conexão e desconexão da fonte de dados.  
  
-   Verificação de erros de função não verificados pelo Gerenciador de Driver.  
  
-   Iniciando transações; Isso é transparente para o aplicativo.  
  
-   Enviar instruções SQL para a fonte de dados para execução. O driver deve modificar ODBC SQL para SQL DBMS específico; Isso geralmente é limitado a substituição de cláusulas de fuga definidas pelo ODBC com o SQL DBMS específico.  
  
-   Enviar dados para e recuperar dados da fonte de dados, incluindo conversão de tipos de dados conforme especificado pelo aplicativo.  
  
-   Mapeando erros específicos de DBMS para SQLSTATEs do ODBC.
