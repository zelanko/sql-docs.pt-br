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
manager: shamikg
ms.openlocfilehash: 697f7049a60aa7ae2b8c89d1fb6c5ce8e3d29312
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266130"
---
# <a name="creating-test-cases-oracletosql"></a>Criar casos de teste (OracleToSQL)
Use o assistente de caso de teste para criar um teste. Este assistente permite que você crie casos de teste escolhendo objetos testados e verificados e especificando os parâmetros de teste.  
  
## <a name="starting-the-test-case-wizard"></a>Iniciando o assistente de caso de teste  
Para iniciar o assistente de caso de teste, clique em **novo caso de teste...** no menu **testador** .  
  
Quando iniciado, o assistente procura SSMATESTER_ORACLE de esquema no servidor Oracle de origem. É o esquema de extensão do testador usado para armazenar objetos auxiliares. Se o assistente de caso de teste não conseguir localizar SSMATESTER_ORACLE, ele exibirá uma janela de diálogo que propõe criar o esquema. (Essa situação geralmente ocorre durante a primeira execução do SSMA Tester.)  
  
Se você receber a janela de diálogo, clique em **Sim** para criar SSMATESTER_ORACLE esquema no servidor de origem. Observe que você deve ter privilégios Oracle para criar um novo usuário e criar objetos no esquema deste usuário.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Visão geral da criação de casos de teste usando o assistente  
O processo de criação de um caso de teste consiste em cinco etapas:  
  
1.  [Inicializando casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [Selecionando e configurando objetos para testar &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [Selecionando e configurando objetos afetados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [Personalizando a ordem das chamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [Concluindo a preparação do caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Testando objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
