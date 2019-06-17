---
title: Objeto SqlContext | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 223111874ca34ba4df4968c550e6cc47edf2b390
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920050"
---
# <a name="sqlcontext-object"></a>Objeto SqlContext
  O código gerenciado é invocado no servidor quando você chama um procedimento ou uma função, quando chama um método em um tipo CLR (Common Language Runtime) definido pelo usuário ou quando sua ação dispara um gatilho definido em qualquer das linguagens do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Como a execução desse código é exigida como parte de uma conexão de usuário, o acesso ao contexto do chamador a partir do código em execução no servidor é necessário. Além disso, determinadas operações de acesso a dados podem ser válidas somente se executadas no contexto do chamador. Por exemplo, o acesso a pseudotabelas inseridas e excluídas usadas em operações de gatilho será válido somente no contexto do chamador.  
  
 O contexto do chamador é abstraído em um objeto `SqlContext`. Para obter mais informações sobre os métodos e as propriedades `SqlTriggerContext`, consulte a documentação de referência da classe `Microsoft.SqlServer.Server.SqlTriggerContext` no SDK do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 `SqlContext` fornece acesso aos seguintes componentes:  
  
-   `SqlPipe`: O `SqlPipe` objeto representa o "pipe" por meio do qual os resultados fluem para o cliente. Para obter mais informações sobre o `SqlPipe` do objeto, consulte [objeto SqlPipe](sqlpipe-object.md).  
  
-   `SqlTriggerContext`: O `SqlTriggerContext` objeto só pode ser recuperado de dentro um gatilho CLR. Ele fornece informações sobre a operação que fez o gatilho ser acionado e um mapa das colunas que foram atualizadas. Para obter mais informações sobre o `SqlTriggerContext` do objeto, consulte [objeto SqlTriggerContext](sqltriggercontext-object.md).  
  
-   `IsAvailable`: O `IsAvailable` propriedade é usada para determinar a disponibilidade de contexto.  
  
-   `WindowsIdentity`: O `WindowsIdentity` propriedade é usada para recuperar a identidade do Windows do chamador.  
  
## <a name="determining-context-availability"></a>Determinando a disponibilidade de contexto  
 Consulte a classe `SqlContext` para ver se o código em execução no momento está sendo executado em processo. Para fazer isso, verifique a propriedade `IsAvailable` do objeto `SqlContext`. A propriedade `IsAvailable` é somente leitura e retornará `True` se o código de chamada estiver em execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se outros membros de `SqlContext` puderem ser acessados. Se a propriedade `IsAvailable` retornar `False`, todos os outros membros de `SqlContext` lançarão um `InvalidOperationException`, se usado. Se `IsAvailable` retornar `False`, qualquer tentativa de abrir um objeto de conexão que tem "context connection=true" na cadeia de conexão falhará.  
  
## <a name="retrieving-windows-identity"></a>Recuperando a identidade do Windows  
 O código CLR em execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre é invocado no contexto da conta de processo. Se o código deve executar determinadas ações usando a identidade do usuário que fez a chamada em vez da identidade de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um token de representação deve ser obtido por meio da propriedade `WindowsIdentity` do objeto `SqlContext`. A propriedade `WindowsIdentity` retorna uma instância `WindowsIdentity` que representa a identidade do [!INCLUDE[msCoName](../../includes/msconame-md.md)] do chamador ou que é nula, se o cliente foi autenticado usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Outros assemblies marcados com `EXTERNAL_ACCESS` ou permissões `UNSAFE` podem acessar esta propriedade.  
  
 Depois de obter o objeto `WindowsIdentity`, os chamadores podem representar a conta de cliente e executar ações em seu nome.  
  
 A identidade do chamador está disponível por meio de `SqlContext.WindowsIdentity` somente se o cliente que iniciou a execução do procedimento armazenado ou da função se conectou ao servidor usando a Autenticação do Windows. Se, em vez disso, a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi usada, essa propriedade será nula e o código não poderá representar o chamador.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como obter a identidade do Windows do cliente que fez a chamada e representar o cliente.  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto SqlPipe](sqlpipe-object.md)   
 [Objeto SqlTriggerContext](sqltriggercontext-object.md)   
 [Gatilhos CLR](../../database-engine/dev-guide/clr-triggers.md)   
 [Extensões específicas em processo do SQL Server para o ADO.NET](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
