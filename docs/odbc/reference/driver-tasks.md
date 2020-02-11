---
title: Tarefas do driver | Microsoft Docs
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
ms.openlocfilehash: 2e2ed50ac3f9e914953abdd64907199a5f978af2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915465"
---
# <a name="driver-tasks"></a>Tarefas de driver
Tarefas específicas executadas por drivers incluem:  
  
-   Conectando-se e desconectando-se da fonte de dados.  
  
-   Verificando se há erros de função não verificados pelo Gerenciador de driver.  
  
-   Iniciando transações; Isso é transparente para o aplicativo.  
  
-   Enviando instruções SQL para a fonte de dados para execução. O driver deve modificar o ODBC SQL para SQL específico do DBMS; Isso geralmente é limitado à substituição de cláusulas de escape definidas pelo ODBC por SQL específico do DBMS.  
  
-   Enviando dados para e recuperando dados da fonte de dados, incluindo a conversão de tipos de dados conforme especificado pelo aplicativo.  
  
-   Mapeamento de erros específicos do DBMS para o ODBC sqlstates.
