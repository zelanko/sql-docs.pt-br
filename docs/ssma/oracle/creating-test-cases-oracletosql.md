---
title: Criando casos de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: a2c1bd3fea167a784d86f7e323566f73c3a01f86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287713"
---
# <a name="creating-test-cases-oracletosql"></a>Criar casos de teste (OracleToSQL)
Use o Assistente de caso de teste para criar um teste. Este assistente permite criar casos de teste escolhendo testados e verificados os objetos e especificando os parâmetros de testes.  
  
## <a name="starting-the-test-case-wizard"></a>Iniciando o Assistente de caso de teste  
Para iniciar o Assistente de caso de teste, clique em **novo caso de teste...**  do **testador** menu.  
  
Quando iniciado, o assistente procura o esquema SSMATESTER_ORACLE no servidor do Oracle de origem. É o esquema de extensão do testador usado para armazenar objetos auxiliares. Se o Assistente de caso de teste não é possível localizar SSMATESTER_ORACLE, ele exibirá uma janela de caixa de diálogo que propõe para criar o esquema. (Essa situação geralmente ocorre durante a primeira execução do SSMA testador).  
  
Se você receber a janela de diálogo, clique em **Sim** para criar o esquema SSMATESTER_ORACLE no servidor de origem. Observe que você deve ter privilégios de Oracle para criar um novo usuário e criar objetos no esquema deste usuário.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Visão geral da criação de casos de teste usando o Assistente  
O processo de criação de um caso de teste consiste em cinco etapas:  
  
1.  [Inicializar casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [Selecionando e Configurando objetos a testar &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [Selecionar e configurar os objetos afetados pelo &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [Personalizando a ordem das chamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [Concluir a preparação do caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Testar objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
