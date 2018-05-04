---
title: Usando o ADO com o Driver do OLE DB para SQL Server | Microsoft Docs
description: Usando o ADO com o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 48f16f274d616489a5b7a796c6327ce59427f4a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>Usando o ADO com o Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Para tirar proveito dos novos recursos introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] como vários conjuntos de resultados ativos (MARS), as notificações de consulta, tipos definidos pelo usuário (UDTs) ou o novo **xml** tipo de dados, os aplicativos existentes que usam o ActiveX Data Objects (ADO) devem usar o Driver OLE DB para SQL Server como seu provedor de acesso de dados.  
  
 Para habilitar o ADO para usar os novos recursos de versões recentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], algumas melhorias foram feitas para o Driver OLE DB para SQL Server que estende os recursos principais do OLE DB. Essas melhorias permitem que os aplicativos ADO usem mais recente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recursos e consumam dois tipos de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** e **udt**. Esses também exploram melhorias feitas para o **varchar**, **nvarchar**, e **varbinary** tipos de dados. OLE DB Driver para SQL Server adiciona a propriedade de inicialização SSPROP_INIT_DATATYPECOMPATIBILITY para o conjunto de propriedades DBPROPSET_SQLSERVERDBINIT definido para uso por aplicativos do ADO para que os novos tipos de dados são expostos de maneira compatível com o ADO. Além disso, o Driver OLE DB para SQL Server também define uma nova conexão cadeia palavra-chave denominada **DataTypeCompatibility** que é definido na cadeia de conexão.  

> [!NOTE]  
>  Os aplicativos do ADO existentes podem acessar e atualizar valores de XML, UDT, de campo binário e de texto grandes usando o provedor SQLOLEDB. O novo maior **varchar (max)**, **nvarchar (max)**, e **varbinary (max)** tipos de dados são retornados como tipos do ADO **adLongVarChar**, **adLongVarWChar** e **adLongVarBinary** respectivamente. Colunas XML são retornadas como **adLongVarChar**, e colunas UDT são retornadas como **adVarBinary**. No entanto, se você usar o Driver OLE DB para SQL Server (MSOLEDBSQL) em lugar do SQLOLEDB, você precisa certificar-se de definir o **DataTypeCompatibility** palavra-chave como "80" para que os novos tipos de dados sejam mapeados corretamente para os tipos de dados do ADO.  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>Habilitar o Driver do OLE DB para SQL Server do ADO  
 Para habilitar o uso do Driver do OLE DB para SQL Server, os aplicativos ADO serão necessário implementar as seguintes palavras-chave nas cadeias de conexão:  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 Para obter mais informações sobre o ADO com suporte no Driver do OLE DB para SQL Server, as palavras-chave de cadeia de conexão consulte [usando Conexão String Keywords com OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  

 Este é um exemplo do estabelecimento de uma cadeia de caracteres de conexão ADO totalmente habilitada para trabalhar com o Driver do OLE DB para SQL Server, incluindo a habilitação do recurso MARS:  

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
 As seções a seguir fornecem exemplos de como você pode usar o ADO com o Driver OLE DB para SQL Server.  

### <a name="retrieving-xml-column-data"></a>Recuperando dados da coluna XML  
 Neste exemplo, um conjunto de registros é usado para recuperar e exibir os dados de uma coluna XML no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** banco de dados de exemplo.  

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
 Neste exemplo, um **comando** objeto é usado para executar uma consulta SQL que retorna uma UDT, os dados UDT são atualizados e, em seguida, os novos dados são inseridos novamente no banco de dados. Este exemplo supõe que o **ponto** UDT já foi registrado no banco de dados.  

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
 Neste exemplo, a cadeia de caracteres de conexão é criada para habilitar MARS por meio do Driver OLE DB para SQL Server e, em seguida, os dois objetos de conjunto de registros são criados para serem executados usando a mesma conexão.  

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

 Em versões anteriores do provedor OLE DB, esse código faria com que uma conexão implícita fosse criada na segunda execução porque apenas um conjunto de resultados ativo podia ser aberto por conexão. Como a conexão implícita não foi agrupada no pool de conexões OLE DB, isso causaria uma sobrecarga adicional. Com o recurso MARS exposto pelo Driver OLE DB para SQL Server, você obtém vários resultados ativos na conexão a um.  

## <a name="see-also"></a>Consulte também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
