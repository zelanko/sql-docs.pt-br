---
title: Criar casos de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: e2bf49da49e6b7e79ee62b18925aa60401e4e2a4
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777222"
---
# <a name="creating-test-cases-oracletosql"></a>Criar casos de teste (OracleToSQL)
Use o Assistente de caso de teste para criar um teste. Este assistente permite que você crie casos de teste escolhendo testados e verificados os objetos e especificando os parâmetros de teste.  
  
## <a name="starting-the-test-case-wizard"></a>Iniciar o Assistente de caso de teste  
Para iniciar o clique do Assistente de caso de teste **novo caso de teste...** do **Tester** menu.  
  
Quando iniciado, o assistente procura por esquema SSMATESTER_ORACLE no servidor do Oracle de origem. É o esquema de extensão de teste usado para armazenar objetos auxiliares. Se o Assistente de caso de teste não é possível localizar SSMATESTER_ORACLE, ele exibe uma janela de diálogo que propõe para criar o esquema. (Essa situação normalmente ocorre durante a primeira execução do SSMA Tester).  
  
Se você abrir a janela de diálogo, clique em **Sim** para criar o esquema SSMATESTER_ORACLE no servidor de origem. Observe que você deve ter privilégios de Oracle para criar um novo usuário e criar objetos no esquema de usuário.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Visão geral de casos de teste usando o Assistente de criação  
O processo de criação de um caso de teste consiste em cinco etapas:  
  
1.  [Inicializando os casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [Selecionando e Configurando objetos para teste &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [Selecionar e configurar objetos afetados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [Personalizando a ordem de chamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [Concluindo a preparação do caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Teste de objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
