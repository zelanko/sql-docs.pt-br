---
title: Objeto SqlContext | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
caps.latest.revision: "54"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 70a25a1b656e20ff7d2457df581a3a1b94ee3b9a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sqlcontext-object"></a>Objeto SqlContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Chamar código gerenciado no servidor quando você chamar um procedimento ou função, quando você chama um método em um tipo common language runtime (CLR) definidos pelo usuário, ou quando sua ação dispara um gatilho definido em qualquer um do [!INCLUDE[msCoName](../../includes/msconame-md.md)] linguagens do .NET Framework. Como a execução desse código é exigida como parte de uma conexão de usuário, o acesso ao contexto do chamador a partir do código em execução no servidor é necessário. Além disso, determinadas operações de acesso a dados podem ser válidas somente se executadas no contexto do chamador. Por exemplo, o acesso a pseudotabelas inseridas e excluídas usadas em operações de gatilho será válido somente no contexto do chamador.  
  
 O contexto do chamador é abstraído em um **SqlContext** objeto. Para obter mais informações sobre o **SqlTriggerContext** métodos e propriedades, consulte o **Microsoft.SqlServer.Server.SqlTriggerContext** documentação de referência na classe de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
 **SqlContext** fornece acesso para os seguintes componentes:  
  
-   **SqlPipe**: O **SqlPipe** objeto representa o "pipe" pelo qual os resultados fluem para o cliente. Para obter mais informações sobre o **SqlPipe** de objeto, consulte [objeto SqlPipe](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md).  
  
-   **SqlTriggerContext**: O **SqlTriggerContext** objeto só pode ser recuperado de dentro de um gatilho CLR. Ele fornece informações sobre a operação que fez o gatilho ser acionado e um mapa das colunas que foram atualizadas. Para obter mais informações sobre o **SqlTriggerContext** de objeto, consulte [objeto SqlTriggerContext](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md).  
  
-   **IsAvailable**: O **IsAvailable** propriedade é usada para determinar a disponibilidade de contexto.  
  
-   **WindowsIdentity**: O **WindowsIdentity** propriedade é usada para recuperar a identidade do Windows do chamador.  
  
## <a name="determining-context-availability"></a>Determinando a disponibilidade de contexto  
 Consulta o **SqlContext** classe para ver se o código em execução no momento está em execução no processo. Para fazer isso, verifique o **IsAvailable** propriedade o **SqlContext** objeto. O **IsAvailable** propriedade é somente leitura e retorna **True** se o código de chamada está em execução dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se outros **SqlContext** membros podem ser acessados. Se o **IsAvailable** propriedade retorna **False**, todas as outras **SqlContext** membros lançam um **InvalidOperationException**, se usado . Se **IsAvailable** retorna **False**, qualquer tentativa de abrir um objeto de conexão que tem "conexão de contexto = true" na cadeia de conexão falhar.  
  
## <a name="retrieving-windows-identity"></a>Recuperando a identidade do Windows  
 O código CLR em execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre é invocado no contexto da conta de processo. Se o código deve executar determinadas ações usando a identidade do usuário da chamada, em vez do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processar identidade, em seguida, um token de representação deve ser obtido por meio de **WindowsIdentity** propriedade o  **SqlContext** objeto. O **WindowsIdentity** propriedade retorna um **WindowsIdentity** instância que representa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] identidade Windows do chamador, ou nulo se o cliente foi autenticado usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticação. Somente assemblies marcados com **EXTERNAL_ACCESS** ou **UNSAFE** permissões podem acessar essa propriedade.  
  
 Depois de obter o **WindowsIdentity** do objeto, os chamadores podem representar a conta de cliente e executar ações em nome deles.  
  
 A identidade do chamador só está disponível por meio de **SqlContext.WindowsIdentity** se o cliente que iniciou a execução do procedimento armazenado ou função conectado ao servidor usando a autenticação do Windows. Se, em vez disso, a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi usada, essa propriedade será nula e o código não poderá representar o chamador.  
  
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
  
  
