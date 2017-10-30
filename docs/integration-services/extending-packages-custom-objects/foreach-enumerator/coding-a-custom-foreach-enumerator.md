---
title: Codificando um enumerador Foreach personalizado | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom foreach enumerators [Integration Services], coding
ms.assetid: 279cf6de-d06f-40e7-b8ca-569310449f36
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 74e6e838c3dcfb18e52a8fbf460a5b71ee25399a
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="coding-a-custom-foreach-enumerator"></a>Codificando um enumerador Foreach personalizado
  Depois de criar uma classe que herda da classe base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> e aplicar o atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> a essa classe, você deve substituir a implementação das propriedades e dos métodos da classe base para fornecer sua funcionalidade personalizada.  
  
 Para obter um exemplo de funcionamento de um enumerador personalizado, consulte [desenvolvendo uma Interface de usuário para um enumerador de ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md).  
  
## <a name="initializing-the-enumerator"></a>Inicializando o enumerador  
 Você substitui o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.InitializeForEachEnumerator%2A> para referências aos gerenciadores de conexões definidos no pacote, e para referências de cache à interface de eventos que você pode usar para gerar erros, avisos e mensagens informativas.  
  
## <a name="validating-the-enumerator"></a>Validando o enumerador  
 Você substitui o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> para verificar se o enumerador está configurado corretamente. Se o método retornar **falha**, o enumerador e o pacote que contém o enumerador não serão executados. A implementação desse método é específica de cada enumerador, mas se o enumerador depender de objetos <xref:Microsoft.SqlServer.Dts.Runtime.Variable> ou <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>, adicione código para verificar se esses objetos existem nas coleções fornecidas para o método.  
  
 O exemplo de código a seguir demonstra uma implementação de <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> que verifica uma variável especificada em uma propriedade do enumerador.  
  
```csharp  
private string variableNameValue;  
  
public string VariableName  
{  
    get{ return this.variableNameValue; }  
    set{ this.variableNameValue = value; }  
}  
  
public override DTSExecResult Validate(Connections connections, VariableDispenser variableDispenser, IDTSInfoEvents infoEvents, IDTSLogging log)  
{  
    if (!variableDispenser.Contains(this.variableNameValue))  
    {  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + this.variableNameValue + " does not exist in the collection.", "", 0);  
            return DTSExecResult.Failure;  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Private variableNameValue As String  
  
Public Property VariableName() As String  
    Get   
         Return Me.variableNameValue  
    End Get  
    Set (ByVal Value As String)   
         Me.variableNameValue = value  
    End Set  
End Property  
  
Public Overrides Function Validate(ByVal connections As Connections, ByVal variableDispenser As VariableDispenser, ByVal infoEvents As IDTSInfoEvents, ByVal log As IDTSLogging) As DTSExecResult  
    If Not variableDispenser.Contains(Me.variableNameValue) Then  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + Me.variableNameValue + " does not exist in the collection.", "", 0)  
            Return DTSExecResult.Failure  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
## <a name="returning-the-collection"></a>Retornando a coleção  
 Durante execução, o contêiner <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> chama o método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> do enumerador personalizado. Nesse método, o enumerador cria, preenche e retorna sua coleção de itens. O <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> itera os itens na coleção e executa seu fluxo de controle para cada item da coleção.  
  
 O exemplo a seguir mostra uma implementação de <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> que retorna uma matriz de inteiros aleatórios.  
  
```csharp  
public override object GetEnumerator()  
{  
    ArrayList numbers = new ArrayList();  
  
    Random randomNumber = new Random(DateTime.Now);  
  
    for( int x=0; x < 100; x++ )  
        numbers.Add( randomNumber.Next());  
  
    return numbers;  
}  
```  
  
```vb  
Public Overrides Function GetEnumerator() As Object  
    Dim numbers As ArrayList =  New ArrayList()   
  
    Dim randomNumber As Random =  New Random(DateTime.Now)   
  
        Dim x As Integer  
        For  x = 0 To  100- 1  Step  x + 1  
        numbers.Add(randomNumber.Next())  
        Next  
  
    Return numbers  
End Function  
```  
 
## <a name="see-also"></a>Consulte também  
 [Criação de um enumerador de Foreach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [Desenvolvendo uma Interface de usuário para um enumerador ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  

