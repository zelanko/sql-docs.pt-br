---
title: Analisar formatos de arquivo de texto não padrão com o componente Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- text file reading [Integration Services]
- Script component [Integration Services], non-standard text file formats
- transformations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: 1fda034d-09e4-4647-9a9f-e8d508c2cc8f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc8ac157a3bdfa240414fe4055cc322370bac019
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85427083"
---
# <a name="parsing-non-standard-text-file-formats-with-the-script-component"></a>Analisando formatos de arquivo de texto fora do padrão com o componente Script
  Quando seus dados de origem estiverem dispostos em um formato não padrão, talvez seja mais conveniente consolidar toda a sua lógica de análise em um único script do que reunir várias transformações [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para chegar ao mesmo resultado.  
  
 [Exemplo 1: analisar registros delimitados por linha](#example1)  
  
 [Exemplo 2: dividir registros pai e filho](#example2)  
  
> [!NOTE]  
>  Se desejar criar um componente que possa ser reutilizado mais facilmente em várias tarefas de fluxo de dados e em vários pacotes, procure utilizar o código deste exemplo de componente Script como o ponto inicial de um componente de fluxo de dados personalizado. Para obter mais informações, consulte [Desenvolvendo um componente de fluxo de dados personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
##  <a name="example-1-parsing-row-delimited-records"></a><a name="example1"></a> Exemplo 1: analisar registros delimitados por linha  
 Este exemplo mostra como utilizar um arquivo de texto em que cada coluna de dados aparece em uma linha separada e analisá-lo em uma tabela de destino usando o componente Script.  
  
 Para obter mais informações sobre como configurar o componente Script para uso como uma transformação no fluxo de dados, consulte [criando uma transformação síncrona com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)e [criando uma transformação assíncrona com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar esse exemplo de componente Script  
  
1.  Crie e salve um arquivo de texto nomeado **rowdelimiteddata.txt** contendo os seguintes dados de origem:  
  
    ```  
    FirstName: Nancy  
    LastName: Davolio  
    Title: Sales Representative  
    City: Seattle  
    StateProvince: WA  
  
    FirstName: Andrew  
    LastName: Fuller  
    Title: Vice President, Sales  
    City: Tacoma  
    StateProvince: WA  
  
    FirstName: Steven  
    LastName: Buchanan  
    Title: Sales Manager  
    City: London  
    StateProvince:  
  
    ```  
  
2.  Abra o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Selecione um banco de dados de destino e abra uma nova janela de consulta. Na janela de consulta, execute o seguinte script para criar a tabela de destino:  
  
    ```  
    create table RowDelimitedData  
    (  
    FirstName varchar(32),  
    LastName varchar(32),  
    Title varchar(32),  
    City varchar(32),  
    StateProvince varchar(32)  
    )  
  
    ```  
  
4.  Abra o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] e crie um novo pacote de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nomeado ParseRowDelim.dtsx.  
  
5.  Adicione um gerenciador de conexões de arquivos simples ao pacote, nomeie-o como RowDelimitedData e configure-o para conectá-lo ao arquivo rowdelimiteddata.txt criado em uma etapa anterior.  
  
6.  Adicione um gerenciador de conexões OLE DB ao pacote e configure-o para conectá-lo à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao banco de dados em que você criou a tabela de destino.  
  
7.  Adicione uma tarefa de Fluxo de Dados ao pacote e clique na guia **Fluxo de Dados** do Designer SSIS.  
  
8.  Adicione uma Fonte de Arquivo Simples ao fluxo de dados e configure-a para usar o gerenciador de conexões do RowDelimitedData. Na página **Colunas** do **Editor de Fonte de Arquivo Simples**, selecione a única coluna externa disponível.  
  
9. Adicione um Componente Script ao fluxo de dados e configure-o como uma transformação. Conecte a saída da Fonte de Arquivo Simples ao Componente Script.  
  
10. Clique duas vezes no componente Script para exibir o **Editor de Transformação Scripts**.  
  
11. Na página **Colunas de Entrada** do **Editor de Transformação Scripts**, selecione a única coluna de entrada disponível.  
  
12. Na página **entradas e saídas** do editor de **transformação scripts**, selecione saída 0 e defina `SynchronousInputID` como nenhum. Crie 5 colunas de saída, todas com tipo cadeia de caracteres [DT_STR] com comprimento 32:  
  
    -   Nome  
  
    -   LastName  
  
    -   Title  
  
    -   City  
  
    -   StateProvince  
  
13. Na página **script** do editor de **transformação scripts**, clique em **Editar script** e insira o código mostrado na `ScriptMain` classe do exemplo. Feche o ambiente de desenvolvimento de scripts e o **Editor de Transformação Scripts**.  
  
14. Adicione um Destino de SQL Server ao fluxo de dados. Configure-o para usar o gerenciador de conexões do OLE DB e a tabela RowDelimitedData. Conecte a saída do Componente Script a este destino.  
  
15. Execute o pacote. Depois da conclusão do pacote, examine os registros na tabela de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Dim columnName As String  
    Dim columnValue As String  
  
    ' Check for an empty row.  
    If Row.Column0.Trim.Length > 0 Then  
        columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"))  
        ' Check for an empty value after the colon.  
        If Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd.Length > 1 Then  
            ' Extract the column value from after the colon and space.  
            columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2)  
            Select Case columnName  
                Case "FirstName"  
                    ' The FirstName value indicates a new record.  
                    Me.Output0Buffer.AddRow()  
                    Me.Output0Buffer.FirstName = columnValue  
                Case "LastName"  
                    Me.Output0Buffer.LastName = columnValue  
                Case "Title"  
                    Me.Output0Buffer.Title = columnValue  
                Case "City"  
                    Me.Output0Buffer.City = columnValue  
                Case "StateProvince"  
                    Me.Output0Buffer.StateProvince = columnValue  
            End Select  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
        string columnName;  
        string columnValue;  
  
        // Check for an empty row.  
        if (Row.Column0.Trim().Length > 0)  
        {  
            columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"));  
            // Check for an empty value after the colon.  
            if (Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd().Length > 1)  
            // Extract the column value from after the colon and space.  
            {  
                columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2);  
                switch (columnName)  
                {  
                    case "FirstName":  
                        // The FirstName value indicates a new record.  
                        this.Output0Buffer.AddRow();  
                        this.Output0Buffer.FirstName = columnValue;  
                        break;  
                    case "LastName":  
                        this.Output0Buffer.LastName = columnValue;  
                        break;  
                    case "Title":  
                        this.Output0Buffer.Title = columnValue;  
                        break;  
                    case "City":  
                        this.Output0Buffer.City = columnValue;  
                        break;  
                    case "StateProvince":  
                        this.Output0Buffer.StateProvince = columnValue;  
                        break;  
                }  
            }  
        }  
  
    }  
```  
  
##  <a name="example-2-splitting-parent-and-child-records"></a><a name="example2"></a> Exemplo 2: dividir registros pai e filho  
 Este exemplo mostra como utilizar um arquivo de texto, em que uma linha delimitadora precede uma linha de registro pai, que é seguida de um número indefinido de linhas de registro filho, e analisa-as em tabelas de destino pai e filho, adequadamente normalizadas, através do componente Script. Esse exemplo simples pode ser facilmente adaptado para arquivos de origem que utilizam mais de uma linha ou coluna para cada registro pai e filho, desde que exista uma forma de identificar o início e o fim de cada registro.  
  
> [!CAUTION]  
>  Esse exemplo é utilizado apenas para fins de demonstração. Se você executar o exemplo mais de uma vez, ele inserirá valores de chave duplicados na tabela de destino.  
  
 Para obter mais informações sobre como configurar o componente Script para uso como uma transformação no fluxo de dados, consulte [criando uma transformação síncrona com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)e [criando uma transformação assíncrona com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar esse exemplo de componente Script  
  
1.  Crie e salve um arquivo de texto nomeado **parentchilddata.txt** contendo os seguintes dados de origem:  
  
    ```  
    **********  
    PARENT 1 DATA  
    child 1 data  
    child 2 data  
    child 3 data  
    child 4 data  
    **********  
    PARENT 2 DATA  
    child 5 data  
    child 6 data  
    child 7 data  
    child 8 data  
    **********  
  
    ```  
  
2.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Selecione um banco de dados de destino e abra uma nova janela de consulta. Na janela de consulta, execute o seguinte script para criar as tabelas de destino:  
  
    ```  
    CREATE TABLE [dbo].[Parents]([ParentID] [int] NOT NULL,  
    [ParentRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Parents] PRIMARY KEY CLUSTERED   
    ([ParentID] ASC))  
    GO  
    CREATE TABLE [dbo].[Children]([ChildID] [int] NOT NULL,  
    [ParentID] [int] NOT NULL,  
    [ChildRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Children] PRIMARY KEY CLUSTERED   
    ([ChildID] ASC))  
    GO  
    ALTER TABLE [dbo].[Children] ADD CONSTRAINT [FK_Children_Parents] FOREIGN KEY([ParentID])  
    REFERENCES [dbo].[Parents] ([ParentID])  
  
    ```  
  
4.  Abra o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e crie um novo pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nomeado SplitParentChild.dtsx.  
  
5.  Adicione um gerenciador de conexões de arquivos simples ao pacote, nomeie-o como ParentChildData e configure-o para conectá-lo ao arquivo parentchilddata.txt criado em uma etapa anterior.  
  
6.  Adicione um gerenciador de conexões OLE DB ao pacote e configure-o para conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ao banco de dados em que você criou as tabelas de destino.  
  
7.  Adicione uma tarefa de Fluxo de Dados ao pacote e clique na guia **Fluxo de Dados** do Designer SSIS.  
  
8.  Adicione uma Fonte de Arquivo Simples ao fluxo de dados e configure-a para usar o gerenciador de conexões do ParentChildData. Na página **Colunas** do **Editor de Fonte de Arquivo Simples**, selecione a única coluna externa disponível.  
  
9. Adicione um Componente Script ao fluxo de dados e configure-o como uma transformação. Conecte a saída da Fonte de Arquivo Simples ao Componente Script.  
  
10. Clique duas vezes no componente Script para exibir o **Editor de Transformação Scripts**.  
  
11. Na página **Colunas de Entrada** do **Editor de Transformação Scripts**, selecione a única coluna de entrada disponível.  
  
12. Na página **entradas e saídas** do editor de **transformação scripts**, selecione saída 0, renomeie para ParentRecords e defina seu `SynchronousInputID` como nenhum. Crie 2 colunas de saída:  
  
    -   ParentID (a chave primária), de tipo inteiro assinado de quatro bytes [DT_I4]  
  
    -   ParentRecord, de cadeia de caracteres de tipo [DT_STR] com comprimento de 32.  
  
13. Crie uma segunda saída e nomeie-a como ChildRecords. O `SynchronousInputID` da nova saída já está definido como Nenhum. Crie 3 colunas de saída:  
  
    -   ChildID (a chave primária), de tipo inteiro assinado de quatro bytes [DT_I4]  
  
    -   ParentID (a chave estrangeira), também de tipo inteiro assinado de quatro bytes [DT_I4]  
  
    -   ChildRecord, de cadeia de caracteres de tipo [DT_STR] com comprimento de 50  
  
14. Na página **Script** do **Editor de Transformação Scripts**, clique em **Editar Script**. Na classe `ScriptMain`, digite o código mostrado no exemplo. Feche o ambiente de desenvolvimento de scripts e o **Editor de Transformação Scripts**.  
  
15. Adicione um Destino de SQL Server ao fluxo de dados. Conecte a saída de ParentRecords do Componente Script a esse destino. Configure-o para usar o gerenciador de conexões OLE DB e a tabela Pais.  
  
16. Adicione outro Destino de SQL Server ao fluxo de dados. Conecte a saída ChildRecords do Componente Script a esse destino. Configure-o para usar o gerenciador de conexões OLE DB e a tabela Filhos.  
  
17. Execute o pacote. Depois da conclusão do pacote, examine os registros pai e filho nas duas tabelas de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Static nextRowIsParent As Boolean = False  
    Static parentCounter As Integer = 0  
    Static childCounter As Integer = 0  
  
    ' If current row starts with separator characters,  
    '  then following row contains new parent record.  
    If Row.Column0.StartsWith("***") Then  
        nextRowIsParent = True  
    Else  
        If nextRowIsParent Then  
            ' Current row contains parent record.  
            parentCounter += 1  
            Me.ParentRecordsBuffer.AddRow()  
            Me.ParentRecordsBuffer.ParentID = parentCounter  
            Me.ParentRecordsBuffer.ParentRecord = Row.Column0  
            nextRowIsParent = False  
        Else  
            ' Current row contains child record.  
            childCounter += 1  
            Me.ChildRecordsBuffer.AddRow()  
            Me.ChildRecordsBuffer.ChildID = childCounter  
            Me.ChildRecordsBuffer.ParentID = parentCounter  
            Me.ChildRecordsBuffer.ChildRecord = Row.Column0  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
    int static_Input0_ProcessInputRow_childCounter = 0;  
    int static_Input0_ProcessInputRow_parentCounter = 0;  
    bool static_Input0_ProcessInputRow_nextRowIsParent = false;  
  
        // If current row starts with separator characters,   
        // then following row contains new parent record.   
        if (Row.Column0.StartsWith("***"))  
        {  
            static_Input0_ProcessInputRow_nextRowIsParent = true;  
        }  
        else  
        {  
            if (static_Input0_ProcessInputRow_nextRowIsParent)  
            {  
                // Current row contains parent record.   
                static_Input0_ProcessInputRow_parentCounter += 1;  
                this.ParentRecordsBuffer.AddRow();  
                this.ParentRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ParentRecordsBuffer.ParentRecord = Row.Column0;  
                static_Input0_ProcessInputRow_nextRowIsParent = false;  
            }  
            else  
            {  
                // Current row contains child record.   
                static_Input0_ProcessInputRow_childCounter += 1;  
                this.ChildRecordsBuffer.AddRow();  
                this.ChildRecordsBuffer.ChildID = static_Input0_ProcessInputRow_childCounter;  
                this.ChildRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ChildRecordsBuffer.ChildRecord = Row.Column0;  
            }  
        }  
  
    }  
```  
  
![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando uma transformação síncrona com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 [Criando uma transformação assíncrona com o componente Script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
  
  
