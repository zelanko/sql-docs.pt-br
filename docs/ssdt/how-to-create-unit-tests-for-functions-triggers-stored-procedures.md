---
title: 'Como fazer: Criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5d985e2b2638d8b0047f5b4d010d87c8f631af65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090222"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>Como fazer: Criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados
Você pode gravar testes de unidade que avaliem as alterações feitas em qualquer objeto de banco de dados. No entanto, o SQL Server Data Tools inclui suporte adicional para criar testes para funções de banco de dados, gatilhos e procedimentos armazenados de um nó de projeto de banco de dados no Pesquisador de Objetos do SQL Server. Os stubs de código Transact\-SQL podem ser gerados automaticamente para que você os personalize.  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>Para criar um teste de unidade do SQL Server a partir de uma função, um gatilho ou um procedimento armazenado  
  
1.  Veja [Passo a passo: criar e executar um teste de unidade do SQL Server](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md) para obter um exemplo de como adicionar um teste de unidade para um procedimento armazenado, na seção "Para criar um teste de unidade do SQL Server para os procedimentos armazenados".  
  
    A condição de teste Inconclusivo é a condição padrão adicionada a cada teste. Ela é incluída para indicar que a verificação de teste não foi implementada. Exclua essa condição do teste depois que você adicionar outras condições. Para obter mais informações, confira [Como Adicionar condições de teste a testes de unidade do SQL Server](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md).  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Como: Criar um teste de unidade do SQL Server vazio](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
