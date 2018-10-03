---
title: Tarefas de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee695c62fc60b2ebb0ae9bb33ef9008ba617b49a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772624"
---
# <a name="driver-tasks"></a>Tarefas de driver
As tarefas específicas realizadas por drivers incluem:  
  
-   Conexão e desconexão da fonte de dados.  
  
-   Verificando se há erros de função não verificados pelo Gerenciador de Driver.  
  
-   Iniciando transações; Isso é transparente para o aplicativo.  
  
-   Enviando instruções SQL para a fonte de dados para execução. O driver deve modificar ODBC SQL para SQL específicos de DBMS; Isso geralmente é limitado a substituição de cláusulas de escape definidas pelo ODBC com o SQL específicas do DBMS.  
  
-   Enviar dados e recuperação de dados da fonte de dados, incluindo a conversão de tipos de dados conforme especificado pelo aplicativo.  
  
-   Mapeamento de erros específicos de DBMS para SQLSTATEs do ODBC.
