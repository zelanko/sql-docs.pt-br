---
title: Tarefas do motorista | Microsoft Docs
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
ms.openlocfilehash: 1b30df63a3c955d2ed074ab13649ea55c21a6da7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294196"
---
# <a name="driver-tasks"></a>Tarefas de driver
Tarefas específicas executadas pelos drivers incluem:  
  
-   Conectando e desconectando da fonte de dados.  
  
-   Verificando se há erros de função não verificados pelo Gerenciador de Driver.  
  
-   Início das transações; isso é transparente para a aplicação.  
  
-   Submetendo declarações SQL à fonte de dados para execução. O driver deve modificar o ODBC SQL para o SQL específico do DBMS; isso é muitas vezes limitado à substituição de cláusulas de escape definidas pela ODBC por SQL específico do DBMS.  
  
-   Envio de dados e recuperação de dados da fonte de dados, incluindo a conversão de tipos de dados conforme especificado pelo aplicativo.  
  
-   Mapeamento de erros específicos do DBMS para ODBC SQLSTATEs.
