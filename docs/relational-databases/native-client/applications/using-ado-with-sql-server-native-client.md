---
title: Usando o ADO com SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7a09bd10314d8533152c7317682501df8b28eb9a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428285"
---
# <a name="using-ado-with-sql-server-native-client"></a>Usando o ADO com SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Para tirar proveito dos novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , como vários conjuntos de resultados ativos (MARS), as notificações de consulta, tipos definidos pelo usuário (UDTs) ou o novo **xml** tipo de dados, os aplicativos existentes que usam o ActiveX Data Objects (ADO) deve usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client como seu provedor de acesso de dados.  
  
 Caso você não precise usar nenhum dos novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], não há necessidade de usar o provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. É possível continuar usando o provedor de acesso a dados atual, normalmente SQLOLEDB. Caso esteja aperfeiçoando um aplicativo existente e precise usar os novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], você deve usar o provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
> [!NOTE]  
>  Caso você esteja desenvolvendo um novo aplicativo, é recomendável considerar o uso do ADO.NET e do provedor de dados .NET Framework do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], e não o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, para acessar todos os novos recursos de versões recentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações sobre o provedor de dados .NET Framework do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte a documentação do SDK do .NET Framework referente ao ADO.NET.  
  
 Para permitir que o ADO use os novos recursos de versões recentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], foram feitas algumas melhorias no provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, que estende os principais recursos do OLE DB. Esses aprimoramentos permitem que aplicativos ADO usem mais recente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recursos e consumir os dois tipos de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** e **udt**. Elas também exploram melhorias para o **varchar**, **nvarchar**, e **varbinary** tipos de dados. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client adiciona a propriedade de inicialização SSPROP_INIT_DATATYPECOMPATIBILITY ao propriedades DBPROPSET_SQLSERVERDBINIT a ser definido para uso por aplicativos do ADO para que os novos tipos de dados são expostos de maneira compatível com o ADO. Além disso, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client também define uma nova conexão palavra-chave cadeia chamada **DataTypeCompatibility** que é definido na cadeia de conexão.  
  
> [!NOTE]  
>  Os aplicativos do ADO existentes podem acessar e atualizar valores de XML, UDT, de campo binário e de texto grandes usando o provedor SQLOLEDB. O novo maiores **varchar (max)**, **nvarchar (max)**, e **varbinary (max)** tipos de dados são retornados como tipos do ADO **adLongVarChar**, **adLongVarWChar** e **adLongVarBinary** , respectivamente. Colunas XML são retornadas como **adLongVarChar**, e colunas UDT são retornadas como **adVarBinary**. No entanto, se você usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client (SQLNCLI11) em lugar do SQLOLEDB, você precisa certificar-se de definir o **DataTypeCompatibility** palavra-chave como "80" para que os novos tipos de dados sejam mapeados corretamente para os dados do ADO tipos.  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>Habilitando o SQL Server Native Client no ADO  
 Para habilitar o uso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, aplicativos do ADO deverão implementar as seguintes palavras-chave nas cadeias de conexão:  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 Para obter mais informações sobre o ADO conexões de cadeia de caracteres palavras-chave com suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, consulte [usando Conexão String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 A seguir está um exemplo do estabelecimento de uma cadeia de caracteres de conexão ADO totalmente habilitada para trabalhar com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, incluindo a habilitação do recurso MARS:  
  
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
 As seções a seguir fornecem exemplos de como você pode usar o ADO com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client.  
  
### <a name="retrieving-xml-column-data"></a>Recuperando dados da coluna XML  
 Neste exemplo, um conjunto de registros é usado para recuperar e exibir os dados de uma coluna XML na [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** banco de dados de exemplo.  
  
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
 Neste exemplo, uma **comando** objeto é usado para executar uma consulta SQL que retorna uma UDT, os dados UDT são atualizados e, em seguida, os novos dados são inseridos novamente no banco de dados. Este exemplo supõe que o **ponto** UDT já foi registrado no banco de dados.  
  
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
 Neste exemplo, a cadeia de caracteres de conexão é criada para habilitar MARS por meio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client e, em seguida, dois objetos de conjunto de registros são criados para serem executados usando a mesma conexão.  
  
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
  
 Em versões anteriores do provedor OLE DB, esse código faria com que uma conexão implícita fosse criada na segunda execução porque apenas um conjunto de resultados ativo podia ser aberto por conexão. Como a conexão implícita não foi agrupada no pool de conexões OLE DB, isso causaria uma sobrecarga adicional. Com o recurso MARS exposto pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client, você obtém vários resultados ativos na conexão a um.  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
