---
title: Adicionar suporte para depuração em uma tarefa personalizada | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BreakpointManager class
- breakpoints [Integration Services]
- custom tasks [Integration Services], debugging
- IDTSSuspend interface
- IDTSBreakpointSite interface
- SSIS custom tasks, debugging
- debugging [Integration Services], custom tasks
ms.assetid: 7f06e49b-0b60-4e81-97da-d32dc248264a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: abb30ee26f5063c4a119b13c6891b53518d63b9e
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724487"
---
# <a name="adding-support-for-debugging-in-a-custom-task"></a>Adicionando suporte para depurando em uma tarefa personalizada

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O mecanismo de tempo de execução [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] permite a suspensão de pacotes, tarefas e outros tipos de contêineres durante a execução usando pontos de interrupção. O uso de pontos de interrupção permite que você analise e corrija erros que impedem a execução adequada de seu aplicativo ou de tarefas. A arquitetura de ponto de interrupção permite ao cliente avaliar o valor do tempo de execução de objetos no pacote em pontos definidos da execução enquanto o processamento da tarefa fica suspenso.  
  
 Desenvolvedores de tarefa personalizada podem usar essa arquitetura para criar destinos de ponto de interrupção personalizados através da interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite>, e de sua interface pai, <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend>. A interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite> define a interação entre o mecanismo de tempo de execução e a tarefa para criar e gerenciar sites ou destinos de ponto de interrupção personalizados. A interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend> fornece métodos e propriedades que são chamadas pelo mecanismo de tempo de execução para notificar a tarefa para suspender ou retomar sua execução.  
  
 Um site ou destino de ponto de interrupção é um ponto na execução da tarefa onde o processamento pode ser suspenso. Usuários selecionam entre os sites de ponto de interrupção disponíveis na caixa de diálogo **Definir Pontos de Interrupção**. Por exemplo, além das opções de ponto de interrupção padrão, o Contêiner do Loop Foreach oferece a opção "Quebra no início de cada iteração do loop".  
  
 Quando uma tarefa alcança um destino de ponto de interrupção durante a execução, ela avalia esse destino para determinar se um ponto de interrupção está habilitado. Isso indica que o usuário deseja parar a execução nesse ponto de interrupção. Se o ponto de interrupção estiver habilitado, a tarefa gerará o evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnBreakpointHit%2A> para o mecanismo de tempo de execução. O mecanismo de tempo de execução responde ao evento chamando o método **Suspend** de cada tarefa que está em execução no momento no pacote. A execução da tarefa retoma quando o tempo de execução chama o método **ResumeExecution** da tarefa suspensa.  
  
 As tarefas que não usam pontos de interrupção ainda devem implementar as interfaces <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite> e <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend>. Isso garante que a tarefa será suspensa corretamente quando outros objetos do pacote gerarem eventos <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnBreakpointHit%2A>.  
  
## <a name="idtsbreakpointsite-interface-and-breakpointmanager"></a>Interface IDTSBreakpointSite e BreakpointManager  
 As tarefas criam destinos de ponto de interrupção chamando o método <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager.CreateBreakpointTarget%2A> do <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager>, fornecendo uma ID de inteiro e uma descrição de cadeia de caracteres como parâmetros. Quando a tarefa atinge o ponto em seu código que contém um destino de ponto de interrupção, ela avalia o destino de ponto de interrupção usando o método <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager.IsBreakpointTargetEnabled%2A> para determinar se esse ponto de interrupção está habilitado. Se **true**, a tarefa notifica o mecanismo de tempo de execução, gerando o evento <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnBreakpointHit%2A>.  
  
 A interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite> define um único método, <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite.AcceptBreakpointManager%2A>, que é chamado pelo mecanismo de tempo de execução durante a criação da tarefa. Esse método fornece como parâmetro o objeto <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager>, que é usado então pela tarefa para criar e gerenciar seus pontos de interrupção. As tarefas devem armazenar o <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager> localmente para uso durante os métodos **Validate** e **Execute**.  
  
 O exemplo de código a seguir demonstra como criar um destino de ponto de interrupção através do <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager>. O exemplo chama o método <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnBreakpointHit%2A> para gerar o evento.  
  
```csharp  
public void AcceptBreakpointManager( BreakpointManager breakPointManager )  
{  
   //   Store the breakpoint manager locally.  
   this.bpm  = breakPointManager;  
}  
public override DTSExecResult Execute( Connections connections,  
  Variables variables, IDTSComponentEvents events,  
  IDTSLogging log, DtsTransaction txn)  
{  
   //   Create a breakpoint.  
   this.bpm.CreateBreakPointTarget( 1 , "A sample breakpoint target." );  
...  
   if( this.bpm.IsBreakpointTargetEnabled( 1 ) == true )  
      events.OnBreakpointHit( this.bpm.GetBreakpointTarget( 1 ) );  
}  
```  
  
```vb  
Public Sub AcceptBreakpointManager(ByVal breakPointManager As BreakpointManager)  
  
   ' Store the breakpoint manager locally.  
   Me.bpm  = breakPointManager  
  
End Sub  
  
Public Overrides Function Execute(ByVal connections As Connections, _  
  ByVal variables As Variables, ByVal events As IDTSComponentEvents, _  
  ByVal log As IDTSLogging, ByVal txn As DtsTransaction) As DTSExecResult  
  
   ' Create a breakpoint.  
   Me.bpm.CreateBreakPointTarget(1 , "A sample breakpoint target.")  
  
   If Me.bpm.IsBreakpointTargetEnabled(1) = True Then  
      events.OnBreakpointHit(Me.bpm.GetBreakpointTarget(1))  
   End If  
  
End Function  
```  
  
## <a name="idtssuspend-interface"></a>Interface IDTSSuspend  
 A interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend> define os métodos que são chamados pelo mecanismo de tempo de execução quando ele pausa ou retoma a execução de uma tarefa. A interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend> é implementada pela interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite> e seus métodos **Suspend** e **ResumeExecution** costumam ser substituídos pela tarefa personalizada. Quando o mecanismo de tempo de execução recebe um evento **OnBreakpointHit** de uma tarefa, ele chama o método **Suspend** de cada tarefa em execução, notificando as tarefas que elas devem pausar. Quando o cliente retoma a execução, o mecanismo de tempo de execução chama o método **ResumeExecution** das tarefas que são suspensas.  
  
 A suspensão e a continuação da execução de tarefas envolvem a pausa e a continuação do thread de execução da tarefa. Em código gerenciado, você faz isso usando a classe **ManualResetEvent** no namespace **System.Threading** do .NET Framework.  
  
 O exemplo de código a seguir demonstra a suspensão e a continuação da execução da tarefa. Observe que o método **Execute** foi alterado do exemplo de código anterior e o thread de execução foi colocado em pausa ao acionar o ponto de interrupção.  
  
```csharp  
private ManualResetEvent m_suspended = new ManualResetEvent( true );  
private ManualResetEvent m_canExecute = new ManualResetEvent( true );  
private int   m_suspendRequired = 0;  
private int   m_debugMode = 0;  
  
public override DTSExecResult Execute( Connections connections, Variables variables, IDTSComponentEvents events, IDTSLogging log, DtsTransaction txn)  
{  
   // While a task is not executing, it is suspended.    
   // Now that we are executing,  
   // change to not suspended.  
   ChangeEvent(m_suspended, false);  
  
   // Check for a suspend before doing any work,   
   // in case the suspend and execute calls  
   // were initiated at virtually the same time.  
   CheckAndSuspend();  
   CheckAndFireBreakpoint( componentEvents, 1);  
}  
private void CheckAndSuspend()  
{  
   // Loop until we can execute.    
   // The loop is required rather than a simple If  
   // because there is a time between the return from WaitOne and the  
   // reset that we might receive another Suspend call.    
   // Suspend() will see that we are suspended  
   // and return.  So we need to rewait.  
   while (!m_canExecute.WaitOne(0, false))  
   {  
      ChangeEvent(m_suspended, true);  
      m_canExecute.WaitOne();  
      ChangeEvent(m_suspended, false);  
   }  
}  
private void CheckAndFireBreakpoint(IDTSComponentEvents events, int breakpointID)  
{  
   // If the breakpoint is enabled, fire it.  
   if (m_debugMode != 0 &&    this.bpm.IsBreakpointTargetEnabled(breakpointID))  
   {  
      //   Enter a suspend mode before firing the breakpoint.    
      //   Firing the breakpoint will cause the runtime   
      //   to call Suspend on this task.    
      //   Because we are blocked on the breakpoint,   
      //   we are suspended.  
      ChangeEvent(m_suspended, true);  
      events.OnBreakpointHit(this.bpm.GetBreakpointTarget(breakpointID));  
      ChangeEvent(m_suspended, false);  
   }  
   // Check for a suspension for two reasons:   
   //   1. If we are at a point where we could fire a breakpoint,   
   //      we are at a valid suspend point.  Even if we didn't hit a  
   //      breakpoint, the runtime may have called suspend,   
   //      so check for it.       
   //   2. Between the return from OnBreakpointHit   
   //      and the reset of the event, it is possible to have  
   //      received a suspend call from which we returned because   
   //      we were already suspended.  We need to be sure it is okay  
   //      to continue executing now.  
   CheckAndSuspend();  
}  
static void ChangeEvent(ManualResetEvent e, bool shouldSet)  
{  
   bool succeeded;  
   if (shouldSet)  
      succeeded = e.Set();  
   else  
      succeeded = e.Reset();  
  
   if (!succeeded)  
      throw new Exception("Synchronization object failed.");  
  
}  
public bool SuspendRequired  
{  
   get   {return m_suspendRequired != 0;}  
   set  
   {  
      // This lock is also taken by Suspend().    
      // Because it is possible for the package to be  
      // suspended and resumed in quick succession,   
      // this property might be set before  
      // the actual Suspend() call.    
      // Without the lock, the Suspend() might reset the canExecute  
      // event after we set it to abort the suspension.  
      lock (this)  
      {  
         Interlocked.Exchange(ref m_suspendRequired, value ? 1 : 0);  
         if (!value)  
            ResumeExecution();  
      }  
   }  
}  
public void ResumeExecution()  
{  
   ChangeEvent( m_canExecute,true );  
}  
public void Suspend()  
{  
   // This lock is also taken by the set SuspendRequired method.    
   // It prevents this call from overriding an   
   // aborted suspension.  See comments in set SuspendRequired.  
   lock (this)  
   {  
      // If a Suspend is required, do it.  
      if (m_suspendRequired != 0)  
         ChangeEvent(m_canExecute, false);  
   }  
   // We can't return from Suspend until the task is "suspended".  
   // This can happen one of two ways:   
   // the m_suspended event occurs, indicating that the execute thread  
   // has suspended, or the canExecute flag is set,   
   // indicating that a suspend is no longer required.  
   WaitHandle [] suspendOperationComplete = {m_suspended, m_canExecute};  
   WaitHandle.WaitAny(suspendOperationComplete);  
}  
```  
  
```vb  
Private m_suspended As ManualResetEvent = New ManualResetEvent(True)  
Private m_canExecute As ManualResetEvent = New ManualResetEvent(True)  
Private m_suspendRequired As Integer = 0  
Private m_debugMode As Integer = 0  
  
Public Overrides Function Execute(ByVal connections As Connections, _  
ByVal variables As Variables, ByVal events As IDTSComponentEvents, _  
ByVal log As IDTSLogging, ByVal txn As DtsTransaction) As DTSExecResult  
  
   ' While a task is not executing it is suspended.    
   ' Now that we are executing,  
   ' change to not suspended.  
   ChangeEvent(m_suspended, False)  
  
   ' Check for a suspend before doing any work,   
   ' in case the suspend and execute calls  
   ' were initiated at virtually the same time.  
   CheckAndSuspend()  
   CheckAndFireBreakpoint(componentEvents, 1)  
  
End Function  
  
Private Sub CheckAndSuspend()  
  
   ' Loop until we can execute.    
   ' The loop is required rather than a simple if  
   ' because there is a time between the return from WaitOne and the  
   ' reset that we might receive another Suspend call.    
   ' Suspend() will see that we are suspended  
   ' and return.  So we need to rewait.  
   Do While Not m_canExecute.WaitOne(0, False)  
              ChangeEvent(m_suspended, True)  
              m_canExecute.WaitOne()  
              ChangeEvent(m_suspended, False)  
   Loop  
  
End Sub  
  
Private Sub CheckAndFireBreakpoint(ByVal events As IDTSComponentEvents, _  
ByVal breakpointID As Integer)  
  
   ' If the breakpoint is enabled, fire it.  
   If m_debugMode <> 0 AndAlso Me.bpm.IsBreakpointTargetEnabled(breakpointID) Then  
              '   Enter a suspend mode before firing the breakpoint.    
              '   Firing the breakpoint will cause the runtime   
              '   to call Suspend on this task.    
              '   Because we are blocked on the breakpoint,   
              '   we are suspended.  
              ChangeEvent(m_suspended, True)  
              events.OnBreakpointHit(Me.bpm.GetBreakpointTarget(breakpointID))  
              ChangeEvent(m_suspended, False)  
   End If  
  
   ' Check for a suspension for two reasons:   
   '   1. If we are at a point where we could fire a breakpoint,   
   '         we are at a valid suspend point.  Even if we didn't hit a  
   '         breakpoint, the runtime may have called suspend,   
   '         so check for it.     
   '   2. Between the return from OnBreakpointHit   
   '         and the reset of the event, it is possible to have  
   '         received a suspend call from which we returned because   
   '         we were already suspended.  We need to be sure it is okay  
   '         to continue executing now.  
   CheckAndSuspend()  
  
End Sub  
  
Shared Sub ChangeEvent(ByVal e As ManualResetEvent, ByVal shouldSet As Boolean)  
  
   Dim succeeded As Boolean  
   If shouldSet Then  
              succeeded = e.Set()  
   Else  
              succeeded = e.Reset()  
   End If  
  
   If (Not succeeded) Then  
              Throw New Exception("Synchronization object failed.")  
   End If  
  
End Sub  
  
Public Property SuspendRequired() As Boolean  
   Get  
               Return m_suspendRequired <> 0  
  End Get  
  Set  
    ' This lock is also taken by Suspend().    
     '   Because it is possible for the package to be  
     '   suspended and resumed in quick succession,   
     '   this property might be set before  
     '   the actual Suspend() call.    
     '   Without the lock, the Suspend() might reset the canExecute  
     '   event after we set it to abort the suspension.  
              SyncLock Me  
                         Interlocked.Exchange(m_suspendRequired,IIf(Value, 1, 0))  
                         If (Not Value) Then  
                                    ResumeExecution()  
                         End If  
              End SyncLock  
   End Set  
End Property  
  
Public Sub ResumeExecution()  
   ChangeEvent(m_canExecute,True)  
End Sub  
  
Public Sub Suspend()  
  
   ' This lock is also taken by the set SuspendRequired method.    
   ' It prevents this call from overriding an   
   ' aborted suspension.  See comments in set SuspendRequired.  
   SyncLock Me  
   ' If a Suspend is required, do it.  
              If m_suspendRequired <> 0 Then  
                         ChangeEvent(m_canExecute, False)  
              End If  
   End SyncLock  
   ' We can't return from Suspend until the task is "suspended".  
   ' This can happen one of two ways:   
   ' the m_suspended event occurs, indicating that the execute thread  
   ' has suspended, or the canExecute flag is set,   
   ' indicating that a suspend is no longer required.  
   Dim suspendOperationComplete As WaitHandle() = {m_suspended, m_canExecute}  
   WaitHandle.WaitAny(suspendOperationComplete)  
  
End Sub  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Depurando o fluxo de controle](../../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  
