---
description: Loop em arquivos e tabelas do Excel com um contêiner do Loop Foreach
title: Loop em arquivos e tabelas do Excel com um contêiner do Loop Foreach | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: a5393c1a-cc37-491a-a260-7aad84dbff68
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0eaa6b0cbe19656096cdb47a31ec73b5fd4ade7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88392622"
---
# <a name="loop-through-excel-files-and-tables-with-a-foreach-loop-container"></a>Loop em arquivos e tabelas do Excel com um contêiner do Loop Foreach

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Os procedimentos neste tópico descrevem como criar um loop através de pastas de trabalho do Excel ou através de tabelas em uma pasta de trabalho do Excel, usando o contêiner Loop Foreach com o enumerador apropriado.  

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).
 
## <a name="to-loop-through-excel-files-by-using-the-foreach-file-enumerator"></a>Para criar um loop através de arquivos do Excel usando o enumerador de Arquivo Foreach  
  
1.  Crie uma variável de cadeia que receberá o caminho atual do Excel e nome de arquivo em cada iteração do loop. Para evitar problemas de validação, atribua um caminho de Excel válido e um nome de arquivo como o valor inicial da variável. (A expressão de amostra exibida mais adiante neste procedimento usa o nome da variável, `ExcelFile`.)  
  
2.  Como alternativa, crie outra variável de cadeia que irá conter o valor do argumento Propriedades Estendidas da cadeia de conexão do Excel. Este argumento contém uma série de valores que especificam a versão do Excel, determinam se a primeira linha contém nomes de coluna e se o modo de importação é usado. (A expressão de amostra exibida mais adiante neste procedimento usa o nome de variável `ExtProperties`, com um valor inicial de “`Excel 12.0;HDR=Yes`”.)  
  
     Se você não usar uma variável para o argumento Propriedades Estendidas, adicione-a manualmente à expressão que contém a cadeia de conexão.  
  
3.  Adicione um contêiner Loop Foreach à guia **Fluxo de Controle** . Para obter informações sobre como configurar um Contêiner Loop Foreach, consulte [Para configurar um contêiner Loop Foreach](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
4.  Na página **Coleção** do **Editor de Loop Foreach**, selecione o enumerador de Arquivo Foreach, especifique a pasta na qual as pastas de trabalho do Excel estão situadas e especifique o filtro de arquivo (geralmente *.xlsx).  
  
5.  Na página **Mapeamento de Variáveis** , mapeie Index 0 para uma variável de cadeia definida pelo usuário que receberá o caminho atual do Excel e o nome de arquivo em cada iteração do loop. (A expressão de amostra exibida mais adiante neste procedimento usa o nome da variável `ExcelFile`.)  
  
6.  Feche o **Editor de Loop Foreach**.  
  
7.  Adicione um gerenciador de conexões do Excel para o pacote conforme descrito em [Adicionar, excluir ou compartilhar um Gerenciador de Conexões em um pacote](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655). Selecione uma pasta de trabalho existente do Excel para a conexão para evitar erros de validação.  
  
    > [!IMPORTANT]  
    >  Para evitar erros de validação conforme você configura tarefas e componentes de fluxo de dados que usam esse gerenciador de conexões do Excel, selecione uma pasta de trabalho existente do Excel no **Editor do Gerenciador de Conexões do Excel**. O gerenciador de conexões não usará esta pasta de trabalho em tempo de execução depois que você configurar uma expressão para a propriedade **ConnectionString** conforme descrito nas etapas a seguir. Após criar e configurar o pacote, você pode limpar o valor da propriedade **ConnectionString** na janela Propriedades. No entanto, se você limpar esse valor, a propriedade da cadeia de conexão do gerenciador de conexões do Excel não será mais válida até que Loop Foreach seja executado. Portanto você deve definir a propriedade **DelayValidation** como **True** nas tarefas ou no pacote em que o gerenciador de conexões é usado para evitar erros de validação.  
    >   
    >  Você também deve usar o valor padrão de **False** para a propriedade **RetainSameConnection** do gerenciador de conexões do Excel. Se você alterar esse valor para **True**, cada iteração do loop continuará a abrir a primeira pasta de trabalho do Excel.  
  
8.  Selecione o novo gerenciador de conexões do Excel, clique na propriedade **Expressões** na janela Propriedades e clique nas reticências.  
  
9. No **Editor de Expressões de Propriedades**, selecione a propriedade **ConnectionString** e depois clique no botão de reticências.  
  
10. No Construtor de Expressões, digite a expressão a seguir:  
  
    ```  
    "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=\"" + @[User::ExtProperties] + "\""  
    ```  
  
     Observe o uso do caractere de escape "\\" para não ter que usar as aspas exigidas no valor do argumento Propriedades Estendidas.  
  
     O argumento Propriedades Estendidas não é opcional. Se você não usar uma variável para conter seu valor, será preciso adicioná-la manualmente à expressão, como neste exemplo:  
  
    ```  
    "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=Excel 12.0"  
    ```  
  
11. Crie tarefas no contêiner Loop Foreach que usam o gerenciador de conexões do Excel para executar as mesmas operações em cada pasta de trabalho do Excel que corresponde ao local e padrão de arquivo especificado.  
  
## <a name="to-loop-through-excel-tables-by-using-the-foreach-adonet-schema-rowset-enumerator"></a>Para criar um loop através de tabelas do Excel usando o enumerador de Conjunto de Linhas de Esquema ADO.NET Foreach  
  
1.  Crie um gerenciador de conexões ADO.NET que use o Provedor Microsoft ACE OLE DB para se conectar a uma pasta de trabalho do Excel. Na página Tudo da caixa de diálogo **Gerenciador de Conexões**, insira a versão do Excel, neste caso, Excel 12.0, como o valor da propriedade Propriedades Estendidas. Para obter mais informações, consulte [adicionar, excluir ou compartilhar um Gerenciador de Conexão em um pacote](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655).  
  
2.  Crie uma variável de cadeia que receberá o nome da tabela atual em cada iteração do loop.  
  
3.  Adicione um contêiner Loop Foreach à guia **Fluxo de Controle** . Para obter informações sobre como configurar um contêiner Loop Foreach, consulte [Para configurar um contêiner Loop Foreach](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
4.  Na página **Coleção** do **Editor de Loop Foreach**, selecione o Enumerador de Conjunto de Linhas de Esquema ADO.NET Foreach.  
  
5.  Como valor de **Conexão**, selecione o gerenciador de conexões ADO.NET que você criou anteriormente.  
  
6.  Como valor de **Esquema**, selecione Tabelas.  
  
    > [!NOTE]  
    >  A lista de tabelas em uma pasta de trabalho do Excel inclui planilhas (que têm o sufixo $) e intervalos nomeados. Se você tiver que filtrar a lista para apenas planilhas ou apenas intervalos nomeados, talvez seja necessário gravar o código personalizado em uma tarefa Script para essa finalidade. Para obter mais informações, consulte [Trabalhando com arquivos do Excel com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md).  
  
7.  Na página **Mapeamentos de Variáveis** , mapeie Index 2 para a variável de cadeia criada anteriormente para manter o nome da tabela atual.  
  
8.  Feche o **Editor de Loop Foreach**.  
  
9. Crie tarefas no contêiner Loop Foreach que usam o gerenciador de conexões do Excel para executar as mesmas operações em cada tabela do Excel na pasta de trabalho especificada. Se você usar uma tarefa Script para examinar o nome de tabela enumerado ou para trabalhar com tabelas individualmente, lembre-se de adicionar a variável de cadeia à propriedade ReadOnlyVariables da tarefa Script.  
  
## <a name="see-also"></a>Consulte Também  
 [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)  
 [Para configurar um contêiner Loop Foreach](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)   
 [Adicionar ou alterar uma expressão de propriedade](../../integration-services/expressions/add-or-change-a-property-expression.md)   
 [Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Origem do Excel](../../integration-services/data-flow/excel-source.md)   
 [Destino do Excel](../../integration-services/data-flow/excel-destination.md)   
 [Trabalhar com arquivos do Excel com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
