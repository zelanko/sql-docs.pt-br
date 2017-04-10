---
title: "Loop atrav&#233;s de arquivos e tabelas do Excel por meio de um cont&#234;iner Loop Foreach | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "conexões [Integration Services], Excel"
  - "Excel [Integration Services]"
  - "gerenciadores de conexões [Integration Services], Excel"
ms.assetid: a5393c1a-cc37-491a-a260-7aad84dbff68
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Loop atrav&#233;s de arquivos e tabelas do Excel por meio de um cont&#234;iner Loop Foreach
  Os procedimentos neste tópico descrevem como criar um loop através de pastas de trabalho do Excel ou através de tabelas em uma pasta de trabalho do Excel, usando o contêiner Loop Foreach com o enumerador apropriado.  
  
### Para criar um loop através de arquivos do Excel usando o enumerador de Arquivo Foreach  
  
1.  Crie uma variável de cadeia que receberá o caminho atual do Excel e nome de arquivo em cada iteração do loop. Para evitar problemas de validação, atribua um caminho de Excel válido e um nome de arquivo como o valor inicial da variável. (A expressão de amostra exibida mais adiante neste procedimento usa o nome da variável, `ExcelFile`.)  
  
2.  Como alternativa, crie outra variável de cadeia que irá conter o valor do argumento Propriedades Estendidas da cadeia de conexão do Excel. Este argumento contém uma série de valores que especificam a versão do Excel, determinam se a primeira linha contém nomes de coluna e se o modo de importação é usado. (A expressão de amostra exibida mais adiante neste procedimento usa o nome de variável `ExtProperties`, com um valor inicial de “`Excel 8.0;HDR=Yes`”.)  
  
     Se você não usar uma variável para o argumento Propriedades Estendidas, adicione-a manualmente à expressão que contém a cadeia de conexão.  
  
3.  Adicione um contêiner Loop Foreach à guia **Fluxo de Controle**. Para obter informações sobre como configurar um Contêiner Loop Foreach, consulte [Para configurar um contêiner Loop Foreach](../Topic/Configure%20a%20Foreach%20Loop%20Container.md).  
  
4.  Na página **Coleção** do **Editor de Loop Foreach**, selecione o enumerador de Arquivo Foreach, especifique a pasta na qual as pastas de trabalho do Excel ficam situadas e especifique o filtro de arquivo (geralmente *.xls).  
  
5.  Na página **Mapeamento de Variáveis**, mapeie Index 0 para uma variável de cadeia definida pelo usuário que receberá o caminho atual do Excel e o nome de arquivo em cada iteração do loop. (A expressão de amostra exibida mais adiante neste procedimento usa o nome da variável `ExcelFile`.)  
  
6.  Feche o **Editor de Loop Foreach**.  
  
7.  Adicione um gerenciador de conexões do Excel para o pacote conforme descrito em [Adicionar, excluir ou compartilhar um Gerenciador de Conexões em um pacote](../Topic/Add,%20Delete,%20or%20Share%20a%20Connection%20Manager%20in%20a%20Package.md). Selecione uma pasta de trabalho existente do Excel para a conexão para evitar erros de validação.  
  
    > [!IMPORTANT]  
    >  Para evitar erros de validação conforme você configura tarefas e componentes de fluxo de dados que usam esse gerenciador de conexões do Excel, selecione uma pasta de trabalho existente do Excel no **Editor do Gerenciador de Conexões do Excel**. O gerenciador de conexões não usará esta pasta de trabalho em tempo de execução depois que você configurar uma expressão para a propriedade **ConnectionString** conforme descrito nas etapas a seguir. Após criar e configurar o pacote, você pode limpar o valor da propriedade **ConnectionString** na janela Propriedades. No entanto, se você limpar esse valor, a propriedade da cadeia de conexão do gerenciador de conexões do Excel não será mais válida até que Loop Foreach seja executado. Portanto você deve definir a propriedade **DelayValidation** como **True** nas tarefas ou no pacote em que o gerenciador de conexões é usado para evitar erros de validação.  
    >   
    >  Você também deve usar o valor padrão de **False** para a propriedade **RetainSameConnection** do gerenciador de conexões do Excel. Se você alterar esse valor para **True**, cada iteração do loop continuará a abrir a primeira pasta de trabalho do Excel.  
  
8.  Selecione o novo gerenciador de conexões do Excel, clique na propriedade **Expressões** na janela Propriedades e clique nas reticências.  
  
9. No **Editor de Expressões de Propriedades**, selecione a propriedade **ConnectionString** e depois clique no botão de reticências.  
  
10. No Construtor de Expressões, digite a expressão a seguir:  
  
    ```  
    "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=\"" + @[User::ExtProperties] + "\""  
    ```  
  
     Observe o uso do caractere de escape "\\" para não ter que usar as aspas exigidas no valor do argumento Propriedades Estendidas.  
  
     O argumento Propriedades Estendidas não é opcional. Se você não usar uma variável para conter seu valor, adicione-a manualmente à expressão, como neste exemplo de um arquivo do Excel 2003:  
  
    ```  
    "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=Excel 8.0"  
    ```  
  
11. Crie tarefas no contêiner Loop Foreach que usam o gerenciador de conexões do Excel para executar as mesmas operações em cada pasta de trabalho do Excel que corresponde ao local e padrão de arquivo especificado.  
  
### Para criar um loop através de tabelas do Excel usando o enumerador de Conjunto de Linhas de Esquema ADO.NET Foreach  
  
1.  Crie um gerenciador de conexões ADO.NET que use o provedor OLE DB do Microsoft Jet para se conectar a uma pasta de trabalho do Excel. Na página Tudo da caixa de diálogo **Gerenciador de Conexões**, insira o Excel 8.0 como o valor da propriedade Propriedades Estendidas. Para obter mais informações, consulte [Add, Delete, or Share a Connection Manager in a Package](../Topic/Add,%20Delete,%20or%20Share%20a%20Connection%20Manager%20in%20a%20Package.md).  
  
2.  Crie uma variável de cadeia que receberá o nome da tabela atual em cada iteração do loop.  
  
3.  Adicione um contêiner Loop Foreach à guia **Fluxo de Controle**. Para obter informações sobre como configurar um contêiner Loop Foreach, consulte [Para configurar um contêiner Loop Foreach](../Topic/Configure%20a%20Foreach%20Loop%20Container.md).  
  
4.  Na página **Coleção** do **Editor de Loop Foreach**, selecione o Enumerador de Conjunto de Linhas de Esquema ADO.NET Foreach.  
  
5.  Como valor de **Conexão**, selecione o gerenciador de conexões ADO.NET que você criou anteriormente.  
  
6.  Como valor de **Esquema**, selecione Tabelas.  
  
    > [!NOTE]  
    >  A lista de tabelas em uma pasta de trabalho do Excel inclui planilhas (que têm o sufixo $) e intervalos nomeados. Se você tiver que filtrar a lista para apenas planilhas ou apenas intervalos nomeados, talvez seja necessário gravar o código personalizado em uma tarefa Script para essa finalidade. Para obter mais informações, consulte [Trabalhando com arquivos do Excel com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md).  
  
7.  Na página **Mapeamentos de Variáveis**, mapeie Index 2 para a variável de cadeia criada anteriormente para manter o nome da tabela atual.  
  
8.  Feche o **Editor de Loop Foreach**.  
  
9. Crie tarefas no contêiner Loop Foreach que usam o gerenciador de conexões do Excel para executar as mesmas operações em cada tabela do Excel na pasta de trabalho especificada. Se você usar uma tarefa Script para examinar o nome de tabela enumerado ou para trabalhar com tabelas individualmente, lembre-se de adicionar a variável de cadeia à propriedade ReadOnlyVariables da tarefa Script.  
  
## Consulte também  
 [Configurar um contêiner Loop Foreach](../Topic/Configure%20a%20Foreach%20Loop%20Container.md)   
 [Adicionar ou alterar uma expressão de propriedade](../../integration-services/expressions/add-or-change-a-property-expression.md)   
 [Gerenciador de conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Origem do Excel](../../integration-services/data-flow/excel-source.md)   
 [Destino do Excel](../../integration-services/data-flow/excel-destination.md)   
 [Trabalhando com arquivos do Excel com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  