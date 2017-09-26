---
title: "Carregando a saída de um pacote Local | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
caps.latest.revision: 66
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 41de742c987d9f043f3dd247ee84af6a3eaf365b
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="loading-the-output-of-a-local-package"></a>Carregando a saída de um pacote local
  Aplicativos cliente podem ler a saída de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes quando a saída é salva em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destinos usando [!INCLUDE[vstecado](../../includes/vstecado-md.md)], ou quando a saída é salva em um destino de arquivo simples usando as classes de **System.IO** namespace. Entretanto, um aplicativo cliente também consegue ler a saída de um pacote diretamente da memória, sem precisar de uma etapa intermediária para manter os dados. A chave para essa solução é o **Microsoft.SqlServer.Dts.DtsClient** namespace, que contém implementações especializadas do **IDbConnection**, **IDbCommand**, e **IDbDataParameter** interfaces do **System. Data** namespace. O assembly Microsoft.SqlServer.Dts.DtsClient.dll é instalado por padrão em **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**.  
  
> [!NOTE]  
>  O procedimento descrito neste tópico requer que a propriedade DelayValidation da tarefa de fluxo de dados e de todos os objetos pai ser definido como seu valor padrão de **False**.  
  
## <a name="description"></a>Description  
 Esse procedimento demonstra como desenvolver um aplicativo cliente em código gerenciado que carrega a saída de um pacote com um destino do DataReader diretamente da memória. As etapas resumidas aqui são demonstradas no código de exemplo que segue.  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>Para carregar a saída de pacote de dados em um aplicativo cliente  
  
1.  No pacote, configure um destino do DataReader para receber a saída que você quer ler no aplicativo cliente. Dê ao destino do DataReader um nome descritivo, pois você usará esse nome em seu aplicativo cliente posteriormente. Anote o nome do destino do DataReader.  
  
2.  No projeto de desenvolvimento, defina uma referência o **Microsoft.SqlServer.Dts.DtsClient** namespace pela localização do assembly **Microsoft.SqlServer.Dts.DtsClient.dll**. Por padrão, este assembly é instalado em **C:\Program Files\Microsoft SQL Server\100\DTS\Binn**. Importe o namespace em seu código usando o c# **usando** ou [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **Imports** instrução.  
  
3.  Em seu código, crie um objeto do tipo **DtsClient.DtsConnection** com uma cadeia de caracteres de conexão que contém os parâmetros de linha de comando necessários para **dtexec.exe** para executar o pacote. Para saber mais, veja [dtexec Utility](../../integration-services/packages/dtexec-utility.md). Em seguida, abra a conexão com essa cadeia de conexão. Você também pode usar o **dtexecui** utilitário para criar a cadeia de caracteres de conexão necessária visualmente.  
  
    > [!NOTE]  
    >  O código de exemplo demonstra o carregamento do pacote do sistema de arquivos usando a sintaxe `/FILE <path and filename>`. Contudo, você também pode carregar o pacote do banco de dados MSDB usando a sintaxe `/SQL <package name>` ou do repositório de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando a sintaxe `/DTS \<folder name>\<package name>`.  
  
4.  Criar um objeto do tipo **DtsClient.DtsCommand** que usa criado anteriormente **DtsConnection** e defina seu **CommandText** propriedade para o nome do DataReader destino do pacote. Em seguida, chame o **ExecuteReader** método do objeto de comando para carregar os resultados do pacote em um DataReader novo.  
  
5.  Opcionalmente, você pode parametrizar indiretamente a saída do pacote usando a coleção de **DtsDataParameter** objetos o **DtsCommand** objeto para passar valores para variáveis definidas no pacote. No pacote, você pode usar essas variáveis como parâmetros de consulta ou em expressões para afetar os resultados retornados para o destino do DataReader. Você deve definir essas variáveis no pacote de **DtsClient** namespace antes que você pode usá-los com o **DtsDataParameter** objeto de um aplicativo cliente. (Talvez seja necessário clicar o **escolher colunas de variáveis** botão da barra de ferramentas no **variáveis** janela para exibir o **Namespace** coluna.) No código do cliente, quando você adiciona um **DtsDataParameter** para o **parâmetros** coleção do **DtsCommand**, omita a referência ao namespace DtsClient do nome de variável . Por exemplo:  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  Chamar o **leitura** método do DataReader repetidamente conforme necessário para executar um loop pelas linhas de dados de saída. Use os dados ou salve-os para serem usados posteriormente no aplicativo cliente.  
  
    > [!IMPORTANT]  
    >  O **leitura** método dessa implementação do DataReader retorna **true** mais uma vez após a última linha de dados foi lido. Isso dificulta o uso do código usual que percorre o DataReader enquanto **leitura** retorna **true**. Se o seu código tentar fechar o DataReader ou a conexão depois de ler o número esperado de linhas, sem uma chamada adicional final para o **leitura** método, o código gerará uma exceção sem tratamento. No entanto, se o seu código tentar ler dados nessa iteração final através de um loop, quando **leitura** ainda retorna **true** , mas a última linha foi passada, o código gerará sem tratamento ** ApplicationException** com a mensagem "o IDataReader do SSIS é após o fim do conjunto de resultados". Esse comportamento é diferente de outras implementações do DataReader. Portanto, ao usar um loop para ler as linhas no DataReader enquanto **leitura** retorna **true**, necessárias para escrever código para pegar, testar e descartar essa previsto ** ApplicationException** na última chamada bem-sucedida para o **leitura** método. Ou, se você souber com antecedência o número de linhas esperado, você pode processar as linhas e, em seguida, chamar o **leitura** mais uma vez antes de fechar o DataReader e a conexão.  
  
7.  Chamar o **Dispose** método o **DtsCommand** objeto. Isso é particularmente importante se você usou qualquer **DtsDataParameter** objetos.  
  
8.  Feche o DataReader e os objetos de conexão.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir executa um pacote que calcula um único valor de agregação, salva esse valor em um destino do DataReader e o lê do DataReader e o exibe em uma caixa de texto em um formulário do Windows.  
  
 O uso de parâmetros não é necessário ao carregar a saída de um pacote em um aplicativo cliente. Se você não quiser usar um parâmetro, você pode omitir o uso da variável no **DtsClient** namespace e omitir o código que usa o **DtsDataParameter** objeto.  
  
#### <a name="to-create-the-test-package"></a>Para criar o pacote de teste  
  
1.  Crie um novo pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O código de exemplo usa "DtsClientWParamPkg.dtsx" como o nome do pacote.  
  
2.  Adicione uma variável do tipo Cadeia de caracteres ao namespace DtsClient. O código de exemplo usa País como nome da variável. (Talvez seja necessário clicar o **escolher colunas de variáveis** botão da barra de ferramentas no **variáveis** janela para exibir o **Namespace** coluna.)  
  
3.  Adicione um gerenciador de conexões do OLE DB que se conecta ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
4.  Acrescente uma tarefa de fluxo de dados ao pacote e alterne para a superfície de design de Fluxo de Dados.  
  
5.  Adicione uma origem de OLE DB ao fluxo de dados e configure-a para usar o gerenciador de conexões OLE DB criado anteriormente, e o seguinte comando SQL:  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  Clique em **parâmetros** e, além de **definir parâmetros de consulta** caixa de diálogo caixa, mapeie o único parâmetro de entrada na consulta, Parameter0, para a variável dtsclient:: Country.  
  
7.  Acrescente uma transformação Agregação ao fluxo de dados e conecte a saída da origem de OLE DB à transformação. Abra o Editor de Transformação Agregação e configure-o para realizar uma operação “Contar todas” em todas as colunas de entrada (*) e gerar o valor agregado com o alias CustomerCount.  
  
8.  Acrescente um destino de DataReader ao fluxo de dados e conecte a saída da transformação Agregação a esse destino. O código de exemplo usa "DataReaderDest" como o nome do DataReader. Selecione a única coluna de entrada disponível, CustomerCount, para o destino.  
  
9. Salve o pacote. O aplicativo de teste criado em seguida executará o pacote e recuperará sua saída diretamente da memória.  
  
#### <a name="to-create-the-test-application"></a>Para criar o aplicativo de teste  
  
1.  Crie um novo aplicativo Windows Forms.  
  
2.  Adicione uma referência para o **Microsoft.SqlServer.Dts.DtsClient** namespace navegando até o assembly do mesmo nome em **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**.  
  
3.  Copie e cole o código de exemplo seguinte no módulo de código para o formulário.  
  
4.  Modificar o valor da **dtexecArgs** variável conforme necessário para que ele contém os parâmetros de linha de comando necessários por **dtexec.exe** para executar o pacote. O código de exemplo carrega o pacote do sistema de arquivos.  
  
5.  Modificar o valor da **dataReaderName** variável conforme necessário para que ele contém o nome do destino DataReader no pacote.  
  
6.  Coloque um botão e uma caixa de texto no formulário. O código de exemplo usa **btnRun** como o nome do botão e **txtResults** como o nome da caixa de texto.  
  
7.  Execute o aplicativo e clique no botão. Após uma pequena pausa, enquanto o pacote é executado, você deverá ver o valor de agregação calculado pelo pacote (a contagem de clientes no Canadá) exibido na caixa de texto do formulário.  
  
### <a name="sample-code"></a>Código de exemplo  
  
```vb  
Imports System.Data  
Imports Microsoft.SqlServer.Dts.DtsClient  
  
Public Class Form1  
  
  Private Sub btnRun_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnRun.Click  
  
    Dim dtexecArgs As String  
    Dim dataReaderName As String  
    Dim countryName As String  
  
    Dim dtsConnection As DtsConnection  
    Dim dtsCommand As DtsCommand  
    Dim dtsDataReader As IDataReader  
    Dim dtsParameter As DtsDataParameter  
  
    Windows.Forms.Cursor.Current = Cursors.WaitCursor  
  
    dtexecArgs = "/FILE ""C:\...\DtsClientWParamPkg.dtsx"""  
    dataReaderName = "DataReaderDest"  
    countryName = "Canada"  
  
    dtsConnection = New DtsConnection()  
    With dtsConnection  
      .ConnectionString = dtexecArgs  
      .Open()  
    End With  
  
    dtsCommand = New DtsCommand(dtsConnection)  
    dtsCommand.CommandText = dataReaderName  
  
    dtsParameter = New DtsDataParameter("Country", DbType.String)  
    dtsParameter.Direction = ParameterDirection.Input  
    dtsCommand.Parameters.Add(dtsParameter)  
  
    dtsParameter.Value = countryName  
  
    dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default)  
  
    With dtsDataReader  
      .Read()  
      txtResults.Text = .GetInt32(0).ToString("N0")  
    End With  
  
    'After reaching the end of data rows,  
    ' call the Read method one more time.  
    Try  
      dtsDataReader.Read()  
    Catch ex As Exception  
      MessageBox.Show("Exception on final call to Read method:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception on final call to Read method", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    ' The following method is a best practice, and is  
    '  required when using DtsDataParameter objects.  
    dtsCommand.Dispose()  
  
    Try  
      dtsDataReader.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing DataReader:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing DataReader", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Try  
      dtsConnection.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing connection:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing connection", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Windows.Forms.Cursor.Current = Cursors.Default  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Data;  
using Microsoft.SqlServer.Dts.DtsClient;  
  
namespace DtsClientWParamCS  
{  
  public partial class Form1 : Form  
  {  
    public Form1()  
    {  
      InitializeComponent();  
      this.btnRun.Click += new System.EventHandler(this.btnRun_Click);  
    }  
  
    private void btnRun_Click(object sender, EventArgs e)  
    {  
      string dtexecArgs;  
      string dataReaderName;  
      string countryName;  
  
      DtsConnection dtsConnection;  
      DtsCommand dtsCommand;  
      IDataReader dtsDataReader;  
      DtsDataParameter dtsParameter;  
  
      Cursor.Current = Cursors.WaitCursor;  
  
      dtexecArgs = @"/FILE ""C:\...\DtsClientWParamPkg.dtsx""";  
      dataReaderName = "DataReaderDest";  
      countryName = "Canada";  
  
      dtsConnection = new DtsConnection();  
      {  
        dtsConnection.ConnectionString = dtexecArgs;  
        dtsConnection.Open();  
      }  
  
      dtsCommand = new DtsCommand(dtsConnection);  
      dtsCommand.CommandText = dataReaderName;  
  
      dtsParameter = new DtsDataParameter("Country", DbType.String);  
      dtsParameter.Direction = ParameterDirection.Input;  
      dtsCommand.Parameters.Add(dtsParameter);  
  
      dtsParameter.Value = countryName;  
  
      dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default);  
  
      {  
        dtsDataReader.Read();  
        txtResults.Text = dtsDataReader.GetInt32(0).ToString("N0");  
      }  
  
      //After reaching the end of data rows,  
      // call the Read method one more time.  
      try  
      {  
        dtsDataReader.Read();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception on final call to Read method:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception on final call to Read method", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      // The following method is a best practice, and is  
      //  required when using DtsDataParameter objects.  
      dtsCommand.Dispose();  
  
      try  
      {  
        dtsDataReader.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing DataReader:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing DataReader", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      try  
      {  
        dtsConnection.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing connection:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing connection", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      Cursor.Current = Cursors.Default;  
  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre as diferenças entre execução Local e remota](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Carregando e executando um pacote Local programaticamente](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Carregar e executar um pacote remoto programaticamente](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  
