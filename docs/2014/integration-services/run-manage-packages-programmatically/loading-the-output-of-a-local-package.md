---
title: Carregando a saída de um pacote local | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 57b318ac8062203bd11a0717a4c8077bca9880d3
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382044"
---
# <a name="loading-the-output-of-a-local-package"></a>Carregando a saída de um pacote local
  Aplicativos cliente podem ler a saída de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] quando a saída é salva em destinos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] ou quando a saída é salva em um destino de arquivo simples por meio das classes no namespace **System.IO**. Entretanto, um aplicativo cliente também consegue ler a saída de um pacote diretamente da memória, sem precisar de uma etapa intermediária para manter os dados. A chave para essa solução é o `Microsoft.SqlServer.Dts.DtsClient` namespace, que contém implementações especializadas da `IDbConnection`, `IDbCommand`, e **IDbDataParameter** interfaces do **deSystem.Data** namespace. O assembly Microsoft.SqlServer.Dts.DtsClient.dll é instalado por padrão em **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**.  
  
> [!NOTE]  
>  O procedimento descrito neste tópico exige que a propriedade DelayValidation da tarefa Fluxo de Dados e de qualquer objeto pai seja definida com seu valor padrão **False**.  
  
## <a name="description"></a>Descrição  
 Esse procedimento demonstra como desenvolver um aplicativo cliente em código gerenciado que carrega a saída de um pacote com um destino do DataReader diretamente da memória. As etapas resumidas aqui são demonstradas no código de exemplo que segue.  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>Para carregar a saída de pacote de dados em um aplicativo cliente  
  
1.  No pacote, configure um destino do DataReader para receber a saída que você quer ler no aplicativo cliente. Dê ao destino do DataReader um nome descritivo, pois você usará esse nome em seu aplicativo cliente posteriormente. Anote o nome do destino do DataReader.  
  
2.  No projeto de desenvolvimento, defina uma referência o `Microsoft.SqlServer.Dts.DtsClient` namespace, localizando o assembly **Microsoft.SqlServer.Dts.DtsClient.dll**. Por padrão, esse assembly é instalado em **C:\Program Files\Microsoft SQL Server\100\DTS\Binn**. Importe o namespace em seu código usando o c# `Using` ou o [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] `Imports` instrução.  
  
3.  No seu código, crie um objeto do tipo `DtsClient.DtsConnection` com uma cadeia de caracteres de conexão que contém os parâmetros de linha de comando necessários **dtexec.exe** para executar o pacote. Para saber mais, veja [dtexec Utility](../packages/dtexec-utility.md). Em seguida, abra a conexão com essa cadeia de conexão. Também use o utilitário **dtexecui** para criar a cadeia de conexão necessária visualmente.  
  
    > [!NOTE]  
    >  O código de exemplo demonstra o carregamento do pacote do sistema de arquivos usando a sintaxe `/FILE <path and filename>`. Contudo, você também pode carregar o pacote do banco de dados MSDB usando a sintaxe `/SQL <package name>` ou do repositório de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando a sintaxe `/DTS \<folder name>\<package name>`.  
  
4.  Crie um objeto do tipo `DtsClient.DtsCommand` que use o `DtsConnection` criado anteriormente e defina sua propriedade `CommandText` com o nome de destino do DataReader no pacote. Em seguida, chame o método `ExecuteReader` do objeto de comando para carregar os resultados do pacote em um DataReader novo.  
  
5.  Uma alternativa é parametrizar indiretamente a saída do pacote usando a coleção de objetos `DtsDataParameter` no objeto `DtsCommand` para passar valores para variáveis definidas no pacote. No pacote, você pode usar essas variáveis como parâmetros de consulta ou em expressões para afetar os resultados retornados para o destino do DataReader. Você deve definir essas variáveis no pacote na **DtsClient** namespace antes que você pode usá-los com o `DtsDataParameter` objeto de um aplicativo cliente. (Talvez você precise clicar no botão de barra de ferramentas **Escolher Colunas de Variáveis** na janela **Variáveis** para exibir a coluna **Namespace**.) Em seu código de cliente, quando você adicionar um `DtsDataParameter` à coleção `Parameters` do `DtsCommand`, omita a referência do namespace DtsClient do nome da variável. Por exemplo:  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  Chame repetidamente o método `Read` do DataReader, conforme necessário, para executar o loop pelas linhas de dados de saída. Use os dados ou salve-os para serem usados posteriormente no aplicativo cliente.  
  
    > [!IMPORTANT]  
    >  O método `Read` dessa implementação do DataReader retorna `true` uma vez mais depois que a última linha de dados é lida. Isso dificulta o uso do código usual que executa o loop no DataReader enquanto `Read` retorna `true`. Se seu código tentar fechar o DataReader ou a conexão depois de ler o número de linhas esperado, sem uma chamada adicional final para o método `Read`, o código gerará uma exceção sem-tratamento. Entretanto, se seu código tentar ler dados nessa iteração final através de um loop, quando `Read` ainda retorna `true`, mas a última linha tiver passado, o código gerará uma `ApplicationException` sem-tratamento com a mensagem "O IDataReader SSIS passou do final do conjunto de resultados". Esse comportamento é diferente de outras implementações do DataReader. Entretanto, ao usar um loop para ler as linhas no DataReader enquanto `Read` retorna `true`, você precisa gravar o código para pegar, testar e descartar essa `ApplicationException` antecipada na última chamada bem sucedida do método `Read`. Ou, se você souber antes o número de linhas esperado, você poderá processar as linhas e depois chamar o método `Read` mais uma vez antes de fechar o DataReader e a conexão.  
  
7.  Chame o método `Dispose` do objeto `DtsCommand`. Isso é particularmente importante se você usou qualquer objeto `DtsDataParameter`.  
  
8.  Feche o DataReader e os objetos de conexão.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir executa um pacote que calcula um único valor de agregação, salva esse valor em um destino do DataReader e o lê do DataReader e o exibe em uma caixa de texto em um formulário do Windows.  
  
 O uso de parâmetros não é necessário ao carregar a saída de um pacote em um aplicativo cliente. Se você não quiser usar um parâmetro, você pode omitir o uso da variável na **DtsClient** namespace e omita o código que usa o `DtsDataParameter` objeto.  
  
#### <a name="to-create-the-test-package"></a>Para criar o pacote de teste  
  
1.  Crie um novo pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O código de exemplo usa "DtsClientWParamPkg.dtsx" como o nome do pacote.  
  
2.  Adicione uma variável do tipo Cadeia de caracteres ao namespace DtsClient. O código de exemplo usa País como nome da variável. (Talvez você precise clicar no botão de barra de ferramentas **Escolher Colunas de Variáveis** na janela **Variáveis** para exibir a coluna **Namespace**.)  
  
3.  Adicione um gerenciador de conexões do OLE DB que se conecta ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
4.  Acrescente uma tarefa de fluxo de dados ao pacote e alterne para a superfície de design de Fluxo de Dados.  
  
5.  Adicione uma origem de OLE DB ao fluxo de dados e configure-a para usar o gerenciador de conexões OLE DB criado anteriormente, e o seguinte comando SQL:  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  Clique em `Parameters` e, além de **definir parâmetros de consulta** caixa de diálogo caixa, mapeie o único parâmetro de entrada na consulta, Parameter0, para a variável dtsclient:: Country.  
  
7.  Acrescente uma transformação Agregação ao fluxo de dados e conecte a saída da origem de OLE DB à transformação. Abra o Editor de Transformação Agregação e configure-o para realizar uma operação “Contar todas” em todas as colunas de entrada (*) e gerar o valor agregado com o alias CustomerCount.  
  
8.  Acrescente um destino de DataReader ao fluxo de dados e conecte a saída da transformação Agregação a esse destino. O código de exemplo usa "DataReaderDest" como o nome do DataReader. Selecione a única coluna de entrada disponível, CustomerCount, para o destino.  
  
9. Salve o pacote. O aplicativo de teste criado em seguida executará o pacote e recuperará sua saída diretamente da memória.  
  
#### <a name="to-create-the-test-application"></a>Para criar o aplicativo de teste  
  
1.  Crie um novo aplicativo Windows Forms.  
  
2.  Adicione uma referência para o `Microsoft.SqlServer.Dts.DtsClient` namespace navegando até o assembly do mesmo nome no **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**.  
  
3.  Copie e cole o código de exemplo seguinte no módulo de código para o formulário.  
  
4.  Modificar o valor da `dtexecArgs` variável conforme necessário, de forma que ele contenha os parâmetros de linha de comando necessários **dtexec.exe** para executar o pacote. O código de exemplo carrega o pacote do sistema de arquivos.  
  
5.  Modificar o valor da `dataReaderName` variável conforme necessário, de forma que ele contenha o nome do destino DataReader no pacote.  
  
6.  Coloque um botão e uma caixa de texto no formulário. O código de exemplo usa `btnRun` como o nome do botão, e `txtResults` como o nome da caixa de texto.  
  
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
  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Compreender as diferenças entre execução local e remota](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Carregando e executando um pacote local de forma programática](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Carregar e executar um pacote remoto programaticamente](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  
