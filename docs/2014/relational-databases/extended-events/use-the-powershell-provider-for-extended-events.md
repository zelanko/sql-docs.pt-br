---
title: Usar o provedor do PowerShell para Eventos Estendidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f3a1e5ed2aa8ee73ceefd0d58ddc3c1f06869be5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013337"
---
# <a name="use-the-powershell-provider-for-extended-events"></a>Usar o Provedor do PowerShell para eventos estendidos
  É possível gerenciar Eventos Estendidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do uso do provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. A subpasta XEvent está disponível sob a unidade SQLSERVER. É possível acessar a pasta por meio do uso de um dos métodos a seguir:  
  
-   Em um prompt de comando, digite `sqlps`, e pressione ENTER. Tipo `cd xevent`, e pressione ENTER. A partir daí, você pode usar o **cd** e `dir` comandos (ou **Set-Location** e **Get-Childitem** cmdlets) para navegar até o nome do servidor e o nome de instância.  
  
-   No Pesquisador de Objetos, expanda o nome de instância, expanda **Gerenciamento**, clique com o botão direito do mouse em **Eventos Estendidos**e clique em **Iniciar PowerShell**. Isso inicia o PowerShell no seguinte caminho:  
  
     PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*>  
  
    > [!NOTE]  
    >  Você pode iniciar o PowerShell em qualquer nó sob **Eventos Estendidos**. Por exemplo, você pode clicar com o botão direito do mouse em **Sessões**e clicar em **Iniciar PowerShell**. Isso inicia o PowerShell um nível mais profundo na pasta de Sessões.  
  
 Você pode procurar a árvore de pastas XEvent para exibir sessões existentes de Eventos Estendidos e os eventos, destinos e predicados correspondentes associados. Por exemplo, do SQLServer: \ PS XEvent\\*ServerName*\\*InstanceName*> caminho, se você digitar `cd sessions`, pressione ENTER, digite `dir`e, em seguida, pressionar ENTER, você pode ver a lista de sessões que estão armazenadas nessa instância. Você também pode exibir se a sessão está em execução (e nesse caso, há quanto tempo), e se a sessão está configurada para ser iniciada quando a instância for iniciada.  
  
 Para exibir os eventos, os predicados e os destinos correspondentes associados a uma sessão, você pode alterar diretórios para o nome da sessão e exibir as pastas de eventos ou de destinos. Por exemplo, para exibir os eventos e os predicados que estão associados com a sessão de integridade de sistema padrão, do SQLServer: \ PS XEvent\\*ServerName*\\*InstanceName*\Sessions> >, digite `cd system_health\events,` pressione ENTER, digite `dir`, e pressione ENTER.  
  
 O provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell é uma ferramenta avançada que pode ser usada para criar, alterar e gerenciar sessões de Eventos Estendidos. A seção a seguir fornece alguns exemplos básicos do uso de scripts do PowerShell com Eventos Estendidos.  
  
## <a name="examples"></a>Exemplos  
 Nos exemplos a seguir, observe o seguinte:  
  
-   Os scripts devem ser executados do PS SQLSERVER:\\> prompt (disponível digitando `sqlps` em um prompt de comando).  
  
-   Os scripts usam a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Os scripts devem ser salvos com uma extensão .ps1.  
  
-   A política de execução do PowerShell deve permitir que o script seja executado. Para definir a política de execução, use o cmdlet **Set-Executionpolicy** . (Para obter mais informações, digite `get-help set-executionpolicy -detailed`, e pressione ENTER.)  
  
 O script a seguir cria uma nova sessão denominada 'TestSession.'  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 O script a seguir adiciona o destino de buffer de anéis à sessão criada no exemplo anterior. (Esse exemplo mostra o uso do método `Alter`. Lembre-se de que você pode adicionar o destino ao criar a sessão pela primeira vez.)  
  
```  
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir|where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 O script a seguir cria uma nova sessão que usa uma expressão de predicado. Neste caso, a sessão coleta informações de quando o arquivo c:\temp.log é gravado (por meio do evento sqlserver.file_written).  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -argumentlist $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a>Segurança  
 Para criar, alterar ou cancelar uma sessão de Eventos Estendidos, você deve ter a permissão ALTER ANY EVENT SESSION.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)   
 [Usar a sessão de system_health](use-the-ssms-xe-profiler.md)   
 [Ferramentas de Eventos Estendidos](extended-events-tools.md)  
  
  