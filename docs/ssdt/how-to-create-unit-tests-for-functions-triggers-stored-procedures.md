---
title: Como criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96676bfa7c997d94eb79712f67b4b51fd165134b
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082598"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>Como: Criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados
Você pode gravar testes de unidade que avaliem as alterações feitas em qualquer objeto de banco de dados. No entanto, o SQL Server Data Tools inclui suporte adicional para criar testes para funções de banco de dados, gatilhos e procedimentos armazenados de um nó de projeto de banco de dados no Pesquisador de Objetos do SQL Server. Os stubs de código Transact\-SQL podem ser gerados automaticamente para que você os personalize.  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>Para criar um teste de unidade do SQL Server a partir de uma função, um gatilho ou um procedimento armazenado  
  
1.  Confira [Passo a passo: criar e executar um teste de unidade do SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md) para obter um exemplo de como adicionar um teste de unidade para um procedimento armazenado, na seção "Para criar um teste de unidade do SQL Server para os procedimentos armazenados".  
  
    A condição de teste Inconclusivo é a condição padrão adicionada a cada teste. Ela é incluída para indicar que a verificação de teste não foi implementada. Exclua essa condição do teste depois que você adicionar outras condições. Para saber mais, confira [Como adicionar condições de teste a testes de unidade do SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md).  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Como criar um teste de unidade do SQL Server vazio](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
