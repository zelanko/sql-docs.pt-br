---
title: Funções com valor escalar CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
caps.latest.revision: 81
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9c15ca3b97b63d3f472705c5c7de0e9fe6d59779
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703177"
---
# <a name="clr-scalar-valued-functions"></a>Funções de valor escalar CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Uma função de valor escalar (SVF) retorna um único valor, como uma cadeia de caracteres, um inteiro ou um valor de bit. Você pode criar funções de valor escalar definidas pelo usuário em código gerenciado usando qualquer linguagem de programação do .NET Framework. Essas funções são acessíveis a [!INCLUDE[tsql](../../includes/tsql-md.md)] ou outro código gerenciado. Para obter informações sobre as vantagens da integração CLR e escolhendo entre código gerenciado e [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [visão geral da integração do CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>Requisitos das funções de valor escalar do CLR  
 As SVFs do .NET Framework são implementadas como métodos em uma classe de um assembly do .NET Framework. Os parâmetros de entrada e o tipo retornado de uma SVF podem ser qualquer um dos tipos de dados escalares suportados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto **varchar**, **char**, **rowversion**, **texto**, **ntext**, **imagem**, **timestamp**, **tabela**, ou **cursor** . As SVFs devem garantir uma correspondência entre o tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o tipo de dados de retorno do método de implementação. Para obter mais informações sobre conversões de tipo, consulte [mapeamento de dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 Ao implementar uma SVF do .NET Framework em uma linguagem do .NET Framework, o atributo personalizado **SqlFunction** pode ser especificado para incluir informações adicionais sobre a função. O atributo **SqlFunction** indica se a função acessa ou modifica os dados, se é determinística e se envolve operações de ponto flutuante.  
  
 Funções de valor escalar definidas pelo usuário podem ser determinísticas ou não. Uma função determinística sempre retorna o mesmo resultado quando chamada com um conjunto de parâmetros de entrada específico. Uma função não determinística pode retornar resultados diferentes quando chamada com um conjunto de parâmetros de entrada específico.  
  
> [!NOTE]  
>  Não marque uma função como determinística se ela sempre produzir os mesmos valores de saída, considerando os mesmos valores de entrada e o mesmo estado do banco de dados. A marcação de uma função como determinística, quando a função, de fato, não é pode resultar em exibições indexadas e colunas computadas danificadas. Você marca uma função como determinística definindo a propriedade **IsDeterministic** como true.  
  
### <a name="table-valued-parameters"></a>Parâmetros com valor de tabela  
 Os TVPs (parâmetros com valor de tabela), ou seja, tipos de tabela definidos pelo usuário transmitidos para um procedimento ou uma função, oferecem uma maneira eficiente de passar várias linhas de dados para o servidor. Os TVPs proporcionam funcionalidade semelhante para matrizes de parâmetro, porém com maior flexibilidade e integração com [!INCLUDE[tsql](../../includes/tsql-md.md)]. Eles também fornecem o potencial para melhor desempenho. Os TVPs também ajudam a reduzir o número de viagens de ida e volta para o servidor. Em vez de enviar várias solicitações ao servidor, como com uma lista de parâmetros escalares, os dados podem ser enviados ao servidor como um TVP. Um tipo de tabela definido pelo usuário não pode ser passado como um parâmetro com valor de tabela para, ou ser retornado de, um procedimento armazenado ou uma função gerenciada(o) que é executada(o) no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre TVPs, consulte [usar parâmetros &#40;mecanismo de banco de dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="example-of-a-clr-scalar-valued-function"></a>Exemplo de uma função de valor escalar do CLR  
 Eis uma SVF simples que acessa dados e retorna um valor inteiro:  
  
```csharp  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public class T  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static int ReturnOrderCount()  
    {  
        using (SqlConnection conn   
            = new SqlConnection("context connection=true"))  
        {  
            conn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
            return (int)cmd.ExecuteScalar();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public Class T  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReturnOrderCount() As Integer  
        Using conn As New SqlConnection("context connection=true")  
            conn.Open()  
            Dim cmd As New SqlCommand("SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
            Return CType(cmd.ExecuteScalar(), Integer)  
        End Using  
    End Function  
End Class  
```  
  
 A primeira linha de código referencia **Microsoft.SqlServer.Server** para acessar atributos e **System.Data.SqlClient** para acessar o namespace do ADO.NET. (Este namespace contém **SqlClient**, o .NET Framework Data Provider para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)  
  
 Em seguida, a função recebe o atributo personalizado **SqlFunction** , encontrado no namespace **Microsoft.SqlServer.Server** . O atributo personalizado indica se a UDF (função definida pelo usuário) usa ou não o provedor em processo para ler dados no servidor. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite que as UDFs atualizem, insiram ou excluam dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode otimizar a execução de uma UDF que não usa o provedor em processo. Isso é indicado com a definição de **DataAccessKind** como **DataAccessKind.None**. Na próxima linha, o método de destino é uma estática pública (compartilhada no Visual Basic .NET).  
  
 O **SqlContext** localizado na classe a **SQLServer** namespace, pode acessar um **SqlCommand** objeto com uma conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância que já está definida. Embora não seja usado aqui, o contexto de transação atual também está disponível por meio da API **System.Transactions** .  
  
 A maior parte das linhas de código no corpo da função deve parecer familiar aos desenvolvedores que já criaram aplicativos cliente que usam os tipos encontrados no namespace **System.Data.SqlClient** .  
  
 [C#]  
  
```  
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```  
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 O texto de comando apropriado é especificado com a inicialização do objeto **SqlCommand** . O exemplo anterior conta o número de linhas na tabela **SalesOrderHeader**. Em seguida, o método **ExecuteScalar** do objeto **cmd** é chamado. Isso retorna um valor do tipo **int** com base na consulta. Por fim, a contagem da ordem retorna ao chamador.  
  
 Caso seja salvo em um arquivo chamado FirstUdf.cs, esse código pode ser compilado como assembly da seguinte forma:  
  
 [C#]  
  
```  
csc.exe /t:library /out:FirstUdf.dll FirstUdf.cs   
```  
  
 [Visual Basic]  
  
```  
vbc.exe /t:library /out:FirstUdf.dll FirstUdf.vb  
```  
  
> [!NOTE]  
>  `/t:library` indica que uma biblioteca, e não um executável, deve ser produzida. Os executáveis não podem ser registrados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Objetos de banco de dados do Visual C++ compilados com **/clr: pure** não há suporte para execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, entre esses objetos de banco de dados estão funções de valor escalar.  
  
 A consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] e uma invocação de exemplo de registro do assembly e da UDF são:  
  
```  
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 Observe que o nome da função como exposto em [!INCLUDE[tsql](../../includes/tsql-md.md)] não precisa corresponder ao nome do método estático público de destino.  
  
## <a name="see-also"></a>Consulte também  
 [Mapeamento de dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [Visão geral de atributos personalizados de integração CLR](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [Funções definidas pelo usuário](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [Acesso aos dados dos objetos de banco de dados CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
