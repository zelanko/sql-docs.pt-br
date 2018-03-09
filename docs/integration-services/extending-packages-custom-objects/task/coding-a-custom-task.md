---
title: Codificando uma tarefa personalizada | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Validate method
- custom tasks [Integration Services], validating
- validation [Integration Services], design-time tasks
- SSIS custom tasks, validating
ms.assetid: dc224f4f-b339-4eb6-a008-1b4fe0ea4fd2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d23a210af0a19b81c583304984ae439e411037b5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="coding-a-custom-task"></a>Codificando uma tarefa personalizada
  Depois de criar uma classe que herda da classe base <xref:Microsoft.SqlServer.Dts.Runtime.Task> e aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> a essa classe, você deve substituir a implementação das propriedades e dos métodos da classe base para fornecer sua funcionalidade personalizada.  
  
## <a name="configuring-the-task"></a>Configurando a tarefa  
  
### <a name="validating-the-task"></a>Validando a tarefa  
 Ao projetar um pacote do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], você pode usar a validação para verificar as definições de cada tarefa, de forma a detectar definições incorretas ou inadequadas tão logo sejam definidas, em vez de encontrar todos os erros somente em tempo de execução. O propósito da validação é determinar se a tarefa contém configurações ou conexões inválidas que a impedirão de ser executada com sucesso. Isso garante que o pacote contenha tarefas com boa chance de serem executadas na primeira execução.  
  
 Você pode implementar a validação usando o método **Validate** em código personalizado. O mecanismo de tempo de execução valida uma tarefa chamando o método **Validate** na tarefa. É responsabilidade do desenvolvedor da tarefa definir os critérios que lhe proporcionem uma validação bem sucedida ou malsucedida da tarefa, e notificar o mecanismo de tempo de execução do resultado dessa avaliação.   
  
#### <a name="task-abstract-base-class"></a>Classe base abstrata da tarefa  
 A classe base abstrata <xref:Microsoft.SqlServer.Dts.Runtime.Task> fornece o método **Validate** que cada tarefa substitui para definir seus critérios de validação. O [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer chama automaticamente o método **Validate** várias vezes durante o projeto do pacote e fornece indicações visuais ao usuário quando ocorrem avisos ou erros para ajudar a identificar problemas com a configuração da tarefa. As tarefas fornecem resultados de validação retornando um valor da enumeração <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> e gerando eventos de aviso e erro. Esses eventos contêm informações que são exibidas ao usuário no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer.  
  
 Seguem alguns exemplos de validação:  
  
-   Um gerenciador de conexões valida o nome do arquivo específico.  
  
-   Um gerenciador de conexões valida que o tipo de entrada é o tipo esperado, como um arquivo XML.  
  
-   Uma tarefa que aguarda a entrada de banco de dados verifica se não pode receber dados de uma conexão que não seja de banco de dados.  
  
-   Uma tarefa garante que nenhuma de suas propriedades contradiga outras propriedades definidas na mesma tarefa.  
  
-   Uma tarefa garante que todos os recursos necessários usados pela tarefa em tempo de execução estejam disponíveis.  
  
 Desempenho é algo a ser considerado ao determinar o que é validado e o que não é. Por exemplo, a entrada para uma tarefa pode ser uma conexão em uma rede que tem baixa largura de banda ou alto tráfego. A validação poderá levar vários segundos para ser processada se você decidir validar se o recurso está disponível. Outra validação pode causar uma viagem de ida e volta para um servidor que está em demanda alta e a rotina de validação pode ficar lenta. Embora existam muitas propriedades e configurações que podem ser validadas, nem tudo deve ser validado.  
  
-   O código no método **Validate** também é chamado pelo <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> antes de a tarefa ser executada e o <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> cancela a execução se a validação falha.  
  
#### <a name="user-interface-considerations-during-validation"></a>Considerações da interface do usuário durante a validação  
 O <xref:Microsoft.SqlServer.Dts.Runtime.Task> inclui uma interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> como um parâmetro para o método **Validate**. A interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> contém os métodos que são chamados pela tarefa para gerar eventos para o mecanismo de tempo de execução. Os métodos <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> são chamados quando uma condição de aviso ou erro ocorre durante a validação. Ambos os métodos de aviso requerem os mesmos parâmetros, que incluem um código de erro, um componente de origem, descrição, arquivo de Ajuda e informações de contexto da Ajuda. O [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer usa essas informações para exibir indicações visuais na superfície de design. As indicações visuais fornecidas pelo designer incluem um ícone de exclamação que aparece próximo à tarefa na superfície do designer. Essa indicação visual sinaliza ao usuário que a tarefa requer configuração adicional antes de continuar a execução.  
  
 O ícone de exclamação também exibe uma dica de ferramenta que contém uma mensagem de erro. A mensagem de erro é fornecida pela tarefa no parâmetro de descrição do evento. Mensagens de erro também são exibidas no painel **Lista de Tarefas** do [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], fornecendo ao usuário um local central para exibir todos os erros de validação.  
  
#### <a name="validation-example"></a>Exemplo de validação  
 O exemplo de código seguinte mostra uma tarefa com uma propriedade **UserName**. Essa propriedade foi especificada conforme solicitado para a validação ter sucesso. Se a propriedade não for definida, a tarefa postará um erro e retornará <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Failure> da enumeração <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>. O método **Validate** é quebrado em um bloco de prova/captura e abandona a validação se ocorre uma exceção.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class SampleTask : Task  
{  
  private string userName = "";  
  
  public override DTSExecResult Validate(Connections connections,  
     VariableDispenser variableDispenser, IDTSComponentEvents events,  
     IDTSLogging log)  
  {  
    try  
    {  
      if (this.userName == "")  
      {  
        //   Raise an OnError event.  
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0);  
        //   Fail validation.  
        return DTSExecResult.Failure;  
      }  
      //   Return success.  
      return DTSExecResult.Success;  
    }  
    catch (System.Exception exception)  
    {  
      //   Capture exceptions, post an error, and fail validation.  
      events.FireError(0, "Sampletask", exception.Message, "", 0);  
      return DTSExecResult.Failure;  
    }  
  }  
  public string UserName  
  {  
    get  
    {  
      return this.userName;  
    }  
    set  
    {  
      this.userName = value;  
    }  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Public Class SampleTask  
  Inherits Task  
  
  Private _userName As String = ""  
  
  Public Overrides Function Validate(ByVal connections As Connections, _  
     ByVal variableDispenser As VariableDispenser, _  
     ByVal events As IDTSComponentEvents, _  
     ByVal log As IDTSLogging) As DTSExecResult  
  
    Try  
      If Me._userName = "" Then  
        '   Raise an OnError event.  
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0)  
        '   Fail validation.  
        Return DTSExecResult.Failure  
      End If  
      '   Return success.  
      Return DTSExecResult.Success  
    Catch exception As System.Exception  
      '   Capture exceptions, post an error, and fail validation.  
      events.FireError(0, "Sampletask", exception.Message, "", 0)  
      Return DTSExecResult.Failure  
    End Try  
  
  End Function  
  
  Public Property UserName() As String  
    Get  
      Return Me._userName  
    End Get  
    Set(ByVal Value As String)  
      Me._userName = Value  
    End Set  
  End Property  
  
End Class  
```  
  
### <a name="persisting-the-task"></a>Persistindo a tarefa  
 Normalmente, não é preciso implementar uma persistência personalizada para uma tarefa. A persistência personalizada é necessária somente quando as propriedades de um objeto usam tipos de dados complexos. Para obter mais informações, consulte [Desenvolvendo objetos personalizados para o Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md).  
  
## <a name="executing-the-task"></a>Executando a tarefa  
 Esta seção descreve como usar o método **Execute**, que é herdado e substituído por tarefas. Esta seção também explica vários modos de fornecer informações sobre os resultados da execução de uma tarefa.  
  
### <a name="execute-method"></a>Método Execute  
 As tarefas contidas em um pacote são executadas quando o tempo de execução do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] chama seu método **Execute**. As tarefas implementam sua principal lógica de negócios e sua funcionalidade nesse método e fornecem os resultados da execução postando mensagens, retornando um valor da enumeração <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> e substituindo a propriedade **get** da propriedade **ExecutionValue**.  
  
 A classe base <xref:Microsoft.SqlServer.Dts.Runtime.Task> fornece uma implementação padrão do método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>. As tarefas personalizadas anulam esse método para definir sua funcionalidade de tempo de execução. O objeto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> quebra a tarefa, isolando-a do mecanismo de tempo de execução e dos outros objetos no pacote. Por causa desse isolamento, a tarefa não reconhece sua localização no pacote quanto à ordem de execução e é executada somente quando chamada pelo tempo de execução. Essa arquitetura evita os problemas que podem ocorrer quando as tarefas modificam o pacote durante a execução. A tarefa recebe acesso aos outros objetos do pacote somente por meio dos objetos fornecidos a ela como parâmetros no método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>. Esses parâmetros permitem que as tarefas gerem eventos, gravem entradas no log de eventos, acessem a coleção de variáveis e inscrevam conexões em fontes de dados nas transações, ao mesmo tempo mantendo o isolamento necessário para garantir a estabilidade e a confiabilidade do pacote.  
  
 A tabela seguinte lista os parâmetros fornecidos à tarefa no método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Connections>|Contém uma coleção de objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> disponíveis para a tarefa.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.VariableDispenser>|Contém as variáveis disponíveis para a tarefa. As tarefas usam variáveis pelo VariableDispenser; as tarefas não usam variáveis diretamente. O VariableDispenser bloqueia e desbloqueia as variáveis e impede deadlocks ou substituições.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents>|Contém os métodos chamados pela tarefa para gerar eventos ao mecanismo de tempo de execução.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSLogging>|Contém métodos e propriedades usados pela tarefa para gravar entradas no log de eventos.|  
|Object|Contém o objeto de transação do qual o contêiner faz parte, se houver. Esse valor é passado como um parâmetro ao método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> de um objeto <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.|  
  
### <a name="providing-execution-feedback"></a>Fornecendo comentários de execução  
 As tarefas encapsulam seu código em blocos **try/catch** para evitar que sejam geradas exceções para o mecanismo de tempo de execução. Isso assegura que o pacote conclua a execução e não pare inesperadamente. Porém, o mecanismo de tempo de execução fornece outros mecanismos para tratar condições de erro que podem ocorrer durante a execução de uma tarefa. Eles incluem postar mensagens de erro e de aviso, retornar um valor da estrutura do <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>, postar mensagens, retornar o valor <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> e divulgar informações sobre os resultados da execução da tarefa através da propriedade <xref:Microsoft.SqlServer.Dts.Runtime.Task.ExecutionValue%2A>.  
  
 A interface do <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> contém os métodos <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A>, que podem ser chamados pela tarefa para postar mensagens de erro e de aviso para o mecanismo de tempo de execução. Ambos os métodos requerem parâmetros como código de erro, componente de origem, descrição, arquivo de Ajuda e informações de contexto de ajuda. Dependendo da configuração da tarefa, o tempo de execução responde a essas mensagens gerando eventos e pontos de interrupção, ou gravando informações no log de eventos.  
  
 O <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> também fornece a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> que pode ser usada para fornecer informações adicionais sobre os resultados da execução. Por exemplo, se uma tarefa exclui linhas de uma tabela como parte do seu método **Execute**, ela pode retornar o número de linhas excluídas como o valor da propriedade <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A>. Além disso, o <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> fornece a propriedade <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecValueVariable%2A>. Essa propriedade permite que o usuário mapeie o <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> retornado da tarefa para qualquer variável visível à tarefa. A variável especificada pode ser usada para estabelecer restrições de precedência entre as tarefas.  
  
### <a name="execution-example"></a>Exemplo de execução  
 O exemplo de código seguinte demonstra uma implementação do método **Execute** e mostra uma propriedade **ExecutionValue** substituída. A tarefa exclui o arquivo que é especificado pela propriedade **fileName** da tarefa. A tarefa posta um aviso se o arquivo não existir ou se a propriedade **fileName** for uma cadeia de caracteres vazia. A tarefa retorna um valor **booliano** na propriedade <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> para indicar se o arquivo foi excluído.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class SampleTask : Task  
{  
  private string fileName = "";  
  private bool fileDeleted = false;  
  
  public override DTSExecResult Execute(Connections cons,  
     VariableDispenser vars, IDTSComponentEvents events,  
     IDTSLogging log, Object txn)  
  {  
    try  
    {  
      if (this.fileName == "")  
      {  
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0);  
        this.fileDeleted = false;  
      }  
      else  
      {  
        if (System.IO.File.Exists(this.fileName))  
        {  
          System.IO.File.Delete(this.fileName);  
          this.fileDeleted = true;  
        }  
        else  
          this.fileDeleted = false;  
      }  
      return DTSExecResult.Success;  
    }  
    catch (System.Exception exception)  
    {  
      //   Capture the exception and post an error.  
      events.FireError(0, "Sampletask", exception.Message, "", 0);  
      return DTSExecResult.Failure;  
    }  
  }  
  public string FileName  
  {  
    get { return this.fileName; }  
    set { this.fileName = value; }  
  }  
  public override object ExecutionValue  
  {  
    get { return this.fileDeleted; }  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Public Class SampleTask  
  Inherits Task  
  
  Private _fileName As String = ""  
  Private _fileDeleted As Boolean = False  
  
  Public Overrides Function Execute(ByVal cons As Connections, _  
     ByVal vars As VariableDispenser, ByVal events As IDTSComponentEvents, _  
     ByVal log As IDTSLogging, ByVal txn As Object) As DTSExecResult  
  
    Try  
      If Me._fileName = "" Then  
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0)  
        Me._fileDeleted = False  
      Else  
        If System.IO.File.Exists(Me._fileName) Then  
          System.IO.File.Delete(Me._fileName)  
          Me._fileDeleted = True  
        Else  
          Me._fileDeleted = False  
        End If  
      End If  
      Return DTSExecResult.Success  
    Catch exception As System.Exception  
      '   Capture the exception and post an error.  
      events.FireError(0, "Sampletask", exception.Message, "", 0)  
      Return DTSExecResult.Failure  
    End Try  
  
  End Function  
  
  Public Property FileName() As String  
    Get  
      Return Me._fileName  
    End Get  
    Set(ByVal Value As String)  
      Me._fileName = Value  
    End Set  
  End Property  
  
  Public Overrides ReadOnly Property ExecutionValue() As Object  
    Get  
      Return Me._fileDeleted  
    End Get  
  End Property  
  
End Class  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Criar uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)   
 [Codificar uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)   
 [Desenvolver uma interface do usuário para uma tarefa personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
  
  
