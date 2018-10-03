---
title: Objeto SqlContext | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c14003652db37ca23addd2ac0dfd14ca0ada9f00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825284"
---
# <a name="sqlcontext-object"></a>Objeto SqlContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O código gerenciado é invocado no servidor quando você chama um procedimento ou uma função, quando chama um método em um tipo CLR (Common Language Runtime) definido pelo usuário ou quando sua ação dispara um gatilho definido em qualquer das linguagens do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Como a execução desse código é exigida como parte de uma conexão de usuário, o acesso ao contexto do chamador a partir do código em execução no servidor é necessário. Além disso, determinadas operações de acesso a dados podem ser válidas somente se executadas no contexto do chamador. Por exemplo, o acesso a pseudotabelas inseridas e excluídas usadas em operações de gatilho será válido somente no contexto do chamador.  
  
 O contexto do chamador é abstraído em um **SqlContext** objeto. Para obter mais informações sobre o **SqlTriggerContext** métodos e propriedades, consulte o **Microsoft.SqlServer.Server.SqlTriggerContext** documentação de referência na classe de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** fornece acesso para os seguintes componentes:  
  
-   **SqlPipe**: O **SqlPipe** objeto representa o "pipe" por meio do qual os resultados fluem para o cliente. Para obter mais informações sobre o **SqlPipe** do objeto, consulte [objeto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext**: O **SqlTriggerContext** objeto só pode ser recuperado de dentro um gatilho CLR. Ele fornece informações sobre a operação que fez o gatilho ser acionado e um mapa das colunas que foram atualizadas. Para obter mais informações sobre o **SqlTriggerContext** do objeto, consulte [objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **IsAvailable**: O **IsAvailable** propriedade é usada para determinar a disponibilidade de contexto.  
  
-   **WindowsIdentity**: O **WindowsIdentity** propriedade é usada para recuperar a identidade do Windows do chamador.  
  
## <a name="determining-context-availability"></a>Determinando a disponibilidade de contexto  
 Consulta de **SqlContext** classe para ver se o código em execução no momento está em execução no processo. Para fazer isso, verifique as **IsAvailable** propriedade da **SqlContext** objeto. O **IsAvailable** propriedade é somente leitura e retorna **verdadeiro** se o código de chamada está em execução dentro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se outros **SqlContext** membros podem ser acessados. Se o **IsAvailable** propriedade retorna **falso**, todos os outros **SqlContext** membros lançar um **InvalidOperationException**, se usado . Se **IsAvailable** retorna **falso**, qualquer tentativa de abrir um objeto de conexão que tem "conexão de contexto = true" na cadeia de conexão falhará.  
  
## <a name="retrieving-windows-identity"></a>Recuperando a identidade do Windows  
 O código CLR em execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre é invocado no contexto da conta de processo. Se o código deve executar determinadas ações usando a identidade do usuário da chamada, em vez do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processar identidade, em seguida, um token de representação deve ser obtido por meio de **WindowsIdentity** propriedade o  **SqlContext** objeto. O **WindowsIdentity** propriedade retorna um **WindowsIdentity** instância que representa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] identidade Windows do chamador, ou nulo se o cliente foi autenticado usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticação. Somente assemblies marcados com **EXTERNAL_ACCESS** ou **UNSAFE** permissões podem acessar essa propriedade.  
  
 Depois de obter o **WindowsIdentity** do objeto, os chamadores podem representar a conta de cliente e executar ações em seu nome.  
  
 A identidade do chamador só está disponível por meio **Sqlcontext** se o cliente que iniciou a execução do procedimento armazenado ou da função conectado ao servidor usando a autenticação do Windows. Se, em vez disso, a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi usada, essa propriedade será nula e o código não poderá representar o chamador.  
  
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
 [Objeto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [Objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [Gatilhos CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [Extensões específicas em processo do SQL Server para o ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
