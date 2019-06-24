---
title: Usar o ADO com o OLE DB Driver para SQL Server | Microsoft Docs
description: Usar o ADO com o OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 1906ad25e9bb170b8979f44757ec5742ad9ec6c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778051"
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>Usando o ADO com o OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Para usufruir os novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] como, por exemplo, MARS (conjuntos de resultados ativos múltiplos), notificações de consulta, UDTs (tipos definidos pelo usuário) ou o novo tipo de dados **xml**, os aplicativos existentes que usam o ADO (ActiveX Data Objects) devem usar o OLE DB Driver for SQL Server como o provedor de acesso a dados.  
  
 Para permitir que o ADO use os novos recursos de versões recentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], foram feitas algumas melhorias no OLE DB Driver for SQL Server, que estende os principais recursos do OLE DB. Essas melhorias permitem que os aplicativos ADO usem recursos mais novos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e consumam dois tipos de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** e **udt**. Essas melhorias também exploram as melhorias feitas nos tipos de dados **varchar**, **nvarchar** e **varbinary**. O OLE DB Driver for SQL Server adiciona a propriedade de inicialização SSPROP_INIT_DATATYPECOMPATIBILITY ao conjunto de propriedades DBPROPSET_SQLSERVERDBINIT a ser usada por aplicativos ADO, de modo que os novos tipos de dados sejam expostos de maneira compatível com o ADO. Além disso, o Driver do OLE DB para SQL Server também define uma nova conexão palavra-chave cadeia chamada **DataTypeCompatibility** que é definido na cadeia de conexão.  

> [!NOTE]  
>  Os aplicativos do ADO existentes podem acessar e atualizar valores de XML, UDT, de campo binário e de texto grandes usando o provedor SQLOLEDB. Os novos tipos de dados **varchar(max)** , **nvarchar(max)** e **varbinary(max)** maiores são retornados como tipos do ADO **adLongVarChar**, **adLongVarWChar** e **adLongVarBinary**, respectivamente. As colunas XML são retornadas como **adLongVarChar**, e as colunas UDT, como **adVarBinary**. No entanto, se você usar o Driver do OLE DB para SQL Server (MSOLEDBSQL) em lugar do SQLOLEDB, você precisa certificar-se de definir as **DataTypeCompatibility** palavra-chave como "80" para que os novos tipos de dados sejam mapeados corretamente para os tipos de dados do ADO.  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>Habilitar o Driver do OLE DB para SQL Server do ADO  
 Para habilitar o uso do OLE DB Driver for SQL Server, os aplicativos ADO precisarão implementar as seguintes palavras-chave nas cadeias de conexão:  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 Para saber mais sobre palavras-chave da cadeia de conexão do ADO com suporte no OLE DB Driver para SQL Server, confira [Usar palavras-chave da cadeia de conexão com o OLE DB Driver para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  

 Este é um exemplo do estabelecimento de uma cadeia de conexão ADO totalmente habilitada para funcionar com o OLE DB Driver for SQL Server, incluindo a habilitação do recurso MARS:  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  

## <a name="examples"></a>Exemplos  
 As seções a seguir fornecem exemplos de como você pode usar o ADO com o Driver do OLE DB para SQL Server.  

### <a name="retrieving-xml-column-data"></a>Recuperando dados da coluna XML  
 Neste exemplo, um conjunto de registros é usado para recuperar e exibir os dados de uma coluna XML no banco de dados de exemplo **AdventureWorks** do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
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

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
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
 Neste exemplo, a cadeia de conexão é criada para habilitar o MARS por meio do OLE DB Driver for SQL Server e, em seguida, dois objetos de conjunto de registros são criados para serem executados usando a mesma conexão.  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
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

 Em versões anteriores do provedor OLE DB, esse código faria com que uma conexão implícita fosse criada na segunda execução porque apenas um conjunto de resultados ativo podia ser aberto por conexão. Como a conexão implícita não foi agrupada no pool de conexões OLE DB, isso causaria uma sobrecarga adicional. Com o recurso MARS exposto pelo OLE DB Driver for SQL Server, você obtém vários resultados ativos na única conexão.  

## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
