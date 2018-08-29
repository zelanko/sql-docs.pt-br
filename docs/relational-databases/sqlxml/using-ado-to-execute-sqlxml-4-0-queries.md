---
title: Usando o ADO para executar o SQLXML 4.0 consultas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8e9243bac63901649e1794cdfe2c3d190ebb2435
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063278"
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>Usando o ADO para executar consultas do SQLXML 4.0
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Nas versões anteriores do SQLXML, o suporte à execução de consultas baseadas em HTTP era oferecido por meio de diretórios virtuais IIS SQLXML e do filtro ISAPI SQLXML. No SQLXML 4.0, esses componentes foram removidos já que uma funcionalidade semelhante é fornecida com os XML Web Services nativos introduzidos no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Como alternativa, você pode executar consultas e usar o SQLXML 4.0 com seus aplicativos baseados no COM, aproveitando as extensões SQLXML para ADO (ActiveX Data Objects) que foram introduzidas pela primeira vez no Microsoft Data Access Components (MDAC) 2.6 e versão posterior.  
  
 Este tópico demonstra o uso do SQLXML e ADO como parte de um aplicativo Visual Basic Scripting Edition (VBScript) (um script com a extensão de nome de arquivo. vbs). Ele fornece procedimentos iniciais de instalação que ajudam a recriar e testar exemplos de consulta na documentação do SQLXML 4.0.  
  
## <a name="creating-the-sqlxml-40-test-script"></a>Criando o script de teste SQLXML 4.0  
 Neste procedimento, você cria um arquivo VBScript (.vbs), Sqlxml4test.vbs, que pode ser usado para executar consultas SQLXML, aproveitando as extensões SQLXML ADO no ADO 2.6 e posterior.  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>Para criar o testador de consulta do SQLXML 4.0 usando ADO (VBScript).  
  
1.  Copie o código abaixo e cole-o em um arquivo de texto. Salve o arquivo como Sqlxml4test.vbs.  
  
    ```  
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  Atualize os valores de script a seguir para o exemplo que você está tentando testar e seu ambiente de teste.  
  
    -   Localize "`@@FILE_NAME@@`" e substitua-o pelo nome do seu arquivo de modelo.  
  
    -   Localize "`@@SERVER_NAME@@`" e substitua-o pelo nome da sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, "`(local)`" se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executado localmente).  
  
    -   Localize "`@@DATABASE_NAME@@`" e substitua-o pelo nome do banco de dados (por exemplo, "`AdventureWorks2012`" ou "`tempdb`").  
  
     Atualize qualquer outro valor se mencionado nas instruções específicas do exemplo que você está tentando recriar localmente em seu computador.  
  
3.  Salve o arquivo e feche-o.  
  
4.  Verifique se você criou outros arquivos, como modelos ou esquemas XML que são parte do exemplo que você está tentando recriar localmente em seu computador. Esses arquivos deveriam estar localizados no mesmo diretório onde você salvou o arquivo de script de teste (Sqlxml4test.vbs).  
  
5.  Siga as instruções da próxima seção sobre como usar o script de teste SQLXML 4.0.  
  
## <a name="using-the-sqlxml-40-test-script"></a>Usando o script de teste SQLXML 4.0  
 O procedimento a seguir descreve como usar os arquivos Sqlxml4test.vbs para testar as consultas de exemplo fornecidas nesta documentação.  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>Para usar o testador de consulta do SQLXML 4.0   
  
1.  Verifique se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está instalado, da seguinte maneira:  
  
    1.  Dos **inicie** , aponte para **configurações**e, em seguida, clique em **painel de controle**.  
  
    2.  No painel de controle, abra **adicionar ou remover programas**  
  
    3.  Na lista de programas instalados, verifique **Microsoft SQL Server Native Client** aparece na lista.  
  
        > [!NOTE]  
        >  Se você precisar instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, consulte [instalar o SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
2.  Verifique se a versão do MDAC instalada no computador cliente é a 2.6 ou mais recente. Se você precisar obter informações sobre a versão do MDAC, poderá usar a ferramenta Component Checker do MDAC, fornecida gratuitamente no site da Microsoft (www.microsoft.com). Para obter mais informações, pesquise em "MDAC Component Checker" no site da Microsoft.  
  
3.  Execute o script.  
  
     Você pode executar o arquivo VBScript na linha de comando usando Cscript.exe ou clicando duas vezes no arquivo Sqlxml4test.vbs para chamar o Windows Script Host (WScript.exe).  
  
     Durante sua execução, o script deverá exibir uma mensagem de alerta informando que poderá levar alguns minutos para ser executado antes de retornar e exibir os resultados da consulta. Quando o resultado for exibido, compare seu conteúdo com o dos resultados esperados para o exemplo.  
  
  
