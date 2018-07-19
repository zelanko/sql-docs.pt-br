---
title: Como adicionar condições de teste a testes de unidade do SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 85ba2e56-a0b2-489c-aea2-fb135cce0cfc
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4e341b085f4a7ca591e02328db1bda8fae75a4ed
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093621"
---
# <a name="how-to-add-test-conditions-to-sql-server-unit-tests"></a>Como: Adicionar condições de teste a testes de unidade do SQL Server
Você pode adicionar condições de teste a um teste de unidade do SQL Server usando o **Designer de Teste de Unidade do SQL Server**. Quando você salvar a classe de teste, as condições de teste serão salvas automaticamente no projeto de teste como código Visual C\# ou Visual Basic no arquivo de código-fonte contendo a classe de teste. Após salvar uma condição de teste, você poderá editá-la no **Designer de Teste de Unidade do SQL Server** ou em seu arquivo de código-fonte.  
  
### <a name="to-add-test-conditions-to-a-sql-server-unit-test"></a>Para adicionar condições de teste a um teste de unidade do SQL Server  
  
1.  Abra um teste de unidade do SQL Server no **Designer de Teste de Unidade do SQL Server**.  
  
    O nome de teste que você abriu é exibido na barra de navegação na parte superior do Designer de Teste de Unidade do SQL Server. Usando a barra de navegação, você pode selecionar os diferentes métodos de teste que estão na classe de teste.  
  
2.  Na barra de navegação, clique no método de teste ao qual deseja adicionar as condições de teste ou clique em **Scripts Comuns**.  
  
    > [!NOTE]  
    > Os scripts comuns não pertencem a um teste de unidade específico. Em vez de isso, eles vêm antes ou depois dos testes de unidade em uma classe de teste. Para saber mais, confira [Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md).  
  
3.  Na barra de navegação, clique no script Transact\-SQL ao qual deseja adicionar as condições de teste. Você pode adicionar condições de teste ao script de pré-teste, de teste ou de pós-teste.  
  
    O script Transact\-SQL desse teste é exibido no editor Transact\-SQL, e suas condições de teste aparecerão no painel **Condições de Teste**.  
  
4.  Na lista de seleção **Condições de Teste**, clique em uma condição de teste e clique em **Adicionar Condição de Teste** (+).  
  
    A condição de teste é adicionada ao método de teste de unidade.  
  
    > [!NOTE]  
    > Você pode reorganizar as condições de teste em um método de teste clicando em uma condição de teste e, em seguida, clicando nas setas para cima e para baixo no painel **Condições de Teste**.  
  
5.  Selecione a condição de teste que você acabou de adicionar e exiba a janela **Propriedades**.  
  
    Configure a condição de teste na janela Propriedades. Por exemplo, você pode alterar a propriedade **Tempo de Execução** de uma condição de teste Tempo de Execução. Se você definir essa propriedade, o teste apresentará falha se o script Transact\-SQL não for executado no tempo especificado.  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[Como criar um teste de unidade do SQL Server vazio](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[Como criar testes de unidade do SQL Server para funções, gatilhos e procedimentos armazenados](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[Usar condições de teste nos testes de unidade do SQL Server](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[Scripts nos testes de unidade do SQL Server](../ssdt/scripts-in-sql-server-unit-tests.md)  
[Interpretar resultados do teste de unidade do SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md)  
[Como executar testes de unidade do SQL Server](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
