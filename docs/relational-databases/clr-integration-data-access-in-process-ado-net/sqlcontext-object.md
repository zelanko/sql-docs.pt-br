---
title: SqlContext Object | Microsoft Docs
description: Quando você invoca código gerenciado no SQL Server em uma conexão de usuário, o acesso ao contexto do chamador é abstraído em um objeto SqlContext.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: cd6d3091b155ae829e368bdd182b3da8286c7194
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487527"
---
# <a name="sqlcontext-object"></a>Objeto SqlContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O código gerenciado é invocado no servidor quando você chama um procedimento ou uma função, quando chama um método em um tipo CLR (Common Language Runtime) definido pelo usuário ou quando sua ação dispara um gatilho definido em qualquer das linguagens do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Como a execução desse código é exigida como parte de uma conexão de usuário, o acesso ao contexto do chamador a partir do código em execução no servidor é necessário. Além disso, determinadas operações de acesso a dados podem ser válidas somente se executadas no contexto do chamador. Por exemplo, o acesso a pseudotabelas inseridas e excluídas usadas em operações de gatilho será válido somente no contexto do chamador.  
  
 O contexto do chamador é abstrato em um objeto **SqlContext.** Para obter mais informações sobre os métodos e propriedades **do SqlTriggerContext,** consulte a documentação de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] referência da classe **Microsoft.SqlServer.Server.SqlTriggerContext** no SDK.  
  
 **O SqlContext** fornece acesso aos seguintes componentes:  
  
-   **SqlPipe**: O objeto **SqlPipe** representa o "tubo" através do qual os resultados fluem para o cliente. Para obter mais informações sobre o objeto **SqlPipe,** consulte [SqlPipe Object](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext**: O objeto **SqlTriggerContext** só pode ser recuperado dentro de um gatilho CLR. Ele fornece informações sobre a operação que fez o gatilho ser acionado e um mapa das colunas que foram atualizadas. Para obter mais informações sobre o objeto **SqlTriggerContext,** consulte [SqlTriggerContext Object](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **IsAvailable**: A propriedade **IsAvailable** é usada para determinar a disponibilidade do contexto.  
  
-   **WindowsIdentity**: A propriedade **WindowsIdentity** é usada para recuperar a identidade do Windows do chamador.  
  
## <a name="determining-context-availability"></a>Determinando a disponibilidade de contexto  
 Consulte a classe **SqlContext** para ver se o código de execução está sendo executado no processo. Para fazer isso, verifique a propriedade **IsAvailable** do objeto **SqlContext.** A propriedade **IsAvailable** é somente leitura e retorna **True** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o código de chamada estiver sendo executado no interior e se outros membros **do SqlContext** puderem ser acessados. Se a propriedade **IsAvailable** retornar **falsa,** todos os outros membros **do SqlContext** jogarão uma **InvalidOperationException**, se usada. Se **IsAvailable retorna** **Falso,** qualquer tentativa de abrir um objeto de conexão que tenha "context connection=true" na seqüência de conexões falha.  
  
## <a name="retrieving-windows-identity"></a>Recuperando a identidade do Windows  
 O código CLR em execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre é invocado no contexto da conta de processo. Se o código executar certas ações usando a identidade [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do usuário de chamada, em vez da identidade do processo, então um token de representação deve ser obtido através da propriedade **WindowsIdentity** do objeto **SqlContext.** A propriedade **WindowsIdentity** retorna uma instância [!INCLUDE[msCoName](../../includes/msconame-md.md)] **do WindowsIdentity** representando a identidade do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do chamador ou nula se o cliente foi autenticado usando autenticação. Somente conjuntos marcados com **permissões EXTERNAL_ACCESS** ou **INSEGURAS** podem acessar esta propriedade.  
  
 Depois de obter o objeto **WindowsIdentity,** os chamadores podem se passar pela conta do cliente e executar ações em seu nome.  
  
 A identidade do chamador só está disponível através **do SqlContext.WindowsIdentity** se o cliente que iniciou a execução do procedimento armazenado ou função estiver conectado ao servidor usando a Autenticação do Windows. Se, em vez disso, a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi usada, essa propriedade será nula e o código não poderá representar o chamador.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Objeto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTriggerContext Object](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [Gatilhos CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [Extensões específicas em processo do SQL Server para o ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
