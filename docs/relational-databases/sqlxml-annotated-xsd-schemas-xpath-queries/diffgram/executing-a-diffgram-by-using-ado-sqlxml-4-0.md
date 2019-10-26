---
title: Executando um DiffGram usando ADO (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b3d0b352c31c7661a92cb53f8331d2a8e062aa8a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909351"
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>Executando um DiffGram usando o ADO (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este aplicativo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic usa o ADO para estabelecer uma conexão com uma instância do Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e então executar um DiffGram. Nesse aplicativo, o DiffGram e o esquema XSD são armazenados em um arquivo. O aplicativo carrega o DiffGram a partir do arquivo especificado. Você pode usar qualquer um dos DiffGrams (e o esquema XSD associado) descrito em [exemplos de DiffGram](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 Este é o processo para o aplicativo de exemplo:  
  
-   O objeto **Conn** (**ADODB. Conexão**) estabelece uma conexão com uma instância em execução do SQL Server em um servidor específico.  
  
-   O objeto **cmd** (**ADODB. Command**) é executado na conexão estabelecida.  
  
-   O dialeto do comando é definido como DBGUID_MSSQLXML.  
  
-   O DiffGram é copiado para o fluxo de comando (**strmIn**) de um arquivo.  
  
-   O fluxo de saída do comando é definido como o objeto **StrmOut** (**ADODB. Stream**) para receber todos os dados retornados.  
  
-   Ao usar o Provedor SQLOLEDB, por padrão, você obterá a funcionalidade do Microsoft SQLXML fornecida por Sqlxmlx.dll. Para usar Sqlxml4. dll com o provedor SQLOLEDB, a propriedade **Version do SQLXML** deve ser definida como **SQLXML. 4.0** no objeto de **conexão** do provedor SQLOLEDB.  
  
-   O comando (DiffGram) é executado.  
  
 O código a seguir é o aplicativo de exemplo.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão.  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Para uma pasta no seu computador, copie qualquer um dos DiffGrams e o esquema XSD correspondente de um dos exemplos em exemplos de [DiffGram](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
2.  Abra o Visual Basic e crie um projeto EXE padrão.  
  
3.  Adicione estas referências ao projeto:  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  Na caixa de ferramentas, clique em **CommandButton**e desenhe um botão no formulário.  
  
5.  Clique duas vezes no botão para editar o código e adicione o código do aplicativo que é fornecido no tópico.  
  
6.  Edite o código para especificar os nomes do DiffGram e do arquivo XSD. Edite também a cadeia de conexão, conforme apropriado.  
  
7.  Execute o aplicativo. O resultado da execução depende do DiffGram que você está executando.  

