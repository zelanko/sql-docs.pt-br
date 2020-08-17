---
description: Tarefas de driver
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 263f591592063a45fdd5afdca4efdd75b5b915b6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339052"
---
# <a name="driver-tasks"></a>Tarefas de driver
Tarefas específicas executadas por drivers incluem:  
  
-   Conectando-se e desconectando-se da fonte de dados.  
  
-   Verificando se há erros de função não verificados pelo Gerenciador de driver.  
  
-   Iniciando transações; Isso é transparente para o aplicativo.  
  
-   Enviando instruções SQL para a fonte de dados para execução. O driver deve modificar o ODBC SQL para SQL específico do DBMS; Isso geralmente é limitado à substituição de cláusulas de escape definidas pelo ODBC por SQL específico do DBMS.  
  
-   Enviando dados para e recuperando dados da fonte de dados, incluindo a conversão de tipos de dados conforme especificado pelo aplicativo.  
  
-   Mapeamento de erros específicos do DBMS para o ODBC sqlstates.
