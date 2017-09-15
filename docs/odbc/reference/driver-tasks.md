---
title: Tarefas de driver | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 331e3aee3a4a60cbfa1a1308b71da80bf9772f23
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="driver-tasks"></a>Tarefas de driver
As tarefas específicas realizadas por drivers incluem:  
  
-   A conexão e desconexão da fonte de dados.  
  
-   Verificação de erros de função não verificados pelo Gerenciador de Driver.  
  
-   Iniciando transações; Isso é transparente para o aplicativo.  
  
-   Enviar instruções SQL para a fonte de dados para execução. O driver deve modificar ODBC SQL para SQL DBMS específico; Isso geralmente é limitado a substituição de cláusulas de fuga definidas pelo ODBC com o SQL DBMS específico.  
  
-   Enviar dados para e recuperar dados da fonte de dados, incluindo conversão de tipos de dados conforme especificado pelo aplicativo.  
  
-   Mapeando erros específicos de DBMS para SQLSTATEs do ODBC.
