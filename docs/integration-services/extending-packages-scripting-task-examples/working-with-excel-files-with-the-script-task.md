---
title: Trabalhando com arquivos do Excel com a tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Excel files
- Script task [Integration Services], examples
- Excel [Integration Services]
ms.assetid: b8fa110a-2c9c-4f5a-8fe1-305555640e44
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b2e826686c4b6fd42d8d5ba7755fa2d4cb8d0f3e
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35331470"
---
# <a name="working-with-excel-files-with-the-script-task"></a>Trabalhando com arquivos do Excel com a tarefa Script
  O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece o gerenciador de conexões do Excel, a origem do Excel e o destino do Excel para trabalhar com dados armazenados em planilhas no formato de arquivo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. As técnicas descritas neste tópico utilizam a tarefa Script para obter informações sobre bancos de dados (arquivos de pasta de trabalho) e tabelas (planilhas e intervalos nomeados) do Excel disponíveis.
  
> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).
 
> [!TIP]  
>  Se desejar criar uma tarefa que possa ser reutilizada em vários pacotes, procure utilizar o código desse exemplo de tarefa Script como o ponto inicial de uma tarefa personalizada. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  

##  <a name="configuring"></a> Configurando um pacote para testar as amostras  
 Você pode configurar um único pacote para testar todos os exemplos neste tópico. Os exemplos usam muitas das mesmas variáveis de pacote e as mesmas classes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
### <a name="to-configure-a-package-for-use-with-the-examples-in-this-topic"></a>Para configurar um pacote para uso com os exemplos neste tópico  
  
1.  Crie um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] novo em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e abra o pacote padrão para editar.  
  
2.  **Variáveis**. Abra a janela **Variáveis** e defina as seguintes variáveis:  
  
    -   `ExcelFile`, do tipo **Cadeia de caracteres**. Digite o caminho completo e o nome do arquivo em uma pasta de trabalho do Excel existente.  
  
    -   `ExcelTable`, do tipo **Cadeia de caracteres**. Digite o nome de uma planilha existente ou intervalo nomeado na pasta de trabalho nomeada no valor da variável `ExcelFile`. Esse valor diferencia maiúsculas de minúsculas.  
  
    -   `ExcelFileExists`, do tipo **Booliano**.  
  
    -   `ExcelTableExists`, do tipo **Booliano**.  
  
    -   `ExcelFolder`, do tipo **Cadeia de caracteres**. Digite o caminho completo de uma pasta que contenha pelo menos uma pasta de trabalho do Excel.  
  
    -   `ExcelFiles`, do tipo **Objeto**.  
  
    -   `ExcelTables`, do tipo **Objeto**.  
  
3.  **Instruções Imports**. A maioria dos exemplos de código requer que você importe um ou ambos namespaces [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] seguintes no topo de seu arquivo de script:  
  
    -   **System.IO**, para operações do sistema de arquivos.  
  
    -   **System.Data.OleDb**, para abrir arquivos do Excel como fontes de dados.  
  
4.  **Referências**. Os exemplos de código que leem informações de esquema de arquivos do Excel exigem uma referência adicional no projeto de script ao namespace **System.Xml**.  
  
5.  Defina a linguagem de scripts padrão para o componente Script usando a opção **Linguagem de scripts** na página **Geral** da caixa de diálogo **Opções**. Para obter mais informações, consulte [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx).  
  
##  <a name="example1"></a> Descrição do exemplo 1: verificar se existe um arquivo do Excel  
 Esse exemplo determina se o arquivo da pasta de trabalho do Excel especificado na variável `ExcelFile` existe, e define o valor booliano da variável `ExcelFileExists` para o resultado. Você pode usar esse valor booliano para ramificar no fluxo de trabalho do pacote.  
  
### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
1.  Adicione uma nova tarefa Script ao pacote e altere seu nome para **ExcelFileExists**.  
  
2.  No **Editor da Tarefa Script**, na guia **Script**, clique em **ReadOnlyVariables** e insira o valor da propriedade usando um dos seguintes métodos:  
  
    -   Digite **ExcelFile**.  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione a variável **ExcelFile**.  
  
3.  Clique em **ReadWriteVariables** e insira o valor da propriedade usando um dos seguintes métodos:  
  
    -   Digite **ExcelFileExists**.  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione a variável **ExcelFileExists**.  
  
4.  Clique em **Editar Script** para abrir o editor de scripts.  
  
5.  Adicione uma instrução **Imports** ao namespace **System.IO** na parte superior do arquivo de script.  
  
6.  Adicione o código seguinte:  
  
### <a name="example-1-code"></a>Código do exemplo 1  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    If File.Exists(fileToTest) Then  
      Dts.Variables("ExcelFileExists").Value = True  
    Else  
      Dts.Variables("ExcelFileExists").Value = False  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    string fileToTest;  
  
    fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
    if (File.Exists(fileToTest))  
    {  
      Dts.Variables["ExcelFileExists"].Value = true;  
    }  
    else  
    {  
      Dts.Variables["ExcelFileExists"].Value = false;  
    }  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
##  <a name="example2"></a> Descrição do exemplo 2: verificar se existe uma tabela do Excel  
 Esse exemplo determina se a planilha ou intervalo nomeado do Excel especificado na variável `ExcelTable` existe no arquivo da pasta de trabalho do Excel especificado na variável `ExcelFile`, e define o valor booliano da variável `ExcelTableExists` para o resultado. Você pode usar esse valor booliano para ramificar no fluxo de trabalho do pacote.  
  
### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
1.  Adicione uma nova tarefa Script ao pacote e altere seu nome para **ExcelTableExists**.  
  
2.  No **Editor da Tarefa Script**, na guia **Script**, clique em **ReadOnlyVariables** e insira o valor da propriedade usando um dos seguintes métodos:  
  
    -   Digite **ExcelTable** e **ExcelFile** separados por vírgula **.**  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione as variáveis **ExcelTable** e **ExcelFile**.  
  
3.  Clique em **ReadWriteVariables** e insira o valor da propriedade usando um dos seguintes métodos:  
  
    -   Digite **ExcelTableExists**.  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione a variável **ExcelTableExists**.  
  
4.  Clique em **Editar Script** para abrir o editor de scripts.  
  
5.  Adicione uma referência ao assembly **System.Xml** no projeto de script.  
  
6.  Adicione instruções **Imports** aos namespaces **System.IO** e **System.Data.OleDb** na parte superior do arquivo de script.  
  
7.  Adicione o código seguinte:  
  
### <a name="example-2-code"></a>Código do exemplo 2  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
    Dim tableToTest As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim excelTables As DataTable  
    Dim excelTable As DataRow  
    Dim currentTable As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    tableToTest = Dts.Variables("ExcelTable").Value.ToString  
  
    Dts.Variables("ExcelTableExists").Value = False  
    If File.Exists(fileToTest) Then  
      connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" & _  
        "Data Source=" & fileToTest & _  
        ";Extended Properties=Excel 12.0"  
      excelConnection = New OleDbConnection(connectionString)  
      excelConnection.Open()  
      excelTables = excelConnection.GetSchema("Tables")  
      For Each excelTable In excelTables.Rows  
        currentTable = excelTable.Item("TABLE_NAME").ToString  
        If currentTable = tableToTest Then  
          Dts.Variables("ExcelTableExists").Value = True  
        End If  
      Next  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
    public void Main()  
        {  
            string fileToTest;  
            string tableToTest;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable excelTables;  
            string currentTable;  
  
            fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
            tableToTest = Dts.Variables["ExcelTable"].Value.ToString();  
  
            Dts.Variables["ExcelTableExists"].Value = false;  
            if (File.Exists(fileToTest))  
            {  
                connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" +  
                "Data Source=" + fileToTest + ";Extended Properties=Excel 12.0";  
                excelConnection = new OleDbConnection(connectionString);  
                excelConnection.Open();  
                excelTables = excelConnection.GetSchema("Tables");  
                foreach (DataRow excelTable in excelTables.Rows)  
                {  
                    currentTable = excelTable["TABLE_NAME"].ToString();  
                    if (currentTable == tableToTest)  
                    {  
                        Dts.Variables["ExcelTableExists"].Value = true;  
                    }  
                }  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
}  
```  
  
##  <a name="example3"></a> Descrição do exemplo 3: obter uma lista de arquivos do Excel em uma pasta  
 Esse exemplo preenche uma matriz com a lista de arquivos do Excel encontrada na pasta especificada no valor da variável `ExcelFolder`, e copia a matriz para a variável `ExcelFiles`. Você pode usar o Enumerador Foreach de Variável para repetir nos arquivos da matriz.  
  
### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
1.  Adicione uma nova tarefa Script ao pacote e altere seu nome para **GetExcelFiles**.  
  
2.  Abra o **Editor da Tarefa Script**, na guia **Script**, clique em **ReadOnlyVariables** e insira o valor da propriedade usando um dos seguintes métodos:  
  
    -   Digite **ExcelFolder**  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione a variável ExcelFolder.  
  
3.  Clique em **ReadWriteVariables** e insira o valor da propriedade usando um dos seguintes métodos:  
  
    -   Digite **ExcelFiles**.  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione a variável ExcelFiles.  
  
4.  Clique em **Editar Script** para abrir o editor de scripts.  
  
5.  Adicione uma instrução **Imports** ao namespace **System.IO** na parte superior do arquivo de script.  
  
6.  Adicione o código seguinte:  
  
### <a name="example-3-code"></a>Código do exemplo 3  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const FILE_PATTERN As String = "*.xlsx"  
  
    Dim excelFolder As String  
    Dim excelFiles As String()  
  
    excelFolder = Dts.Variables("ExcelFolder").Value.ToString  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN)  
  
    Dts.Variables("ExcelFiles").Value = excelFiles  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    const string FILE_PATTERN = "*.xlsx";  
  
    string excelFolder;  
    string[] excelFiles;  
  
    excelFolder = Dts.Variables["ExcelFolder"].Value.ToString();  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN);  
  
    Dts.Variables["ExcelFiles"].Value = excelFiles;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
### <a name="alternate-solution"></a>Solução alternada  
 Em vez de usar uma tarefa Script para reunir uma lista de arquivos do Excel em uma matriz, você também pode usar o Enumerador de Arquivo Foreach para repetir em todos os arquivos do Excel em uma pasta. Para obter mais informações, consulte [Executar um loop por meio de arquivos e tabelas do Excel usando um contêiner do Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
##  <a name="example4"></a> Descrição do exemplo 4: obter uma lista de tabelas em um arquivo do Excel  
 Esse exemplo preenche uma matriz com a lista de planilhas e intervalos nomeados encontrados no arquivo da pasta de trabalho especificado pelo valor da variável `ExcelFile`, e copia a matriz para a variável `ExcelTables`. Você pode usar o Enumerador Foreach de Variável para repetir nas tabelas da matriz.  
  
> [!NOTE]  
>  A lista de tabelas em uma pasta de trabalho do Excel inclui planilhas (que têm o sufixo $) e intervalos nomeados. Se você tiver que filtrar a lista para apenas planilhas ou apenas intervalos nomeados, talvez seja necessário acrescentar um código adicional para esse propósito.  
  
### <a name="to-configure-this-script-task-example"></a>Para configurar esse exemplo de tarefa Script  
  
1.  Adicione uma nova tarefa Script ao pacote e altere seu nome para **GetExcelTables**.  
  
2.  Abra o **Editor da Tarefa Script**, na guia **Script**, clique em **ReadOnlyVariables** e insira o valor da propriedade usando um dos seguintes métodos:  
  
    -   Digite **ExcelFile**.  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione a variável ExcelFile.  
  
3.  Clique em **ReadWriteVariables** e insira o valor da propriedade usando um dos seguintes métodos:  
  
    -   Digite **ExcelTables**.  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione a variável ExcelTables.  
  
4.  Clique em **Editar Script** para abrir o editor de scripts.  
  
5.  Adicione uma referência ao namespace **System.Xml** no projeto de script.  
  
6.  Adicione uma instrução **Imports** ao namespace **System.Data.OleDb** na parte superior do arquivo de script.  
  
7.  Adicione o código seguinte:  
  
### <a name="example-4-code"></a>Exemplo 4 Código  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim excelFile As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim tablesInFile As DataTable  
    Dim tableCount As Integer = 0  
    Dim tableInFile As DataRow  
    Dim currentTable As String  
    Dim tableIndex As Integer = 0  
  
    Dim excelTables As String()  
  
    excelFile = Dts.Variables("ExcelFile").Value.ToString  
    connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" & _  
        "Data Source=" & excelFile & _  
        ";Extended Properties=Excel 12.0"  
    excelConnection = New OleDbConnection(connectionString)  
    excelConnection.Open()  
    tablesInFile = excelConnection.GetSchema("Tables")  
    tableCount = tablesInFile.Rows.Count  
    ReDim excelTables(tableCount - 1)  
    For Each tableInFile In tablesInFile.Rows  
      currentTable = tableInFile.Item("TABLE_NAME").ToString  
      excelTables(tableIndex) = currentTable  
      tableIndex += 1  
    Next  
  
    Dts.Variables("ExcelTables").Value = excelTables  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            string excelFile;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable tablesInFile;  
            int tableCount = 0;  
            string currentTable;  
            int tableIndex = 0;  
  
            string[] excelTables = new string[5];  
  
            excelFile = Dts.Variables["ExcelFile"].Value.ToString();  
            connectionString = "Provider=Microsoft.ACE.OLEDB.12.0;" +  
                "Data Source=" + excelFile + ";Extended Properties=Excel 12.0";  
            excelConnection = new OleDbConnection(connectionString);  
            excelConnection.Open();  
            tablesInFile = excelConnection.GetSchema("Tables");  
            tableCount = tablesInFile.Rows.Count;  
  
            foreach (DataRow tableInFile in tablesInFile.Rows)  
            {  
                currentTable = tableInFile["TABLE_NAME"].ToString();  
                excelTables[tableIndex] = currentTable;  
                tableIndex += 1;  
            }  
  
            Dts.Variables["ExcelTables"].Value = excelTables;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
### <a name="alternate-solution"></a>Solução alternada  
 Em vez de usar uma tarefa Script para reunir uma lista de tabelas do Excel em uma matriz, você também pode usar o Enumerador de Conjunto de Linhas de Esquema ADO.NET Foreach para repetir em todos as tabelas (planinhas e intervalos nomeados) em um arquivo de pasta de trabalho do Excel. Para obter mais informações, consulte [Executar um loop por meio de arquivos e tabelas do Excel usando um contêiner do Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
##  <a name="testing"></a> Exibindo os resultados das amostras  
 Se você configurou cada um dos exemplos deste tópico no mesmo pacote, você pode conectar todas as tarefas Script a uma tarefa Script adicional que exibe a saída de todos os exemplos.  
  
### <a name="to-configure-a-script-task-to-display-the-output-of-the-examples-in-this-topic"></a>Para configurar uma tarefa Script para exibir a saída dos exemplos neste tópico  
  
1.  Adicione uma nova tarefa Script ao pacote e altere seu nome para **DisplayResults**.  
  
2.  Conecte cada uma das quatro tarefas Script de exemplo uma a outra, de forma que cada tarefa seja executada depois que a anterior for concluída com êxito e conecte a quarta tarefa de exemplo à tarefa **DisplayResults**.  
  
3.  Abra a tarefa **DisplayResults** no **Editor da Tarefa Script**.  
  
4.  Na guia **Script**, clique em **ReadOnlyVariables** e use um dos seguintes métodos para adicionar todas as sete variáveis listadas em [Configurando um pacote para testar as amostras](#configuring):  
  
    -   Digite o nome de cada variável separado por vírgulas.  
  
         -ou-  
  
    -   Clique no botão de reticências (**…**) ao lado do campo de propriedade e, na caixa de diálogo **Selecionar variáveis**, selecione as variáveis.  
  
5.  Clique em **Editar Script** para abrir o editor de scripts.  
  
6.  Adicione instruções **Imports** aos namespaces **Microsoft.VisualBasic** e **System.Windows.Forms** na parte superior do arquivo de script.  
  
7.  Adicione o código seguinte:  
  
8.  Execute o pacote e examine os resultados exibidos em uma caixa de mensagem.  
  
### <a name="code-to-display-the-results"></a>Codifique para exibir o resultados  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const EOL As String = ControlChars.CrLf  
  
    Dim results As String  
    Dim filesInFolder As String()  
    Dim fileInFolder As String  
    Dim tablesInFile As String()  
    Dim tableInFile As String  
  
    results = _  
      "Final values of variables:" & EOL & _  
      "ExcelFile: " & Dts.Variables("ExcelFile").Value.ToString & EOL & _  
      "ExcelFileExists: " & Dts.Variables("ExcelFileExists").Value.ToString & EOL & _  
      "ExcelTable: " & Dts.Variables("ExcelTable").Value.ToString & EOL & _  
      "ExcelTableExists: " & Dts.Variables("ExcelTableExists").Value.ToString & EOL & _  
      "ExcelFolder: " & Dts.Variables("ExcelFolder").Value.ToString & EOL & _  
      EOL  
  
    results &= "Excel files in folder: " & EOL  
    filesInFolder = DirectCast(Dts.Variables("ExcelFiles").Value, String())  
    For Each fileInFolder In filesInFolder  
      results &= " " & fileInFolder & EOL  
    Next  
    results &= EOL  
  
    results &= "Excel tables in file: " & EOL  
    tablesInFile = DirectCast(Dts.Variables("ExcelTables").Value, String())  
    For Each tableInFile In tablesInFile  
      results &= " " & tableInFile & EOL  
    Next  
  
    MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information)  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            const string EOL = "\r";  
  
            string results;  
            string[] filesInFolder;  
            //string fileInFolder;  
            string[] tablesInFile;  
            //string tableInFile;  
  
            results = "Final values of variables:" + EOL + "ExcelFile: " + Dts.Variables["ExcelFile"].Value.ToString() + EOL + "ExcelFileExists: " + Dts.Variables["ExcelFileExists"].Value.ToString() + EOL + "ExcelTable: " + Dts.Variables["ExcelTable"].Value.ToString() + EOL + "ExcelTableExists: " + Dts.Variables["ExcelTableExists"].Value.ToString() + EOL + "ExcelFolder: " + Dts.Variables["ExcelFolder"].Value.ToString() + EOL + EOL;  
  
            results += "Excel files in folder: " + EOL;  
            filesInFolder = (string[])(Dts.Variables["ExcelFiles"].Value);  
            foreach (string fileInFolder in filesInFolder)  
            {  
                results += " " + fileInFolder + EOL;  
            }  
            results += EOL;  
  
            results += "Excel tables in file: " + EOL;  
            tablesInFile = (string[])(Dts.Variables["ExcelTables"].Value);  
            foreach (string tableInFile in tablesInFile)  
            {  
                results += " " + tableInFile + EOL;  
            }  
  
            MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)  
 [Loop através de arquivos e tabelas do Excel por meio de um contêiner do Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
