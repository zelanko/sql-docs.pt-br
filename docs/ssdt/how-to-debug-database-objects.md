---
title: Depurar objetos de banco de dados
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: f5d4584f-e85f-4558-b056-83681c365978
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: ba04eba5107968f1be11c62fbac0f57ca5733b3f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241458"
---
# <a name="how-to--debug-database-objects"></a>Como fazer:  Depurar objetos de banco de dados

Um teste de unidade do SQL Server consiste no seguinte:  
  
-   Código de teste de unidade escrito em Visual C\# ou Visual Basic. Este código, que é gerado pelo Designer de Teste de Unidade do SQL Server, é responsável por enviar o script Transact\-SQL que forma o corpo do teste.  
  
-   Uma ou mais condições de teste, que são gravadas na linguagem Visual C\# ou Visual Basic. Para depurar condições de teste, siga o procedimento para depurar um teste de unidade conforme descrito em [Como depurar enquanto um teste é executado (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182484(VS.100).aspx) ou [Como depurar enquanto um teste é executado (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182484.aspx).  
  
-   Um ou mais scripts Transact\-SQL executados nos objetos do banco de dados que você está testando. Você não pode depurar esses scripts Transact\-SQL.  
  
Os procedimentos deste tópico descrevem como depurar objetos de banco de dados específicos, como procedimentos armazenados, funções e gatilhos no banco de dados que você está testando. Para depurar um objeto de banco de dados, siga estes procedimentos nesta ordem:  
  
1.  Habilite a depuração do SQL Server em seu projeto de teste.  
  
2.  Habilite a depuração de aplicativo na instância do SQL Server que hospeda o banco de dados que você está testando.  
  
3.  Defina pontos de interrupção no script Transact\-SQL do objeto de banco de dados que você está depurando.  
  
4.  Depurar o teste de unidade. Neste procedimento, você executa o teste no modo de depuração.  
  
### <a name="to-enable-sql-debugging-on-your-test-project"></a>Para habilitar a depuração do SQL Server no projeto de teste  
  
1.  Abra o **Gerenciador de Soluções**.  
  
2.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de teste e clique em **Propriedades**.  
  
    A página de propriedades que tem o mesmo nome do projeto de teste é aberta.  
  
3.  Na página de propriedades, clique em **Depurar**.  
  
4.  Em **Habilitar depuradores**, clique em **Ativar depuração do SQL Server**.  
  
5.  Salve suas alterações.  
  
### <a name="to-set-an-increased-execution-context-timeout-to-enable-debugging-for-your-test-project"></a>Para definir o tempo limite maior do contexto de execução para habilitar a depuração do projeto de teste  
  
1.  No menu **Arquivo**, aponte para **Abrir**e clique em **Arquivo**.  
  
2.  Navegue até a pasta que contém o projeto de teste e clique duas vezes no arquivo app.config.  
  
    O arquivo app.config é aberto no editor.  
  
3.  Modifique o nó ExecutionContext para adicionar um tempo limite de comando, como no exemplo a seguir:  
  
    ```  
    <ExecutionContext CommandTimeout ="300" Provider="System.Data.SqlClient" ConnectionString="Data Source=TargetServerName\TargetInstanceName;Initial Catalog=TargetDatabaseName;Integrated Security=True;Pooling=False" />  
    ```  
  
4.  Salve suas alterações.  
  
5.  Recompilar o projeto de teste de unidade.  
  
> [!IMPORTANT]  
> Se você não recompilar o projeto, as alterações feitas no arquivo app.config não serão aplicadas quando você executar os testes de unidade, e a depuração falhará.  
  
### <a name="to-add-breakpoints-to-your-transact-sql-script"></a>Para adicionar pontos de interrupção ao script Transact\-SQL  
  
1.  No menu **Exibir**, abra o **Pesquisador de Objetos do SQL Server**.  
  
2.  Em **Conexões de Dados**, expanda o nó do banco de dados que você deseja testar.  
  
3.  Se um “x” vermelho pequeno aparecer ao lado do ícone de banco de dados, a conexão com o banco de dados será fechada. Nesse caso, clique com o botão direito do mouse no banco de dados e clique em **Atualizar**. Talvez seja necessário fornecer credenciais para abrir a conexão com o banco de dados.  
  
4.  Expanda o nó **Exibições**, **Procedimentos Armazenados** ou **Funções** para localizar o objeto a ser depurado.  
  
5.  Clique duas vezes no objeto a ser depurado.  
  
6.  Clique na barra lateral cinza para definir um ponto de interrupção.  
  
### <a name="to-debug-your-sql-server-unit-test"></a>Para depurar seu teste de unidade do SQL Server  
  
1.  No Visual Studio 2010, abra a janela (Test -> Windows) **Modo de Teste**. No Visual Studio 2012, abra a janela **Gerenciador de Testes**.  
  
2.  Clique com o botão direito do mouse no teste cujo script Transact\-SQL usa o objeto de banco de dados em que você define pontos de interrupção e selecione **Depurar Seleção**.  
  
    O teste é executado no modo de depuração até que seja encontrado um ponto de interrupção no objeto de banco de dados.  
  
3.  (Opcional) Para abrir outra janela de depuração, abra o menu **Depurar**, aponte para **Janelas** e clique em **Pontos de Interrupção**, **Saída** ou **Imediato**.  
  
## <a name="see-also"></a>Consulte Também  
[Executar testes de unidade do SQL Server](../ssdt/running-sql-server-unit-tests.md)  
[Depurar o Transact-SQL (Visual Studio 2010)](https://go.microsoft.com/fwlink/?LinkId=163975)  
  
