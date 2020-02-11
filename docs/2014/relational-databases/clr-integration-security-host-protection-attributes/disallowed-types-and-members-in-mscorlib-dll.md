---
title: Tipos e membros não permitidos em mscorlib. dll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: daf82d4b-2f6d-44ca-9148-75193321b6d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 43f71d7dc73239b240b841e14a11f3f28f755b61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874361"
---
# <a name="disallowed-types-and-members-in-mscorlibdll"></a>Membros e tipos não permitidos em mscorlib.dll
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a programação comum de integração de linguagem (CLR) não permite o uso de um tipo ou membro que `HostProtectionAttribute` tenha um que `System.Security.Permissions.HostProtectionResource` especifique uma enumeração com um `ExternalProcessMgmt`valor `ExternalThreading`de `MayLeakOnAbort`, `SecurityInfrastructure`, `SelfAffectingProcessMgmnt`, `SelfAffectingThreading`, ****,, `Synchronization`SharedState, `UI`ou. A tabela a seguir lista os membros e tipos do assembly mscorlib.dll cujos valores de HPA (atributo de proteção de host) não são permitidos.  
  
> [!NOTE]  
>  Esta lista foi gerada dos assembly com suporte. Para obter mais informações, consulte [bibliotecas de .NET Framework com suporte](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo ou membro|Valor(es) de HPA|  
|--------------------|--------------------|  
|SyncStream.BeginRead()|ExternalThreading|  
|SyncStream.BeginWrite ()|ExternalThreading|  
|System.Collections.ArrayList.Synchronized()|Synchronization|  
|System.Collections.Hashtable.Synchronized()|Synchronization|  
|System.Collections.Queue.Synchronized()|Synchronization|  
|System.Collections.SortedList.Synchronized()|Synchronization|  
|System.Collections.Stack.Synchronized()|Synchronization|  
|System.Console.Beep()|Interface do usuário|  
|System.Console.get_Error()|Interface do usuário|  
|System.Console.get_In()|Interface do usuário|  
|System.Console.get_KeyAvailable()|Interface do usuário|  
|System.Console.get_Out()|Interface do usuário|  
|System.Console.OpenStandardError()|Interface do usuário|  
|System.Console.OpenStandardInput()|Interface do usuário|  
|System.Console.OpenStandardOutput()|Interface do usuário|  
|System.Console.Read()|Interface do usuário|  
|System.Console.ReadKey()|Interface do usuário|  
|System.Console.ReadLine()|Interface do usuário|  
|System.Console.SetError()|Interface do usuário|  
|System.Console.SetIn()|Interface do usuário|  
|System.Console.SetOut()|Interface do usuário|  
|System.Console.Write()|Interface do usuário|  
|System.Console.WriteLine()|Interface do usuário|  
|System.Diagnostics.LogMessageEventHandler|ExternalThreading, Synchronization|  
|System.IO.FileStream.BeginRead()|ExternalThreading|  
|System.IO.FileStream.BeginWrite()|ExternalThreading|  
|System.IO.Stream.Synchronized()|Synchronization|  
|System.IO.TextReader.Synchronized()|Synchronization|  
|System.IO.TextWriter.Synchronized()|Synchronization|  
|System.Reflection.Emit.AssemblyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.ConstructorBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.CustomAttributeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EnumBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EventBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.FieldBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodRental|MayLeakOnAbort|  
|System.Reflection.Emit.ModuleBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.PropertyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.TypeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.UnmanagedMarshal|MayLeakOnAbort|  
|System.Security.Principal.WindowsPrincipal|SecurityInfrastructure|  
|System.Threading.AutoResetEvent|ExternalThreading, Synchronization|  
|System.Threading.EventWaitHandle|ExternalThreading, Synchronization|  
|System.Threading.ManualResetEvent|ExternalThreading, Synchronization|  
|System.Threading.Monitor|ExternalThreading, Synchronization|  
|System.Threading.Mutex|ExternalThreading, Synchronization|  
|System.Threading.ReaderWriterLock|ExternalThreading, Synchronization|  
|System.Threading.Thread.AllocateDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.AllocateNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.BeginCriticalRegion()|ExternalThreading, Synchronization|  
|System.Threading.Thread.EndCriticalRegion()|ExternalThreading, Synchronization|  
|System.Threading.Thread.FreeNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.GetData()|ExternalThreading, SharedState|  
|System.Threading.Thread.GetNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.Join()|ExternalThreading, Synchronization|  
|System.Threading.Thread.set_ApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.Thread.set_CurrentUICulture()|ExternalThreading|  
|System.Threading.Thread.set_IsBackground()|SelfAffectingThreading|  
|System.Threading.Thread.set_Name()|ExternalThreading|  
|System.Threading.Thread.set_Priority()|SelfAffectingThreading|  
|System.Threading.Thread.SetApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.Thread.SetData()|ExternalThreading, SharedState|  
|System.Threading.Thread.SpinWait()|ExternalThreading, Synchronization|  
|System.Threading.Thread.Start()|ExternalThreading, Synchronization|  
|System.Threading.Thread.TrySetApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.ThreadPool|ExternalThreading, Synchronization|  
|System.Threading.Timer|ExternalThreading, Synchronization|  
|System.Threading.TimerBase|ExternalThreading, Synchronization|  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos de proteção do host e programação de integração CLR](host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos e membros não permitidos em Microsoft. VisualBasic. dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos e membros não permitidos em System. dll](disallowed-types-and-members-in-system-dll.md)   
 [Tipos e membros não permitidos em System. Data. dll](disallowed-types-and-members-in-system-data-dll.md)   
 [Tipos e membros desaprovados no System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
  
  
