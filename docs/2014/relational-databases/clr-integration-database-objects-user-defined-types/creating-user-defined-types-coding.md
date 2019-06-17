---
title: Codificando tipos definidos pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1df89052e33f75921a45f124739e2a375dc2d2ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919942"
---
# <a name="coding-user-defined-types"></a>codificando tipos definidos pelo usuário
  Ao codificar a definição UDT (tipo definido pelo usuário), você deve implementar vários recursos, dependendo da implementação da UDT como classe ou estrutura, bem como das opções de formato e de serialização escolhidas.  
  
 O exemplo nesta seção ilustra a implementação de uma `Point` UDT como `struct` (ou `Structure` no Visual Basic). A UDT `Point` consiste em coordenadas X e Y implementadas como procedimentos de propriedade.  
  
 Os seguintes namespaces são obrigatórios na definição de uma UDT:  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 O namespace `Microsoft.SqlServer.Server` contém os objetos necessários a vários atributos da UDT, e o namespace `System.Data.SqlTypes` contém as classes que representam os tipos de dados nativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponíveis para o assembly. É claro que talvez haja namespaces adicionais necessários ao funcionamento correto do assembly. A UDT `Point` também usa o namespace `System.Text` para trabalhar com cadeias de caracteres.  
  
> [!NOTE]  
>  Não há suporte para objetos de banco de dados do Visual C++, como UDTs. compilados com `/clr:pure` para execução.  
  
## <a name="specifying-attributes"></a>Especificando atributos  
 Os atributos determinam como a serialização é usada para construir a representação de armazenamento de UDTs e transmiti-los por valor para o cliente.  
  
 A `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` é obrigatória. O atributo `Serializable` é opcional. Também é possível especificar `Microsoft.SqlServer.Server.SqlFacetAttribute` para fornecer informações sobre o tipo de retorno de uma UDT. Para obter mais informações, confira [Atributos personalizados para rotinas do CLR (Common Language Runtime)](../clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
### <a name="point-udt-attributes"></a>Atributos da UDT Point  
 O `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` define o formato de armazenamento para o `Point` UDT como `Native`. `IsByteOrdered` é definido como `true`, o que garante que os resultados das comparações sejam os mesmos no SQL Server se a mesma comparação foi feita no código gerenciado. A UDT implementa a interface `System.Data.SqlTypes.INullable` para que a UDT reconheça nulos.  
  
 O seguinte fragmento de código mostra os atributos da UDT `Point`.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>Implementando a nulidade  
 Além de especificar corretamente os atributos dos assemblies, a UDT também precisa oferecer suporte à nulidade. As UDTs carregadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhecem nulos, mas para que reconheça um valor nulo, a UDT deve implementar a interface `System.Data.SqlTypes.INullable`.  
  
 Você deve criar uma propriedade chamada `IsNull`, necessária para determinar se um valor é nulo dentro do código CLR. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontra uma instância nula de uma UDT, esta é mantida, usando métodos manipulação de nulos normais. O servidor não perde tempo serializando ou desserializando a UDT caso não precise, e ele não perde espaço armazenando uma UDT nula. Essa verificação de nulos é realizada sempre que uma UDT passa pelo CLR, o que significa que usar a construção [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL para verificar se há UDTs nulas deve funcionar sempre. A propriedade `IsNull` também é usada pelo servidor para testar se uma instância é nula. Quando determina que a UDT é nula, o servidor pode usar a manipulação de nulos nativa.  
  
 O método `get()` de `IsNull` não tem diferenciação de maiúsculas ou minúsculas definitivamente. Se uma variável `Point` de `@p` for `Null`, `@p.IsNull` será, por padrão, avaliada como "NULL", e não como "1". Isso porque o atributo `SqlMethod(OnNullCall)` do método `IsNull get()` usa falso como padrão. Como o objeto é `Null`, quando a propriedade é solicitada, o objeto não é desserializado, o método não é chamado e um valor padrão "NULL" é retornado.  
  
### <a name="example"></a>Exemplo  
 No seguinte exemplo, a variável `is_Null` é privada e mantém o estado de nulidade para a instância da UDT. O código deve manter um valor apropriado para `is_Null`. A UDT também deve ter uma propriedade estática chamada `Null` que retorne uma instância de valor nulo da UDT. Isso permite que a UDT retorne um valor nulo caso a instância seja realmente nula no banco de dados.  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>IS NULL vs. IsNull  
 Considere uma tabela que contém o esquema Points(id int, location Point), em que `Point` é uma UDT CLR, além das seguintes consultas:  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 Ambas as consultas retornam as IDs de pontos com locais não `Null`. Na Consulta 1, é usada a manipulação de nulos normal, não havendo nenhuma desserialização das UDTs obrigatória. Já a Consulta 2 precisa desserializar todos os objetos não `Null` e chamar o CLR para obter o valor da propriedade `IsNull`. Claramente, usar `IS NULL` apresentará um desempenho melhor, não devendo haver nenhum motivo para ler a propriedade `IsNull` de uma UDT no código [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Então, para que serve a propriedade `IsNull`? Primeiro, ela é necessária para determinar se um valor é `Null` dentro do código CLR. Segundo, como o servidor precisa de uma forma para testar se uma instância é `Null`, essa propriedade é usada por ele. Depois de determinar ser `Null`, ele poderá usar a manipulação de nulos nativa para tratá-la.  
  
## <a name="implementing-the-parse-method"></a>Implementando o método Parse  
 Os métodos `Parse` e `ToString` permitem conversões de e para representações da cadeia de caracteres da UDT. O método `Parse` permite converter uma cadeia de caracteres em uma UDT. Ele precisa ser declarado como `static` (ou `Shared` no Visual Basic) e usar um parâmetro do tipo `System.Data.SqlTypes.SqlString`.  
  
 O seguinte código implementa o método `Parse` para a UDT `Point`, que separa as coordenadas X e Y. O método `Parse` tem um único argumento do tipo `System.Data.SqlTypes.SqlString` e supõe que os valores X e Y sejam fornecidos como uma cadeia de caracteres delimitados por vírgulas. Definir o atributo `Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall` como `false` impede o método `Parse` de ser chamado em uma instância nula de Point.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>Implementando o método ToString  
 O método `ToString` converte a UDT `Point` em um valor de cadeia de caracteres. Nesse caso, a cadeia de caracteres "NULL" é retornada para uma instância Null do tipo `Point`. O método `ToString` inverte o método `Parse` usando um `System.Text.StringBuilder` para retornar um `System.String` delimitado por vírgulas que consiste nos valores de coordenadas X e Y. Porque **InvokeIfReceiverIsNull** padrão é false, a verificação de uma instância nula de `Point` é desnecessária.  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>Expondo propriedades da UDT  
 A UDT `Point` expõe coordenadas X e Y que são implementadas como propriedades públicas de leitura/gravação do tipo `System.Int32`.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>Validando valores de UDT  
 Ao trabalhar com dados de UDT, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] converte automaticamente valores binários em valores de UDT. Esse processo de conversão envolve verificar se os valores são apropriados ao formato de serialização do tipo e garantir que o valor possa ser desserializado corretamente. Isso garante que o valor pode ser convertido de volta para o formato binário. No caso das UDTs ordenadas por byte, isso também garante que o valor binário resultante corresponda ao valor binário original. Isso impede a manutenção de valores inválidos no banco de dados. Em alguns casos, esse nível de verificação pode ser inadequado. Talvez seja obrigatória uma validação adicional quando os valores de UDT devem estar em um domínio ou intervalo esperado. Por exemplo, uma UDT que implementa uma data pode exigir que o valor de dia seja um número positivo e que esteja em um determinado intervalo de valores válidos.  
  
 A propriedade `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName` de `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` permite fornecer o nome de um método de avaliação executado pelo servidor quando os dados são atribuídos a uma UDT ou convertidos em uma. `ValidationMethodName` também é chamado durante a execução do utilitário bcp, BULK INSERT, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, consulta distribuída e operações RPC (chamada de procedimento remoto) do protocolo TDS. O valor padrão de `ValidationMethodName` é null, o que indica não haver nenhum método de validação.  
  
### <a name="example"></a>Exemplo  
 O seguinte fragmento de código mostra a declaração da classe `Point`, que especifica um `ValidationMethodName` de `ValidatePoint`.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 Caso seja especificado, um método de validação deve ter uma assinatura semelhante ao seguinte fragmento de código.  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 O método de validação pode ter qualquer escopo e deve retornar `true` caso o valor seja válido, e `false` caso contrário. Caso o método retorne `false` ou lance uma exceção, o valor é tratado como não válido, e ocorre um erro.  
  
 No exemplo abaixo, o código só permite valores iguais a zero ou maiores que as coordenadas X e Y.  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>Limitações do método de validação  
 O servidor chama o método de validação ao realizar conversões, e não quando os dados são inseridos definindo propriedades individuais, ou quando eles são inseridos usando uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT.  
  
 Você deve chamar explicitamente o método de validação nos setters de propriedade e o `Parse` método se desejar que o método de validação para ser executado em todas as situações. Não se trata de um requisito e, em alguns casos, talvez não seja sequer desejável.  
  
### <a name="parse-validation-example"></a>Exemplo de validação de Parse  
 Para garantir que o `ValidatePoint` método é invocado na `Point` classe, você deve chamá-lo no `Parse` método e coordenam a valores da propriedade procedimentos que defina X e Y. O fragmento de código a seguir mostra como chamar o `ValidatePoint` método de validação do `Parse` função.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>Exemplo de validação da propriedade  
 O fragmento de código a seguir mostra como chamar o `ValidatePoint` método de validação dos procedimentos de propriedade que definir as coordenadas X e Y.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>Codificando métodos de UDT  
 Durante a codificação dos métodos de UDT, considere se o algoritmo usado pode ser alterado com o passar do tempo. Em caso positivo, você talvez queira considerar a criação de uma classe separada para os métodos usados pela UDT. Caso o algoritmo seja alterado, é possível recompilar a classe com o novo código e carregar o assembly em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem afetar a UDT. Em muitos casos, as UDTs podem ser recarregadas usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY, mas isso pode causar problemas nos dados existentes. Por exemplo, o `Currency` UDT incluído com o **AdventureWorks** usos do banco de dados de exemplo uma **ConvertCurrency** de função para converter valores de moeda, que é implementado em uma classe separada. É possível que algoritmos de conversão sejam alterados de maneiras imprevisíveis no futuro, ou que uma nova funcionalidade seja obrigatória. Separando o **ConvertCurrency** função do `Currency` implementação de UDT fornece maior flexibilidade ao planejar alterações futuras.  
  
### <a name="example"></a>Exemplo  
 O `Point` classe contém três métodos simples para calcular a distância: **Distância**, **DistanceFrom** e **DistanceFromXY**. Cada um retorna `double` que calcula a distância entre `Point` e zero, a distância entre um ponto especificado e `Point`, além da distância entre as coordenadas X e Y e `Point`. **Distância** e **DistanceFrom** cada chamada **DistanceFromXY**e demonstram como usar argumentos diferentes para cada método.  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>Usando atributos SqlMethod  
 A classe `Microsoft.SqlServer.Server.SqlMethodAttribute` fornece atributos personalizados que podem ser usados para marcar definições de método a fim de especificar determinismo, comportamento em chamada nula e determinar se um método é um modificador. Os valores padrão dessas propriedades são pressupostos, e o atributo personalizado só é usado quando um valor não padrão é necessário.  
  
> [!NOTE]  
>  A classe `SqlMethodAttribute` é herdada da classe `SqlFunctionAttribute`, assim `SqlMethodAttribute` herda os campos `FillRowMethodName` e `TableDefinition` de `SqlFunctionAttribute`. Isso indica que é possível escrever um método com valor de tabela, o que não é o caso. O método compila e o assembly implanta, mas um erro sobre o `IEnumerable` retornar o tipo é gerado em tempo de execução com a seguinte mensagem: "Método, propriedade ou campo '\<nome >' em classe\<classe >' no assembly '\<assembly >' tem o tipo de retorno inválido."  
  
 A seguinte tabela descreve algumas das propriedades `Microsoft.SqlServer.Server.SqlMethodAttribute` relevantes que podem ser usadas em métodos de UDT, além de listar os valores padrão.  
  
 DataAccess  
 Indica se a função envolve o acesso a dados de usuário armazenados na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O padrão é `DataAccessKind``None`.  
  
 IsDeterministic  
 Indica se a função produz os mesmos valores de saída, dados os mesmos valores de entrada e o mesmo estado de banco de dados. O padrão é `false`.  
  
 IsMutator  
 Indica se o método causa uma alteração de estado na instância da UDT. O padrão é `false`.  
  
 IsPrecise  
 Indica se a função envolve computações imprecisas como, por exemplo, operações de ponto flutuante. O padrão é `false`.  
  
 OnNullCall  
 Indica se o método é chamado quando são especificados argumentos de entrada de referência nulos. O padrão é `true`.  
  
### <a name="example"></a>Exemplo  
 A propriedade `Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator` possibilita marcar um método que permite uma alteração no estado de uma instância de uma UDT A [!INCLUDE[tsql](../../includes/tsql-md.md)] não permite definir duas propriedades de UDT na cláusula SET de uma instrução UPDATE. No entanto, é possível ter um método marcado como um modificador que altera os dois membros.  
  
> [!NOTE]  
>  Os métodos Mutator não são permitidos em consultas. Eles só podem ser chamados em instruções de atribuição ou de modificação de dados. Caso um método marcado como modificador não retorne `void` (ou não é um `Sub` no Visual Basic), CREATE TYPE falha com um erro.  
  
 A seguinte instrução supõe a existência de uma UDT `Triangles` com um método `Rotate`. A seguinte instrução de atualização [!INCLUDE[tsql](../../includes/tsql-md.md)] invoca o método `Rotate`:  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 O método `Rotate` é decorado com a configuração de atributo `SqlMethod``IsMutator` como `true` para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa marcar o método como modificador. O código também define `OnNullCall` como `false`, o que indica para o servidor que o método retorna uma referência nula (`Nothing` no Visual Basic), caso alguma dos parâmetros de entrada sejam referências nulas.  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>Implementando uma UDT com um formato definido pelo usuário  
 Ao implementar uma UDT com um formato definido pelo usuário, você deve implementar os métodos `Read` e `Write` que implementam a interface Microsoft.SqlServer.Server.IBinarySerialize para tratar dados de UDT de serialização e de desserialização. Também é possível especificar a propriedade `MaxByteSize` de `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute`.  
  
### <a name="the-currency-udt"></a>A UDT Currency  
 A UDT `Currency` está incluída n as amostras do CLR que podem ser instaladas com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 A UDT `Currency` oferece suporte à manipulação de valores em dinheiro no sistema financeiro de uma determinada cultura. Você deve definir dois campos: `string` para `CultureInfo`, que especifica quem emitiu a moeda (pt-br, por exemplo) e `decimal` para `CurrencyValue`, o volume de dinheiro.  
  
 Embora não seja usada pelo servidor para realizar comparações, a UDT `Currency` implementa a interface `System.IComparable`, que expõe um único método, `System.IComparable.CompareTo`. Isso é usado do lado de cliente, em situações nas quais é desejável comparar com precisão ou ordenar valores de moeda dentro de culturas.  
  
 O código em execução no CLR compara a cultura separadamente do valor de moeda. Para o código [!INCLUDE[tsql](../../includes/tsql-md.md)], as seguintes ações determinam a comparação:  
  
1.  Defina o atributo `IsByteOrdered` como true, que informa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar a representação binária mantida em disco para comparações.  
  
2.  Use o método `Write` da UDT `Currency` para determinar como a UDT é mantida em disco e, assim, a forma como os valores da UDT são comparados e ordenados para as operações [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
3.  Salve a UDT `Currency` que usa o seguinte formato binário:  
  
    1.  Salve a cultura como uma cadeia de caracteres codificada UTF-16 para bytes de 0 a 19 com preenchimento à direita com caracteres nulos.  
  
    2.  Use bytes 20 e acima para conter o valor decimal da moeda.  
  
 O propósito do preenchimento é assegurar que a cultura seja totalmente separada do valor de moeda, para que quando uma UDT seja comparada com outra no código [!INCLUDE[tsql](../../includes/tsql-md.md)], os bytes de cultura sejam comparados com os bytes de cultura e os valores de byte da moeda, com os valores de byte da moeda.  
  
 Para o código completo a listagem para o `Currency` UDT, siga as orientações para instalar o CLR amostras em [exemplos do mecanismo de banco de dados do SQL Server](http://msftengprodsamples.codeplex.com/).  
  
### <a name="currency-attributes"></a>Atributos Currency  
 A UDT `Currency` é definida com os atributos a seguir.  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>Criando métodos Read e Write com IBinarySerialize  
 Ao escolher o formato de serialização `UserDefined`, você também deve implementar a interface `IBinarySerialize` e criar seus próprios métodos `Read` e `Write`. Os seguintes procedimentos na UDT `Currency` usam `System.IO.BinaryReader` e `System.IO.BinaryWriter` para ler e gravar na UDT.  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 Para o código completo a listagem para o `Currency` UDT, consulte [exemplos do mecanismo de banco de dados do SQL Server](http://msftengprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Consulte também  
 [Criando um tipo definido pelo usuário](creating-user-defined-types.md)  
  
  
