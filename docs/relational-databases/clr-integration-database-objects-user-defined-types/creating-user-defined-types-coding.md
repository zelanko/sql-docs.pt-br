---
title: Codificando tipos definidos pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b3a698c63fa5fc7e5a0802716b3112df31cf241f
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35697897"
---
# <a name="creating-user-defined-types---coding"></a>Criando tipos definidos pelo usuário - codificação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Ao codificar a definição UDT (tipo definido pelo usuário), você deve implementar vários recursos, dependendo da implementação da UDT como classe ou estrutura, bem como das opções de formato e de serialização escolhidas.  
  
 O exemplo nesta seção ilustra a implementação de um **ponto** UDT como uma **struct** (ou **estrutura** no Visual Basic). O **ponto** UDT consiste em X e Y coordenadas implementadas como procedimentos de propriedade.  
  
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
  
 O **SQLServer** namespace contém os objetos necessários para vários atributos da UDT e o **SqlTypes** namespace contém as classes que representam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]disponíveis para o assembly de tipos de dados nativos. É claro que talvez haja namespaces adicionais necessários ao funcionamento correto do assembly. O **ponto** UDT também usa o **Text** namespace para trabalhar com cadeias de caracteres.  
  
> [!NOTE]  
>  Objetos de banco de dados de Visual C++, como UDTs, compiladas com **/clr: pure** não têm suporte para execução.  
  
## <a name="specifying-attributes"></a>Especificando atributos  
 Os atributos determinam como a serialização é usada para construir a representação de armazenamento de UDTs e transmiti-los por valor para o cliente.  
  
 O **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** é necessário. O **Serializable** atributo é opcional. Você também pode especificar o **Microsoft.SqlServer.Server.SqlFacetAttribute** para fornecer informações sobre o tipo de retorno de um UDT. Para obter mais informações, confira [Atributos personalizados para rotinas do CLR (Common Language Runtime)](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
### <a name="point-udt-attributes"></a>Atributos da UDT Point  
 O **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** define o formato de armazenamento para o **ponto** UDT **nativo**. **IsByteOrdered** é definido como **true**, que garante que os resultados das comparações sejam os mesmos no SQL Server, como se a mesma comparação foi feita no código gerenciado. A UDT implementa o **System.Data.SqlTypes.INullable** interface para informar o nulo UDT.  
  
 O fragmento de código a seguir mostra os atributos para o **ponto** UDT.  
  
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
 Além de especificar corretamente os atributos dos assemblies, a UDT também precisa oferecer suporte à nulidade. Os UDTs carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reconhecem nulos, mas na ordem para o UDT reconheça um valor nulo, o UDT precisa implementar o **System.Data.SqlTypes.INullable** interface.  
  
 Você deve criar uma propriedade chamada **IsNull**, que é necessário para determinar se um valor é nulo dentro do código CLR. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontra uma instância nula de uma UDT, esta é mantida, usando métodos manipulação de nulos normais. O servidor não perde tempo serializando ou desserializando a UDT caso não precise, e ele não perde espaço armazenando uma UDT nula. Essa verificação de nulos é realizada sempre que uma UDT passa pelo CLR, o que significa que usar a construção [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL para verificar se há UDTs nulas deve funcionar sempre. O **IsNull** propriedade também é usada pelo servidor para testar se uma instância é nula. Quando determina que a UDT é nula, o servidor pode usar a manipulação de nulos nativa.  
  
 O **Get ()** método **IsNull** não é especial de maiusculas e minúsculas de forma alguma. Se um **ponto** variável **@p** é **nulo**, em seguida, **@p.IsNull** será, por padrão, avaliada como "NULL", não "1". Isso ocorre porque o **SqlMethod(OnNullCall)** atributo o **IsNull Get ()** método padrão é false. Porque o objeto é **nulo**, quando a propriedade é solicitada, o objeto não é desserializado, o método não é chamado e um valor padrão de "NULL" será retornado.  
  
### <a name="example"></a>Exemplo  
 No seguinte exemplo, a variável `is_Null` é privada e mantém o estado de nulidade para a instância da UDT. O código deve manter um valor apropriado para `is_Null`. A UDT também deve ter uma propriedade estática chamada **nulo** que retorna uma instância de valor nulo da UDT. Isso permite que a UDT retorne um valor nulo caso a instância seja realmente nula no banco de dados.  
  
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
  
### <a name="is-null-vs-isnull"></a>IS NULL e IsNull  
 Considere uma tabela que contém o esquema Points (id int, ponto de local), onde **ponto** é um CLR UDT e as consultas a seguir:  
  
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
  
 Ambas as consultas retornam as IDs de pontos com não**nulo** locais. Na Consulta 1, é usada a manipulação de nulos normal, não havendo nenhuma desserialização das UDTs obrigatória. Consulta 2, por outro lado, precisa desserializar cada não -**nulo** de objeto e chamar o CLR para obter o valor da **IsNull** propriedade. Claramente, usar **IS NULL** exibirá o melhor desempenho e nunca deve ser um motivo para ler o **IsNull** propriedade de um UDT de [!INCLUDE[tsql](../../includes/tsql-md.md)] código.  
  
 Portanto, o que é o uso do **IsNull** propriedade? Primeiro, é necessário para determinar se um valor é **nulo** dentro do código CLR. Segundo, o servidor precisa de uma maneira de testar se uma instância é **nulo**, portanto, esta propriedade é usada pelo servidor. Depois de determinar ser é **nulo**, em seguida, ele pode usar a manipulação de nulos nativa para tratá-la.  
  
## <a name="implementing-the-parse-method"></a>Implementando o método Parse  
 O **analisar** e **ToString** métodos permitem conversões de e para representações de cadeia de caracteres do UDT. O **analisar** método permite que uma cadeia de caracteres a ser convertido em um UDT. Ele deve ser declarado como **estático** (ou **compartilhado** no Visual Basic) e usar um parâmetro de tipo **System.Data.SqlTypes.SqlString**.  
  
 O código a seguir implementa a **analisar** método para o **ponto** UDT, que separa as coordenadas X e Y. O **analisar** método tem um único argumento de tipo **System.Data.SqlTypes.SqlString**e pressupõe que os valores X e Y são fornecidos como uma cadeia de caracteres delimitada por vírgulas. Definindo o **Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall** atributo **false** impede o **analisar** método seja chamado a partir de uma instância nula de Ponto.  
  
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
 O **ToString** método converte o **ponto** UDT com um valor de cadeia de caracteres. Nesse caso, a cadeia de caracteres "NULL" é retornada para uma instância nula da **ponto** tipo. O **ToString** método inverte o **analisar** método usando um **StringBuilder** para retornar um delimitada por vírgulas **System. String**consiste em valores de coordenada X e Y. Porque **InvokeIfReceiverIsNull** padrão é false, a verificação de uma instância nula de **ponto** é desnecessária.  
  
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
 O **ponto** UDT expõe coordenadas X e Y que são implementadas como propriedades públicas de leitura / gravação do tipo **System. Int32**.  
  
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
 Ao trabalhar com dados de UDT, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] converte automaticamente valores binários em valores de UDT. Esse processo de conversão envolve verificar se os valores são apropriados ao formato de serialização do tipo e garantir que o valor possa ser desserializado corretamente. Isso garante que o valor pode ser convertido para formato binário. No caso das UDTs ordenadas por byte, isso também garante que o valor binário resultante corresponda ao valor binário original. Isso impede a manutenção de valores inválidos no banco de dados. Em alguns casos, esse nível de verificação pode ser inadequado. Talvez seja obrigatória uma validação adicional quando os valores de UDT devem estar em um domínio ou intervalo esperado. Por exemplo, uma UDT que implementa uma data pode exigir que o valor de dia seja um número positivo e que esteja em um determinado intervalo de valores válidos.  
  
 O **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName** propriedade o **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** permite que você forneça o nome de um método de validação que o servidor é executada quando dados são atribuídos a uma UDT ou convertidos em uma. **ValidationMethodName** também é chamado durante a execução do utilitário bcp, BULK INSERT, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, consulta distribuída e operações de RPC (chamada) de procedimento remoto de protocolo TDS de dados tabulares. O valor padrão para **ValidationMethodName** é null, indicando que não há nenhum método de validação.  
  
### <a name="example"></a>Exemplo  
 O fragmento de código a seguir mostra a declaração para o **ponto** classe, que especifica um **ValidationMethodName** de **ValidatePoint**.  
  
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
  
 O método de validação pode ter qualquer escopo e deve retornar **true** se o valor for válido, e **false** caso contrário. Se o método retornar **false** ou lançará uma exceção, o valor é tratado não é válido e um erro será gerado.  
  
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
  
 Você deve chamar explicitamente o método de validação nos setters de propriedade e o **analisar** método se você quiser que o método de validação para executar em todas as situações. Não se trata de um requisito e, em alguns casos, talvez não seja sequer desejável.  
  
### <a name="parse-validation-example"></a>Exemplo de validação de Parse  
 Para garantir que o **ValidatePoint** método é invocado no **ponto** classe, você deverá chamá-la do **analisar** método e os procedimentos de propriedade que defina X e Y valores de coordenada. O fragmento de código a seguir mostra como chamar o **ValidatePoint** método de validação do **analisar** função.  
  
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
 O fragmento de código a seguir mostra como chamar o **ValidatePoint** método de validação dos procedimentos de propriedade que defina as coordenadas X e Y.  
  
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
 Durante a codificação dos métodos de UDT, considere se o algoritmo usado pode ser alterado com o passar do tempo. Em caso positivo, você talvez queira considerar a criação de uma classe separada para os métodos usados pela UDT. Caso o algoritmo seja alterado, é possível recompilar a classe com o novo código e carregar o assembly em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem afetar a UDT. Em muitos casos, as UDTs podem ser recarregadas usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY, mas isso pode causar problemas nos dados existentes. Por exemplo, o **moeda** UDT incluído com o **AdventureWorks** usa do banco de dados de exemplo um **ConvertCurrency** função para converter valores de moeda, que é implementado em uma classe separada. É possível que algoritmos de conversão sejam alterados de maneiras imprevisíveis no futuro, ou que uma nova funcionalidade seja obrigatória. Separando o **ConvertCurrency** de função do **moeda** implementação de UDT fornece maior flexibilidade durante o planejamento de alterações futuras.  
  
### <a name="example"></a>Exemplo  
 O **ponto** classe contém três métodos simples para calcular a distância: **distância**, **DistanceFrom** e **DistanceFromXY**. Cada um retorna um **duplo** calcula a distância entre **ponto** a zero, a distância de um ponto especificado para **ponto**, e a distância do especificado coordenadas X e Y para **ponto**. **Distância** e **DistanceFrom** cada chamada **DistanceFromXY**e demonstram como usar argumentos diferentes para cada método.  
  
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
 O **Microsoft.SqlServer.Server.SqlMethodAttribute** classe fornece atributos personalizados que podem ser usados para marcar definições de método, a fim de especificar determinismo, comportamento em chamada nula e para especificar se um método é um modificador. Os valores padrão dessas propriedades são pressupostos, e o atributo personalizado só é usado quando um valor não padrão é necessário.  
  
> [!NOTE]  
>  O **SqlMethodAttribute** classe herda o **SqlFunctionAttribute** classe isso **SqlMethodAttribute** herda o **FillRowMethodName** e **TableDefinition** os campos do **SqlFunctionAttribute**. Isso indica que é possível escrever um método com valor de tabela, o que não é o caso. O método compila e o assembly implanta, mas um erro sobre a **IEnumerable** retornar o tipo é gerado em tempo de execução com a seguinte mensagem: "método, propriedade ou campo '\<nome >' na classe\<classe >' no assembly '\<assembly >' tem o tipo de retorno inválido. "  
  
 A tabela a seguir descreve algumas das relevante **Microsoft.SqlServer.Server.SqlMethodAttribute** propriedades que podem ser usadas em métodos de UDT e lista seus valores padrão.  
  
 DataAccess  
 Indica se a função envolve o acesso a dados de usuário armazenados na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O padrão é **DataAccessKind**. **Nenhum**.  
  
 IsDeterministic  
 Indica se a função produz os mesmos valores de saída, dados os mesmos valores de entrada e o mesmo estado de banco de dados. O padrão é **false**.  
  
 IsMutator  
 Indica se o método causa uma alteração de estado na instância da UDT. O padrão é **false**.  
  
 IsPrecise  
 Indica se a função envolve computações imprecisas como, por exemplo, operações de ponto flutuante. O padrão é **false**.  
  
 OnNullCall  
 Indica se o método é chamado quando são especificados argumentos de entrada de referência nulos. O padrão é **true**.  
  
### <a name="example"></a>Exemplo  
 O **Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator** propriedade permite que você marcar um método que permite uma alteração no estado de uma instância de um UDT. A [!INCLUDE[tsql](../../includes/tsql-md.md)] não permite definir duas propriedades de UDT na cláusula SET de uma instrução UPDATE. No entanto, é possível ter um método marcado como um modificador que altera os dois membros.  
  
> [!NOTE]  
>  Os métodos Mutator não são permitidos em consultas. Eles só podem ser chamados em instruções de atribuição ou de modificação de dados. Se um método marcado como modificador não retorne **void** (ou não é um **Sub** no Visual Basic), CREATE TYPE falhará com um erro.  
  
 A seguinte instrução supõe a existência de um **triângulos** UDT que tem um **girar** método. O seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução update invoca o **girar** método:  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 O **girar** método é decorado com o **SqlMethod** configuração de atributo **IsMutator** para **true** para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode marcar o método como um método modificador. O código também define **OnNullCall** para **false**, que indica para o servidor que o método retorna uma referência nula (**nada** no Visual Basic) se houver da entrada os parâmetros são referências nulas.  
  
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
 Ao implementar uma UDT com um formato definido pelo usuário, você deve implementar **leitura** e **gravar** métodos que implementam a interface Microsoft.SqlServer.Server.IBinarySerialize para manipular a serialização e desserializar os dados UDT. Você também deve especificar o **MaxByteSize** propriedade o **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
### <a name="the-currency-udt"></a>A UDT Currency  
 O **moeda** UDT é incluído com os exemplos CLR que podem ser instalados com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 O **moeda** UDT oferece suporte à manipulação de valores em dinheiro no sistema monetário de uma determinada cultura. Você deve definir dois campos: um **cadeia de caracteres** para **CultureInfo**, que especifica quem emitiu a moeda (en-us, por exemplo) e um **decimal** para  **CurrencyValue**, a quantidade de dinheiro.  
  
 Embora não seja usada pelo servidor para realizar comparações, o **moeda** UDT implementa o **System. IComparable** interface, que expõe um único método,  **System.IComparable.CompareTo**. Isso é usado do lado de cliente, em situações nas quais é desejável comparar com precisão ou ordenar valores de moeda dentro de culturas.  
  
 O código em execução no CLR compara a cultura separadamente do valor de moeda. Para o código [!INCLUDE[tsql](../../includes/tsql-md.md)], as seguintes ações determinam a comparação:  
  
1.  Definir o **IsByteOrdered** atributo como true, que informa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar a representação binária mantida em disco para comparações.  
  
2.  Use o **gravar** método para o **moeda** UDT para determinar como a UDT é mantida em disco e, portanto, como valores UDT são comparados e ordenados para [!INCLUDE[tsql](../../includes/tsql-md.md)] operações.  
  
3.  Salve o **moeda** UDT usando o seguinte formato binário:  
  
    1.  Salve a cultura como uma cadeia de caracteres codificada UTF-16 para bytes de 0 a 19 com preenchimento à direita com caracteres nulos.  
  
    2.  Use bytes 20 e acima para conter o valor decimal da moeda.  
  
 O propósito do preenchimento é assegurar que a cultura seja totalmente separada do valor de moeda, para que quando uma UDT seja comparada com outra no código [!INCLUDE[tsql](../../includes/tsql-md.md)], os bytes de cultura sejam comparados com os bytes de cultura e os valores de byte da moeda, com os valores de byte da moeda.  
  
 Para o código completo listagem para o **moeda** UDT, siga as instruções para instalar o CLR amostras em [exemplos do mecanismo de banco de dados do SQL Server](http://msftengprodsamples.codeplex.com/).  
  
### <a name="currency-attributes"></a>Atributos Currency  
 O **moeda** UDT é definido com os seguintes atributos.  
  
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
 Quando você escolhe **UserDefined** formato de serialização, você também deve implementar o **IBinarySerialize** interface e criar seu próprio **leitura** e **de gravação**  métodos. Os procedimentos a seguir do **moeda** uso UDT de **System.IO.BinaryReader** e **System.IO.BinaryWriter** para ler e gravar na UDT.  
  
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
  
 Para o código completo listagem para o **moeda** UDT, consulte [exemplos do mecanismo de banco de dados do SQL Server](http://msftengprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Consulte também  
 [Criando um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
