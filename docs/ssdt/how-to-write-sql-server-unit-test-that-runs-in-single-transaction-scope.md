---
title: Como gravar um teste de unidade do SQL Server executado no escopo de uma única transação | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cb241e94-d81c-40e9-a7ae-127762a6b855
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 789322fa4274c6819fe1f71ac7ae06056fce5a5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785454"
---
# <a name="how-to-write-a-sql-server-unit-test-that-runs-within-the-scope-of-a-single-transaction"></a>Como: Gravar um teste de unidade do SQL Server executado no escopo de uma única transação
Você pode modificar os teste de unidade para execução no escopo de uma única transação. Se você usar essa abordagem, poderá reverter todas as alterações decretadas pelo teste após seu término. Os procedimentos a seguir descreve como:  
  
-   Criar uma transação em seu script de teste Transact\-SQL que usa **BEGIN TRANSACTION** e **ROLLBACK TRANSACTION**.  
  
-   Criar uma transação para um único método de teste em uma classe de teste.  
  
-   Criar uma transação para todos os métodos de teste em uma classe de teste.  
  
**Pré-requisitos**  
  
Para alguns procedimentos deste tópico, o serviço Coordenador de Transações Distribuídas deve estar em executar no computador em que o teste de unidade é executado. Para obter mais informações, consulte o procedimento descrito no final deste tópico.  
  
## <a name="to-create-a-transaction-using-transact-sql"></a>Para criar uma transação usando o Transact\-SQL  
  
#### <a name="to-create-a-transaction-using-transact-sql"></a>Para criar uma transação usando o Transact\-SQL  
  
1.  Abra um teste de unidade no Designer de Teste de Unidade do SQL Server. (Clique duas vezes no arquivo do código-fonte para o teste de unidade a ser exibido no designer.)  
  
2.  Especifique o tipo de script para o qual você deseja criar a transação. Por exemplo, você pode especificar o script de pré-teste, de teste ou de pós-teste.  
  
3.  Insira um script de teste no editor de Transact\-SQL.  
  
4.  Insira as instruções `BEGIN TRANSACTION` e `ROLLBACK TRANSACTION`, conforme mostrado neste exemplo simples. O exemplo usa uma tabela de banco de dados chamada OrderDetails que contém 50 linhas de dados:  
  
    ```  
    BEGIN TRANSACTION TestTransaction  
    UPDATE "OrderDetails" set Quantity = Quantity + 10  
    IF @@ROWCOUNT!=50  
    RAISERROR('Row count does not equal 50',16,1)  
    ROLLBACK TRANSACTION TestTransaction  
    ```  
  
    > [!NOTE]  
    > Não é possível reverter uma transação depois que a instrução COMMIT TRANSACTION é executada.  
  
    Para saber mais sobre como ROLLBACK TRANSACTION funciona com procedimentos armazenados e gatilhos, consulte esta página no site da Microsoft: [ROLLBACK TRANSACTION (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkID=115927).  
  
## <a name="to-create-a-transaction-for-a-single-test-method"></a>Para criar uma transação para um único método de teste  
Neste exemplo, você está usando uma transação de ambiente com o tipo [System.Transactions.TransactionScope](https://docs.microsoft.com/dotnet/api/system.transactions.transactionscope). Por padrão, as conexões de execução e privilegiadas não usarão a transação de ambiente, porque as conexões foram criadas antes que o método seja executado. A SqlConnection tem um método [System.Data.SqlClient.SqlConnection.EnlistTransaction](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlconnection.enlisttransaction), que associa uma conexão ativa a uma transação. Quando uma transação de ambiente é criada, ela é registrada como a transação atual, e você pode acessá-la através da propriedade [System.Transactions.Transaction.Current](https://docs.microsoft.com/dotnet/api/system.transactions.transaction.current). Neste exemplo, a transação é revertida quando a transação de ambiente é descartada. Para confirmar qualquer alteração feita durante a execução do teste de unidade, você deve chamar o método [System.Transactions.TransactionScope.Complete](https://docs.microsoft.com/dotnet/api/system.transactions.transactionscope.complete).  
  
#### <a name="to-create-a-transaction-for-a-single-test-method"></a>Para criar uma transação para um único método de teste  
  
1.  No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Referências** no projeto de teste e clique em **Adicionar Referência**.  
  
    A caixa de diálogo **Adicionar Referência** é exibida.  
  
2.  Clique na guia **.NET**.  
  
3.  Na lista de assemblies, clique em **System.Transactions** e clique em **OK**.  
  
4.  Abra o arquivo do Visual Basic ou do C# para o teste de unidade.  
  
5.  Encapsule as ações de pré-teste, teste e pós-teste conforme mostrado no seguinte exemplo de código do Visual Basic:  
  
    ```  
    <TestMethod()> _  
    Public Sub dbo_InsertTable1Test()  
  
        Using ts as New System.Transactions.TransactionScope( System.Transactions.TransactionScopeOption.Required)  
            ExecutionContext.Connection.EnlistTransaction(Transaction.Current)  
            PrivilegedContext.Connection.EnlistTransaction(Transaction.Current)  
  
            Dim testActions As DatabaseTestActions = Me.dbo_InsertTable1TestData  
            'Execute the pre-test script  
            '  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.PretestAction) Is Nothing), "Executing pre-test script...")  
            Dim pretestResults() As ExecutionResult = TestService.Execute(Me.PrivilegedContext, Me.PrivilegedContext, testActions.PretestAction)  
            'Execute the test script  
  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.TestAction) Is Nothing), "Executing test script...")  
            Dim testResults() As ExecutionResult = TestService.Execute(ExecutionContext, Me.PrivilegedContext, testActions.TestAction)  
  
            'Execute the post-test script  
            '  
            System.Diagnostics.Trace.WriteLineIf((Not (testActions.PosttestAction) Is Nothing), "Executing post-test script...")  
            Dim posttestResults() As ExecutionResult = TestService.Execute(Me.PrivilegedContext, Me.PrivilegedContext, testActions.PosttestAction)  
  
            'Because the transaction is not explicitly committed, it  
            'is rolled back when the ambient transaction is   
            'disposed.  
            'To commit the transaction, remove the comment delimiter  
            'from the following statement:  
            'ts.Complete()  
  
    End Sub  
    Private dbo_InsertTable1TestData As DatabaseTestActions  
    ```  
  
    > [!NOTE]  
    > Se você estiver usando o Visual Basic, deverá adicionar `Imports System.Transactions` (além de `Imports Microsoft.VisualStudio.TestTools.UnitTesting`, `Imports Microsoft.VisualStudio.TeamSystem.Data.UnitTesting` e `Imports Microsoft.VisualStudio.TeamSystem.Data.UnitTest.Conditions`). Se você estiver usando o Visual C#, deverá adicionar `using System.Transactions` (além das instruções `using` para Microsoft.VisualStudio.TestTools, Microsoft.VisualStudio.TeamSystem.Data.UnitTesting e Microsoft.VisualStudio.TeamSystem.Data.UnitTesting.Conditions). Você também deve adicionar uma referência ao projeto a esses assemblies.  
  
## <a name="to-create-a-transaction-for-all-test-methods-in-a-test-class"></a>Para criar uma transação para todos os métodos de teste em uma classe de teste  
  
#### <a name="to-create-a-transaction-for-all-test-methods-in-a-test-class"></a>Para criar uma transação para todos os métodos de teste em uma classe de teste  
  
1.  Abra o arquivo do Visual Basic ou do C# para o teste de unidade.  
  
2.  Crie a transação em TestInitialize, e descarte-a em TestCleanup, conforme mostrado no exemplo de código do Visual C #:  
  
    ```  
    TransactionScope _trans;  
  
            [TestInitialize()]  
            public void Init()  
            {  
                _trans = new TransactionScope();  
                base.InitializeTest();  
            }  
  
            [TestCleanup()]  
            public void Cleanup()  
            {  
                base.CleanupTest();  
                _trans.Dispose();  
            }  
  
            [TestMethod()]  
            public void TransactedTest()  
            {  
                DatabaseTestActions testActions = this.DatabaseTestMethod1Data;  
                // Execute the pre-test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.PretestAction != null), "Executing pre-test script...");  
                ExecutionResult[] pretestResults = TestService.Execute(this.PrivilegedContext, this.PrivilegedContext, testActions.PretestAction);  
                // Execute the test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.TestAction != null), "Executing test script...");  
                ExecutionResult[] testResults = TestService.Execute(this.ExecutionContext, this.PrivilegedContext, testActions.TestAction);  
                // Execute the post-test script  
                //   
                System.Diagnostics.Trace.WriteLineIf((testActions.PosttestAction != null), "Executing post-test script...");  
                ExecutionResult[] posttestResults = TestService.Execute(this.PrivilegedContext, this.PrivilegedContext, testActions.PosttestAction);  
  
            }  
    ```  
  
## <a name="to-start-the-distributed-transaction-coordinator-service"></a>Para iniciar o serviço Coordenador de Transações Distribuídas  
Alguns procedimentos deste tópico usam os tipos do assembly System.Transactions. Antes de executar estes procedimentos, verifique se o serviço Coordenador de Transações Distribuídas está em execução no computador em que os testes de unidade são executados. Do contrário, o teste apresentará falha, e a seguinte mensagem de erro será exibida: "O método de teste *ProjectName*.*TestName*.*MethodName* lançou a exceção: System.Data.SqlClient.SqlException: MSDTC no servidor '*ComputerName*' não está disponível".  
  
#### <a name="to-start-the-distributed-transaction-coordinator-service"></a>Para iniciar o serviço Coordenador de Transações Distribuídas  
  
1.  Abra o **Painel de Controle**.  
  
2.  No **Painel de Controle**, abra **Ferramentas Administrativas**.  
  
3.  Em **Ferramentas Administrativas**, abra **Serviços**.  
  
4.  No painel **Serviços**, clique com o botão direito do mouse no serviço **Controlador de Transação Distribuída** e clique em **Iniciar**.  
  
    O status do serviço deve ser atualizado para **Iniciado**. Agora você poderá executar testes de unidade que usam System.Transactions.  
  
> [!IMPORTANT]  
> O erro a seguir pode aparecer, mesmo se você tiver iniciado o serviço Controlador de Transação Distribuída: `System.Transactions.TransactionManagerCommunicationException: Network access for Distributed Transaction Manager (MSDTC) has been disabled. Please enable DTC for network access in the security configuration for MSDTC using the Component Services Administrative tool. ---> System.Runtime.InteropServices.COMException: The transaction manager has disabled its support for remote/network transactions. (Exception from HRESULT: 0x8004D024)`. Se esse erro aparecer, você deverá configurar o Controlador de Transação Distribuída para acesso à rede. Para saber mais, confira [Habilitar acesso do DTC à rede](http://go.microsoft.com/fwlink/?LinkId=193916).  
  
## <a name="see-also"></a>Consulte Também  
[Criando e definindo testes de unidade do SQL Server](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
  
