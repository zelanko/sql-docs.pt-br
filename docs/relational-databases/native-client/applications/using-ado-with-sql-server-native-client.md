---
title: Usando o ADO com o Cliente Nativo do Servidor SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 81f7ff71643776eb3116dab0157a4f2cd32b788a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302457"
---
# <a name="using-ado-with-sql-server-native-client"></a>Usando o ADO com SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para aproveitar os novos recursos [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduzidos em vários conjuntos de resultados ativos (MARS), notificações de consulta, tipos definidos pelo usuário (UDTs) ou o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] novo tipo de dados **xml,** os aplicativos existentes que usam ODO (ActiveX Data Objects, objetos de dados do ActiveX) devem usar o provedor OLE DB do Cliente Nativo como seu provedor de acesso a dados.  
  
 Caso você não precise usar nenhum dos novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], não há necessidade de usar o provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. É possível continuar usando o provedor de acesso a dados atual, normalmente SQLOLEDB. Caso esteja aperfeiçoando um aplicativo existente e precise usar os novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], você deve usar o provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
> [!NOTE]  
>  Caso você esteja desenvolvendo um novo aplicativo, é recomendável considerar o uso do ADO.NET e do provedor de dados .NET Framework do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], e não o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, para acessar todos os novos recursos de versões recentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações sobre o provedor de dados .NET Framework do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte a documentação do SDK do .NET Framework referente ao ADO.NET.  
  
 Para permitir que o ADO use os novos recursos de versões recentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], foram feitas algumas melhorias no provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, que estende os principais recursos do OLE DB. Essas melhorias permitem que os aplicativos ADO usem recursos mais novos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e consumam dois tipos de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** e **udt**. Essas melhorias também exploram as melhorias feitas nos tipos de dados **varchar**, **nvarchar** e **varbinary**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]O Native Client adiciona a propriedade de inicialização SSPROP_INIT_DATATYPECOMPATIBILITY ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT para uso por aplicativos ADO para que os novos tipos de dados sejam expostos de forma compatível com o ADO. Além disso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o provedor Nativo Cliente OLE DB também define uma nova palavra-chave de seqüência de conexões chamada **DataTypeCompatibility** que está definida na seqüência de conexões.  
  
> [!NOTE]  
>  Os aplicativos do ADO existentes podem acessar e atualizar valores de XML, UDT, de campo binário e de texto grandes usando o provedor SQLOLEDB. Os novos tipos de dados **varchar(max)**, **nvarchar(max)** e **varbinary(max)** maiores são retornados como tipos do ADO **adLongVarChar**, **adLongVarWChar** e **adLongVarBinary**, respectivamente. As colunas XML são retornadas como **adLongVarChar**, e as colunas UDT, como **adVarBinary**. No entanto, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se você usar o provedor OLE DB do Cliente Nativo (SQLNCLI11) em vez do SQLOLEDB, você precisa ter certeza de definir a palavra-chave **DataTypeCompatibility** como "80" para que os novos tipos de dados mapeiem corretamente para os tipos de dados ADO.  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>Habilitando o SQL Server Native Client no ADO  
 Para habilitar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o uso do Cliente Nativo, os aplicativos ADO precisarão implementar as seguintes palavras-chave em suas strings de conexão:  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 Para obter mais informações sobre as palavras-chave [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de seqüência de conexões ADO suportadas no Cliente Nativo, consulte [Usando palavras-chave de seqüência de conexão com o Cliente Nativo do Servidor SQL](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 O seguinte é um exemplo de estabelecer uma seqüência de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conexões ADO totalmente habilitada para trabalhar com o Cliente Nativo, incluindo a habilitação do recurso MARS:  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  
  
## <a name="examples"></a>Exemplos  
 As seções a seguir fornecem exemplos de como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] você pode usar o ADO com o provedor Native Client OLE DB.  
  
### <a name="retrieving-xml-column-data"></a>Recuperando dados da coluna XML  
 Neste exemplo, um conjunto de registros é usado para recuperar e exibir os dados de uma coluna XML no banco de dados de exemplo  **AdventureWorks** do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _   
         & "DataTypeCompatibility=80;"  
  
con.Open  
  
' Get the xml data as a recordset.  
Set rst.ActiveConnection = con  
rst.Source = "SELECT AdditionalContactInfo FROM Person.Contact " _  
   & "WHERE AdditionalContactInfo IS NOT NULL"  
rst.Open  
  
' Display the data in the recordset.  
While (Not rst.EOF)  
   sXMLResult = rst.Fields("AdditionalContactInfo").Value  
   Debug.Print (sXMLResult)  
   rst.MoveNext  
End While  
  
con.Close  
Set con = Nothing  
```  
  
> [!NOTE]  
>  Não há suporte para a filtragem do conjunto de registros com colunas XML. Se ela for usada, será retornado um erro.  
  
### <a name="retrieving-udt-column-data"></a>Recuperando dados da coluna UDT  
 Neste exemplo, um objeto **Command** é usado para executar uma consulta SQL que retorna um UDT, os dados UDT são atualizados e, em seguida, os novos dados são inseridos novamente no banco de dados. Este exemplo supõe que o UDT **Point** já foi registrado no banco de dados.  
  
```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;"  
  
con.Open  
  
' Get the UDT value.  
Set cmd.ActiveConnection = con  
cmd.CommandText = "SELECT ID, Pnt FROM dbo.Points.ToString()"  
Set rst = cmd.Execute  
strTempID = rst.Fields(0).Value  
strOldUDT = rst.Fields(1).Value  
  
' Do something with the UDT by adding i to each point.  
arytempUDT = Split(strOldUDT, ",")  
i = 3  
strNewUDT = LTrim(Str(Int(aryTempUDT(0)) + i)) + "," + _  
   LTrim(Str(Int(aryTempUDT(1)) + i))  
  
' Insert the new value back into the database.  
cmd.CommandText = "UPDATE dbo.Points SET Pnt = '" + strNewUDT + _  
   "' WHERE ID = '" + strTempID + "'"  
cmd.Execute  
  
con.Close  
Set con = Nothing  
```  
  
### <a name="enabling-and-using-mars"></a>Habilitando e usando MARS  
 Neste exemplo, a seqüência de conexões [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é construída para habilitar o MARS através do provedor Native Client OLE DB e, em seguida, dois objetos de conjunto de registros são criados para serem executados usando a mesma conexão.  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
  
Dim recordset1 As New ADODB.Recordset  
Dim recordset2 As New ADODB.Recordset  
  
Dim recordsaffected As Integer  
Set recordset1 =  con.Execute("SELECT * FROM Table1", recordsaffected, adCmdText)  
Set recordset2 =  con.Execute("SELECT * FROM Table2", recordsaffected, adCmdText)  
  
con.Close  
Set con = Nothing  
```  
  
 Em versões anteriores do provedor OLE DB, esse código faria com que uma conexão implícita fosse criada na segunda execução porque apenas um conjunto de resultados ativo podia ser aberto por conexão. Como a conexão implícita não foi agrupada no pool de conexões OLE DB, isso causaria uma sobrecarga adicional. Com o recurso MARS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exposto pelo provedor Native Client OLE DB, você obtenha vários resultados ativos em uma conexão.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
