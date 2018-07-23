---
title: Como executar testes de unidade do SQL Server | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 34fe2d1e-d47b-4808-af56-8cc0fdae6518
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 276096d9e5ce082f31439e664614833eb68f6984
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083709"
---
# <a name="how-to-run-sql-server-unit-tests"></a>Como: Executar testes de unidade do SQL Server
Você pode executar um teste de unidade do SQL Server de várias maneiras, usando várias janelas e a janela Prompt de Comando.  
  
> [!NOTE]  
> Você não pode executar testes de unidade remotamente.  
  
As maneiras que estão disponíveis para você dependem do software que você instalou, conforme descrito em [Executar testes de unidade do SQL Serve](../ssdt/running-sql-server-unit-tests.md).  
  
### <a name="to-run-sql-server-unit-tests-using-test-view-visual-studio-2010"></a>Para executar testes de unidade do SQL Server usando o Modo de Teste (Visual Studio 2010)  
  
1.  No menu **Teste**, aponte para **Janelas** e clique em **Modo de Teste**.  
  
    A janela **Modo de Teste** é aberta.  
  
2.  Na janela **Modo de Teste**, clique no(s) teste(s) que deseja executar. Usando a tecla CTRL ou SHIFT, você pode especificar blocos de teste descontínuos ou contínuos.  
  
3.  Execute um destes procedimentos:  
  
    -   Clique com o botão direito do mouse na superfície da janela **Modo de Teste** e clique em **Executar Seleção**.  
  
    -   Na barra de ferramentas **Modo de Teste**, clique em **Executar Seleção**.  
  
### <a name="to-run-sql-server-unit-tests-using-test-explorer-visual-studio-2012"></a>Para executar testes de unidade do SQL Server usando o Gerenciador de Testes (Visual Studio 2012)  
  
1.  No menu **Teste**, aponte para **Janelas** e clique em **Gerenciador de Testes**.  
  
    A janela **Gerenciador de Testes** é aberta.  
  
2.  No **Gerenciador de Testes**, clique no(s) teste(s) que deseja executar. Usando a tecla CTRL ou SHIFT, você pode especificar blocos de teste descontínuos ou contínuos.  
  
3.  Clique com o botão direito do mouse em um dos testes realçados e, em seguida, clique em **Executar Testes Selecionados**.  
  
### <a name="to-run-sql-server-unit-tests-from-the-sql-server-unit-test-designer-visual-studio-2010"></a>Para executar testes de unidade do SQL Server do Designer de teste de unidade do SQL Server (Visual Studio 2010)  
  
-   Na barra de ferramentas **Ferramentas de Teste**, você encontrará botões para iniciar um projeto com ou sem o depurador.  
  
Essa etapa é executada em todos os testes na execução de teste atual. Assim que você iniciar uma execução do teste, a janela **Resultados de Teste** aparecerá e exibirá o andamento da execução do teste. Essa exibição inclui os testes que estão em execução e os que foram concluídos. Para saber mais, confira [Interpretar resultados do teste de unidade do SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md).  
  
## <a name="see-also"></a>Consulte Também  
[Executar testes de unidade do SQL Server](../ssdt/running-sql-server-unit-tests.md)  
[Como executar testes automatizados no Microsoft Visual Studio 2010](http://msdn.microsoft.com/library/ms182470(VS.100).aspx)  
[Executar testes automatizados pela linha de comando (Visual Studio 2010)](http://msdn.microsoft.com/library/ms182486(VS.100).aspx)  
[Testar o aplicativo (Visual Studio 2012)](http://msdn.microsoft.com/library/ms182409.aspx)  
  
