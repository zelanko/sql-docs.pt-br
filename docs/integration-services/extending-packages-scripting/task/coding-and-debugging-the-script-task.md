---
title: Codificando e depurando a tarefa Script | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], debugging
- SSIS Script task, development environment
- SSIS Script task, debugging
- Script task [Integration Services], development environment
- Script task [Integration Services], coding
- debugging [Integration Services], scripts
- VSTA
- SSIS Script task, coding
ms.assetid: 687c262f-fcab-42e8-92ae-e956f3d92d69
caps.latest.revision: 81
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8c706fc1db3e31130a7754b9e4c3d16f9a13eaf4
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="coding-and-debugging-the-script-task"></a>Codificando e depurando a tarefa Script
  Depois de configurar o Script de tarefas no **Editor da tarefa Script**, você escreve seu código personalizado no ambiente de desenvolvimento de tarefa de Script.  
  
## <a name="script-task-development-environment"></a>Ambiente de desenvolvimento da tarefa Script  
 A tarefa Script usa [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) como o ambiente de desenvolvimento do próprio script.  
  
 O código de Script é escrito em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic ou em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Especifique a linguagem de script definindo a **ScriptLanguage** propriedade o **Editor da tarefa Script**. Caso prefira usar outra linguagem de programação, você pode desenvolver um assembly personalizado na linguagem de sua escolha e chamar sua funcionalidade a partir do código na tarefa Script.  
  
 O script criado na tarefa Script é armazenado na definição do pacote. Não há arquivo de script separado. Portanto, o uso da tarefa Script não afeta a implantação do pacote.  
  
> [!NOTE]  
>  Quando você projeta o pacote e depura o script, o código de script é gravado temporariamente em um arquivo de projeto. Como o fato de armazenar informações confidenciais em um arquivo é um risco em potencial à segurança, recomendamos não incluir informações confidenciais, como senhas, no código de script.  
  
 Por padrão, **Option Strict** está desabilitado no IDE.  
  
## <a name="script-task-project-structure"></a>Estrutura do projeto da tarefa Script  
 Quando você cria ou modifica o script contido em uma tarefa Script, o VSTA abre um novo projeto vazio ou reabre o projeto existente. A criação desse projeto VSTA não afeta a implantação do pacote, pois o projeto é salvo dentro do arquivo de pacote; a tarefa Script não cria arquivos adicionais.  
  
### <a name="project-items-and-classes-in-the-script-task-project"></a>Itens e classes de projeto no projeto da tarefa Script  
 Por padrão, o projeto da tarefa Script exibido na janela do Explorador de projeto VSTA contém um único item, **ScriptMain**. O **ScriptMain** item, por sua vez, contém uma única classe, também denominada **ScriptMain**. Os elementos de código na classe variam de acordo com a linguagem de programação selecionada para a tarefa Script:  
  
-   Quando a tarefa de Script é configurada para o [!INCLUDE[vb_orcas_long](../../../includes/vb-orcas-long-md.md)] linguagem de programação, o **ScriptMain** classe tem uma sub-rotina pública, **principal**. O **ScriptMain.Main** sub-rotina é o método que o tempo de execução chama quando você executar a tarefa de Script.  
  
     Por padrão, o código somente o **principal** sub-rotina de um novo script é a linha `Dts.TaskResult = ScriptResults.Success`. Essa linha informa o tempo de execução em que a tarefa teve êxito em sua operação. O **Dts.TaskResult** propriedade é abordada em [retornando resultados da tarefa Script](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md).  
  
-   Quando a tarefa de Script é configurada para o Visual c# linguagem de programação, o **ScriptMain** classe tem um método público, **principal**. O método é chamado quando a tarefa Script é executada.  
  
     Por padrão, o **principal** método inclui a linha `Dts.TaskResult = (int)ScriptResults.Success`. Essa linha informa o tempo de execução em que a tarefa teve êxito em sua operação.  
  
 O **ScriptMain** item pode conter classes que o **ScriptMain** classe. Classes só estão disponíveis à tarefa Script na qual elas residem.  
  
 Por padrão, o **ScriptMain** item de projeto contém o seguinte código gerado automaticamente. O modelo de código também fornece uma visão geral da tarefa Script e informações adicionais sobre como recuperar e manipular objetos SSIS, como variáveis, eventos e conexões.  
  
```vb  
' Microsoft SQL Server Integration Services Script Task  
' Write scripts using Microsoft Visual Basic 2008.  
' The ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Runtime.VSTAProxy  
  
<System.AddIn.AddIn("ScriptMain", Version:="1.0", Publisher:="", Description:="")> _  
Partial Class ScriptMain  
  
Private Sub ScriptMain_Startup(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Startup  
  
End Sub  
  
Private Sub ScriptMain_Shutdown(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Shutdown  
Try  
' Unlock variables from the read-only and read-write variable collection properties  
If (Dts.Variables.Count <> 0) Then  
Dts.Variables.Unlock()  
End If  
Catch ex As Exception  
        End Try  
End Sub  
  
Enum ScriptResults  
Success = DTSExecResult.Success  
Failure = DTSExecResult.Failure  
End Enum  
  
' The execution engine calls this method when the task executes.  
' To access the object model, use the Dts property. Connections, variables, events,  
' and logging features are available as members of the Dts property as shown in the following examples.  
'  
' To reference a variable, call Dts.Variables("MyCaseSensitiveVariableName").Value  
' To post a log entry, call Dts.Log("This is my log text", 999, Nothing)  
' To fire an event, call Dts.Events.FireInformation(99, "test", "hit the help message", "", 0, True)  
'  
' To use the connections collection use something like the following:  
' ConnectionManager cm = Dts.Connections.Add("OLEDB")  
' cm.ConnectionString = "Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;"  
'  
' Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.  
'   
' To open Help, press F1.  
  
Public Sub Main()  
'  
' Add your code here  
'  
Dts.TaskResult = ScriptResults.Success  
End Sub  
  
End Class  
```  
  
```csharp  
/*  
   Microsoft SQL Server Integration Services Script Task  
   Write scripts using Microsoft Visual C# 2008.  
   The ScriptMain is the entry point class of the script.  
*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime.VSTAProxy;  
using System.Windows.Forms;  
  
namespace ST_1bcfdbad36d94f8ba9f23a10375abe53.csproj  
{  
    [System.AddIn.AddIn("ScriptMain", Version = "1.0", Publisher = "", Description = "")]  
    public partial class ScriptMain  
    {  
        private void ScriptMain_Startup(object sender, EventArgs e)  
        {  
  
        }  
  
        private void ScriptMain_Shutdown(object sender, EventArgs e)  
        {  
            try  
            {  
                // Unlock variables from the read-only and read-write variable collection properties  
                if (Dts.Variables.Count != 0)  
                {  
                    Dts.Variables.Unlock();  
                }  
            }  
            catch  
            {  
            }  
        }  
  
        #region VSTA generated code  
        private void InternalStartup()  
        {  
            this.Startup += new System.EventHandler(ScriptMain_Startup);  
            this.Shutdown += new System.EventHandler(ScriptMain_Shutdown);  
        }  
        enum ScriptResults  
        {  
            Success = DTSExecResult.Success,  
            Failure = DTSExecResult.Failure  
        };  
  
        #endregion  
  
        /*  
The execution engine calls this method when the task executes.  
To access the object model, use the Dts property. Connections, variables, events,  
and logging features are available as members of the Dts property as shown in the following examples.  
  
To reference a variable, call Dts.Variables["MyCaseSensitiveVariableName"].Value;  
To post a log entry, call Dts.Log("This is my log text", 999, null);  
To fire an event, call Dts.Events.FireInformation(99, "test", "hit the help message", "", 0, true);  
  
To use the connections collection use something like the following:  
ConnectionManager cm = Dts.Connections.Add("OLEDB");  
cm.ConnectionString = "Data Source=localhost;Initial Catalog=AdventureWorks;Provider=SQLNCLI10;Integrated Security=SSPI;Auto Translate=False;";  
  
Before returning from this method, set the value of Dts.TaskResult to indicate success or failure.  
  
To open Help, press F1.  
*/  
  
        public void Main()  
        {  
            // TODO: Add your code here  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
    }  
```  
  
### <a name="additional-project-items-in-the-script-task-project"></a>Itens de projeto adicionais no projeto da tarefa Script  
 O projeto da tarefa Script pode incluir itens que não seja o padrão **ScriptMain** item. Você pode adicionar classes, módulos e arquivos de código ao projeto. Você também pode usar pastas para organizar grupos de itens. Todos os itens que você adiciona persistem dentro do pacote.  
  
### <a name="references-in-the-script-task-project"></a>Referências no projeto da tarefa Script  
 Você pode adicionar referências a assemblies gerenciados clicando com o projeto da tarefa Script no **Explorador de projeto**e, em seguida, clicando em **adicionar referência**. Para obter mais informações, consulte [referenciando outros Assemblies em soluções de script](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md).  
  
> [!NOTE]  
>  Você pode exibir as referências do projeto no VSTA IDE em **exibição de classe** ou **Explorador de projeto**. Abrir uma dessas janelas do **exibição** menu. Você pode adicionar uma nova referência do **projeto** menu de **Explorador de projeto**, ou de **exibição de classe**.  
  
## <a name="interacting-with-the-package-in-the-script-task"></a>Interagindo com o pacote na tarefa Script  
 A tarefa Script usa global **Dts** objeto, que é uma instância do <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> classe e seus membros para interagir com o pacote de conteúdo e o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] em tempo de execução.  
  
 A tabela a seguir lista os membros públicos principais do <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> classe, que é exposta ao código da tarefa de Script por meio de global **Dts** objeto. Os tópicos dessa seção apresentam uma discussão detalhada sobre o uso desses membros.  
  
|Membro|Finalidade|  
|------------|-------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>|Fornece acesso a gerenciadores de conexões definidos no pacote.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>|Fornece uma interface de eventos para deixar a tarefa Script gerar erros, avisos e mensagens informativas.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>|Fornece uma maneira simple de retornar um único objeto no tempo de execução (além de **TaskResult**) que também pode ser usado para a ramificação do fluxo de trabalho.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>|Registra informações tais como o progresso da tarefa e resultados para provedores de log habilitados.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>|Reporta o êxito ou falha da tarefa.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Transaction%2A>|Fornece a transação, caso exista, dentro da qual o contêiner da tarefa está em execução.|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>|Fornece acesso às variáveis listadas no **ReadOnlyVariables** e **ReadWriteVariables** propriedades para uso dentro do script de tarefas.|  
  
 A classe <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> também contém alguns membros públicos que você provavelmente não usará.  
  
|Membro|Description|  
|------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>|A propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> fornece acesso mais conveniente a variáveis. Embora você possa usar o <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.VariableDispenser%2A>, chame explicitamente métodos para bloquear e desbloquear variáveis para leitura e gravação. A tarefa Script trata de semânticas de bloqueio quando você usa a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>.|  
  
## <a name="debugging-the-script-task"></a>Depurando a tarefa Script  
 Para depurar o código na sua tarefa Script, defina pelo menos um ponto de interrupção no código e, depois, feche o VSTA IDE para executar o pacote no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Quando a execução do pacote insere a tarefa Script, o VSTA IDE é reaberto e exibe seu código em modo somente leitura. Depois que a execução atingir seu ponto de interrupção, você poderá examinar valores de variáveis e passar pelo código restante.  
  
> [!WARNING]  
>  Você pode depurar a tarefa Script quando executar o pacote no modo de 64 bits.  
  
> [!NOTE]  
>  Execute o pacote para depurar em sua tarefa Script. Se você executar apenas a tarefa individual, os pontos de interrupção no código da tarefa Script serão ignorados.  
  
> [!NOTE]  
>  Você não pode depurar uma tarefa Script quando executa-a como parte de um pacote filho que é executado a partir de uma tarefa Executar Pacote. Nessas circunstâncias, os pontos de interrupção definidos na tarefa Script no pacote filho são desconsiderados. Você pode depurar o pacote filho normalmente, executando-o separadamente.  
  
> [!NOTE]  
>  Quando você depura um pacote que contém várias tarefas Script, o depurador depura uma tarefa Script. O sistema poderá depurar outra tarefa Script se o depurador for concluído, como no caso de um contêiner Loop Foreach ou Loop For.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [problemas de instalação e configuração de VSTA para instalações de SSIS 2008 e R2](http://go.microsoft.com/fwlink/?LinkId=215661), em blogs.msdn.com.  
  
## <a name="see-also"></a>Consulte também  
 [Referenciando outros Assemblies em soluções de script](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)   
 [Configurando a tarefa de Script no Editor de tarefa de Script](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
  
  

