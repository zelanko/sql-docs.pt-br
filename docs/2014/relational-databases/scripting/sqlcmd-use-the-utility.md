---
title: Usar o utilitário sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL statements, executing
- command prompt utilities [SQL Server], sqlcmd
- statements [SQL Server], executing
- sqlcmd utility, about sqlcmd utility
ms.assetid: 3ec89119-7314-43ef-9e91-12e72bb63d62
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3647937630b259d60670cc470bbd1014dd288404
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62666901"
---
# <a name="use-the-sqlcmd-utility"></a>Usar o utilitário sqlcmd
  O utilitário `sqlcmd` é um utilitário de linha de comando para execução interativa ad hoc dos scripts e instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], e para automatização das tarefas de script do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para usar o `sqlcmd` de forma interativa ou para criar arquivos de script para serem executados com o `sqlcmd`, os usuários devem entender o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O utilitário `sqlcmd` é normalmente usado das seguintes maneiras:  
  
-   Os usuários inserem interativamente instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] de forma semelhante ao trabalho no prompt de comando. Os resultados são exibidos no prompt de comando. Para abrir uma janela de prompt de comando, clique em **Iniciar**, clique em **Todos os Programas**, aponte para **Acessórios**e, em seguida, clique em **Prompt de Comando**. No prompt de comando, digite `sqlcmd` seguido por uma lista de opções que você deseja. Para obter uma lista completa das opções que são suportados pelo `sqlcmd`, consulte [utilitário sqlcmd](../../tools/sqlcmd-utility.md).  
  
-   Os usuários enviam um trabalho `sqlcmd` especificando uma única instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a ser executada ou apontando o utilitário para um arquivo de texto que contenha instruções[!INCLUDE[tsql](../../includes/tsql-md.md)] a serem executadas. O resultado geralmente é dirigido a um arquivo de texto, mas também pode ser exibido no prompt de comando.  
  
-   [modo SQLCMD](edit-sqlcmd-scripts-with-query-editor.md) no Editor de Consultas [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
-   SQL Server Management Objects (SMO)  
  
-   Trabalhos do CmdExec do SQL Server Agent.  
  
## <a name="typically-used-sqlcmd-options"></a>Opções sqlcmd normalmente usadas  
 As opções a seguir são usadas com mais frequência:  
  
-   A opção de servidor (**-S**) que identifica a instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual `sqlcmd` se conecta.  
  
-   Opções de autenticação (**-E**, **- U**, e **-P**) que especificam as credenciais que `sqlcmd` usa para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  A opção **-E** é o padrão e não precisa ser especificada.  
  
-   Opções de entrada (**-Q**, **- q**, e **-i**) que identificam o local da entrada para `sqlcmd`.  
  
-   A opção de saída (**-o**) que especifica o arquivo no qual `sqlcmd` é colocar sua saída.  
  
## <a name="connecting-to-the-sqlcmd-utility"></a>Conectando-se ao utilitário sqlcmd  
 Estes são os usos comuns do utilitário `sqlcmd`:  
  
-   Conectando-se a uma instância padrão usando a Autenticação do Windows para executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] de forma interativa:  
  
    ```  
    sqlcmd -S <ComputerName>  
    ```  
  
    > [!NOTE]  
    >  No exemplo anterior, **-E** não é especificado porque ele é o padrão e `sqlcmd` conecta-se à instância padrão usando a autenticação do Windows.  
  
-   Conexão com uma instância nomeada usando a Autenticação do Windows para executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] interativamente:  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName>  
    ```  
  
     ou em  
  
    ```  
    sqlcmd -S .\<InstanceName>  
    ```  
  
-   Conectando-se com uma instância nomeada, usando a Autenticação do Windows e especificando arquivos de entrada e saída:  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName> -i <MyScript.sql> -o <MyOutput.rpt>  
    ```  
  
-   Conectando-se a uma instância padrão no computador local usando a Autenticação do Windows, executando uma consulta e executando o `sqlcmd` até mesmo após a consulta ter sido concluída:  
  
    ```  
    sqlcmd -q "SELECT * FROM AdventureWorks2012.Person.Person"  
    ```  
  
-   Conectando-se a uma instância padrão no computador local usando a Autenticação do Windows, executando uma consulta, direcionando a saída para um arquivo e fazendo com que o `sqlcmd` feche após a conclusão da consulta:  
  
    ```  
    sqlcmd -Q "SELECT * FROM AdventureWorks2012.Person.Person" -o MyOutput.txt  
    ```  
  
-   Conectando-se a uma instância nomeada que usa a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar de forma interativa as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], com o `sqlcmd` solicitando uma senha:  
  
    ```  
    sqlcmd -U MyLogin -S <ComputerName>\<InstanceName>  
    ```  
  
    > [!NOTE]  
    >  Para consultar uma lista das opções que têm suporte no utilitário `sqlcmd`, execute `sqlcmd -?`.  
  
## <a name="running-transact-sql-statements-interactively-by-using-sqlcmd"></a>Executando instruções Transact-SQL interativamente usando o sqlcmd  
 Você pode usar o utilitário `sqlcmd` interativamente para executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em uma janela de prompt de comando. Para executar interativamente [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções usando `sqlcmd`, execute o utilitário sem usar o **-Q**, **- q**, **-Z**, ou **- i** as opções para especificar qualquer entrada arquivos ou consultas. Por exemplo:   
  
 `sqlcmd -S <ComputerName>\<InstanceName>`  
  
 Quando o comando é executado sem arquivos ou consultas de entrada, o `sqlcmd` se conecta à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, exibe uma nova linha com um `1>` seguido de um sublinhado intermitente, que é conhecido como o prompt do `sqlcmd`. O `1` significa que esta é a primeira linha de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)], e o prompt do `sqlcmd` é o ponto no qual a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] iniciará quando ela for digitada nele.  
  
 No prompt `sqlcmd`, você pode digitar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e comandos `sqlcmd`, como `GO` e `EXIT`. Cada instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] é colocada em um buffer denominado cache de instrução. Essas instruções são enviadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depois que você digita o comando `GO` e pressiona ENTER. Para sair `sqlcmd`, digite `EXIT` ou `QUIT` no início de uma nova linha.  
  
 Para limpar o cache de instruções, digite `:RESET`. Digitação `^C` faz com que `sqlcmd` para sair. O `^C` também pode ser usado para interromper a execução do cache de instrução depois que um comando `GO` é emitido.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções que são inseridas em uma sessão interativa podem ser editadas digitando o **: ED** comando e o `sqlcmd` prompt. O editor será aberto e, após a edição da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] e de fechamento do editor, a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] revisada aparecerá na janela de comando. Insira `GO` para executar revisada [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.  
  
## <a name="quoted-strings"></a>Cadeia de caracteres entre aspas  
 Os caracteres entre aspas são usados sem nenhum pré-processamento adicional, a não ser quando as aspas podem ser inseridas em uma cadeia de caracteres através de duas aspas consecutivas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trata esta sequência de caracteres como uma aspa. (Porém, a tradução acontece no servidor.) Não serão expandidas variáveis de script quando elas aparecerem dentro de uma cadeia de caracteres.  
  
 Por exemplo:   
  
 `sqlcmd`  
  
 `PRINT "Length: 5"" 7'";`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Length: 5" 7'`  
  
## <a name="strings-that-span-multiple-lines"></a>Cadeias de caracteres que abrangem várias linhas  
 O `sqlcmd` oferece suporte a scripts com cadeias de caracteres que abrangem várias linhas. Por exemplo, a seguinte instrução `SELECT` estende diversas linhas, mas é uma única cadeia de caracteres executada ao pressionar a tecla ENTER, depois de digitar `GO`.  
  
 `SELECT First line`  
  
 `FROM Second line`  
  
 `WHERE Third line;`  
  
 `GO`  
  
## <a name="interactive-sqlcmd-example"></a>Exemplo interativo do sqlcmd  
 Este é um exemplo do que você verá ao executar o `sqlcmd` interativamente.  
  
 Ao abrir uma janela de prompt de comando, você verá uma linha semelhante a esta:  
  
 `C:\> _`  
  
 Isso significa que a pasta `C:\` é a pasta atual, e se você especificar um nome de arquivo, o Windows vai procurar o arquivo nessa pasta.  
  
 Digite `sqlcmd` para se conectar à instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador local, e o conteúdo da janela Prompt de Comando será:  
  
 `C:\>sqlcmd`  
  
 `1> _`  
  
 Isso significa que você se conectou com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o `sqlcmd` agora está pronto para aceitar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e os comandos `sqlcmd` . O sublinhado intermitente que precede o `1>` é o prompt `sqlcmd` que marca o local no qual as instruções e os comandos que você digita serão exibidos. Agora, digite `USE AdventureWorks2012` e pressione ENTER e, em seguida, digite `GO` e pressione ENTER. O conteúdo da janela de prompt de comando será:  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `1> _`  
  
 Pressionar ENTER depois de inserir `USE AdventureWorks2012` sinaliza ao `sqlcmd` para iniciar uma linha nova. Ao pressionar ENTER após digitar `GO,` , você sinalizou o `sqlcmd` para enviar a instrução `USE AdventureWorks2012` à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. `sqlcmd` retornou uma mensagem para indicar que a instrução `USE` foi concluída com êxito e exibiu um novo prompt `1>` como sinal para inserir uma nova instrução ou comando.  
  
 O exemplo a seguir mostra o conteúdo da janela de prompt de comando ao você digitar uma instrução `SELECT` , uma `GO` para executar o comando `SELECT`, e uma `EXIT` para fechar o `sqlcmd`:  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `BusinessEntityID   FirstName                 LastName`  
  
 `----------- -------------------------------- -----------`  
  
 `1           Syed                             Abbas`  
  
 `2           Catherine                        Abel`  
  
 `3           Kim                              Abercrombie`  
  
 `(3 rows affected)`  
  
 `1> EXIT`  
  
 `C:\>`  
  
 As linhas depois da linha `3> GO` são a saída de uma instrução `SELECT` . Depois que você gerar a saída, o `sqlcmd` redefine o prompt `sqlcmd` e exibe `1>`. Após digitar `EXIT` na linha `1>`, a janela de prompt de comando exibe a mesma linha, como fez quando você a abriu primeiramente. Isto indica que o `sqlcmd` encerrou sua sessão. Agora você pode fechar a janela de prompt de comando digitando outro comando `EXIT` .  
  
## <a name="running-transact-sql-script-files-by-using-sqlcmd"></a>Executando arquivos de script Transact-SQL usando o sqlcmd  
 Você pode usar o`sqlcmd` para executar arquivos de script de banco de dados. Os arquivos de script são arquivos de texto que contêm uma mistura de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], comandos `sqlcmd` e variáveis de script. Para obter mais informações sobre como usar variáveis de script, veja [Usar sqlcmd com variáveis de script](sqlcmd-use-with-scripting-variables.md). O `sqlcmd` funciona com instruções, comandos e variáveis de script em um arquivo de script de modo semelhante ao modo como funciona com instruções e comandos inseridos interativamente. A principal diferença é que o `sqlcmd` faz a leitura por meio do arquivo de entrada sem pausa, em vez de esperar que um usuário insira as instruções, os comandos e as variáveis de script.  
  
 Existem maneiras diferentes de criar arquivos de script de banco de dados:  
  
-   Você pode criar e depurar interativamente uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e em seguida salvar o conteúdo da janela de consulta como arquivo script.  
  
-   Você pode criar um arquivo de texto que contém instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] usando um editor de textos, como o Bloco de Notas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-running-a-script-by-using-sqlcmd"></a>A. Executando um script usando o sqlcmd  
 Iniciar o Bloco de Notas e digitar as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 Criar uma pasta nomeada `MyFolder` e, em seguida, salvar o script como o arquivo `MyScript.sql` na pasta `C:\MyFolder`. Digite a sequência abaixo no prompt de comando para executar o script e colocar a saída em `MyOutput.txt` , em `MyFolder`:  
  
 `sqlcmd -i C:\MyFolder\MyScript.sql -o C:\MyFolder\MyOutput.txt`  
  
 Ao exibir os conteúdos de `MyOutput.txt` no Bloco de Notas, você verá o seguinte:  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `BusinessEntityID FirstName   LastName`  
  
 `---------------- ----------- -----------`  
  
 `1                Syed        Abbas`  
  
 `2                Catherine   Abel`  
  
 `3                Kim         Abercrombie`  
  
 `(3 rows affected)`  
  
### <a name="b-using-sqlcmd-with-a-dedicated-administrative-connection"></a>B. Usando o sqlcmd com uma conexão administrativa dedicada  
 No exemplo a seguir, `sqlcmd` é usado para se conectar a um servidor que tem um problema de bloqueio utilizando a conexão de administrador dedicada (DAC).  
  
 `C:\>sqlcmd -S ServerName -A`  
  
 `1> SELECT blocked FROM sys.dm_exec_requests WHERE blocked <> 0;`  
  
 `2> GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `spid   blocked`  
  
 `------ -------`  
  
 `62       64`  
  
 `(1 rows affected)`  
  
 Use o `sqlcmd` para finalizar o processo de bloqueio.  
  
 `1> KILL 64;`  
  
 `2> GO`  
  
### <a name="c-using-sqlcmd-to-execute-a-stored-procedure"></a>C. Usando o sqlcmd para executar um procedimento armazenado  
 O exemplo a seguir mostra como executar um procedimento armazenado usando o `sqlcmd`. Criar o seguinte procedimento armazenado.  
  
 `USE AdventureWorks2012;`  
  
 `IF OBJECT_ID ( ' dbo.ContactEmailAddress, 'P' ) IS NOT NULL`  
  
 `DROP PROCEDURE dbo.ContactEmailAddress;`  
  
 `GO`  
  
 `CREATE PROCEDURE dbo.ContactEmailAddress`  
  
 `(`  
  
 `@FirstName nvarchar(50)`  
  
 `,@LastName nvarchar(50)`  
  
 `)`  
  
 `AS`  
  
 `SET NOCOUNT ON`  
  
 `SELECT EmailAddress`  
  
 `FROM Person.Person`  
  
 `WHERE FirstName = @FirstName`  
  
 `AND LastName = @LastName;`  
  
 `SET NOCOUNT OFF`  
  
 No prompt `sqlcmd` , insira o seguinte:  
  
 `C:\sqlcmd`  
  
 `1> :Setvar FirstName Gustavo`  
  
 `1> :Setvar LastName Achong`  
  
 `1> EXEC dbo.ContactEmailAddress $(Gustavo),$(Achong)`  
  
 `2> GO`  
  
 `EmailAddress`  
  
 `-----------------------------`  
  
 `gustavo0@adventure-works.com`  
  
### <a name="d-using-sqlcmd-for-database-maintenance"></a>D. Usando o sqlcmd para manutenção do banco de dados  
 O exemplo a seguir mostra como usar o `sqlcmd` para uma tarefa de manutenção de banco de dados. Crie `C:\BackupTemplate.sql` com o seguinte código.  
  
 `USE master;`  
  
 `BACKUP DATABASE [$(db)] TO DISK='$(bakfile)';`  
  
 No prompt `sqlcmd` , insira o seguinte:  
  
 `C:\ >sqlcmd`  
  
 `1> :connect <server>`  
  
 `Sqlcmd: Successfully connected to server <server>.`  
  
 `1> :setvar db msdb`  
  
 `1> :setvar bakfile c:\msdb.bak`  
  
 `1> :r c:\BackupTemplate.sql`  
  
 `2> GO`  
  
 `Changed database context to 'master'.`  
  
 `Processed 688 pages for database 'msdb', file 'MSDBData' on file 2.`  
  
 `Processed 5 pages for database 'msdb', file 'MSDBLog' on file 2.`  
  
 `BACKUP DATABASE successfully processed 693 pages in 0.725 seconds (7.830 MB/sec)`  
  
### <a name="e-using-sqlcmd-to-execute-code-on-multiple-instances"></a>E. Usando o sqlcmd para executar o código em diversas instâncias  
 O código a seguir em um arquivo exibe um script que conecta a duas instâncias. Note o `GO` antes da conexão com a segunda instância.  
  
 `:CONNECT <server>\,<instance1>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
 `:CONNECT <server>\,<instance2>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
### <a name="e-returning-xml-output"></a>E. Retornando a saída XML  
 O exemplo a seguir mostra como a saída XML é retornada sem formatação, em um fluxo contínuo.  
  
 `C:\>sqlcmd -d AdventureWorks2012`  
  
 `1> :XML ON`  
  
 `1> SELECT TOP 3 FirstName + ' ' + LastName + ', '`  
  
 `2> FROM Person.Person`  
  
 `3> GO`  
  
 `Syed Abbas, Catherine Abel, Kim Abercrombie,`  
  
### <a name="f-using-sqlcmd-in-a-windows-script-file"></a>F. Usando o sqlcmd em um arquivo de script do Windows  
 Um `sqlcmd`comando como `sqlcmd -i C:\InputFile.txt -o C:\OutputFile.txt,` podem ser executados em um arquivo. bat junto com o VBScript. Nesse caso, não use opções interativas. O `sqlcmd` deve ser instalado no computador que está executando o arquivo .bat.  
  
 Primeiro, crie os quatro arquivos a seguir:  
  
-   C:\badscript.sql  
  
    ```  
    SELECT batch_1_this_is_an_error  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\goodscript.sql  
  
    ```  
    SELECT 'batch #1'  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\returnvalue.sql  
  
    ```  
    :exit(select 100)  
    @echo off  
    C:\windowsscript.bat  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
-   C:\windowsscript.bat  
  
    ```  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
 Em seguida, no prompt de comando, execute `C:\windowsscript.bat`:  
  
 `C:\>windowsscript.bat`  
  
 `Running badscript.sql`  
  
 `== An error occurred`  
  
 `Running goodscript.sql`  
  
 `Running returnvalue.sql`  
  
 `SQLCMD returned 100 to the command shell`  
  
### <a name="g-using-sqlcmd-to-set-encryption-on-windows-azure-sql-database"></a>G. Usando o sqlcmd para definir a criptografia em bancos de dados SQL do Windows Azure  
 Um `sqlcmd`pode ser executado em uma conexão para [!INCLUDE[ssSDS](../../includes/sssds-md.md)] dados para especificar a criptografia e certificados confiáveis. Dois ' sqlcmd ' ' opções estão disponíveis:  
  
-   A opção -N é usada pelo cliente para solicitar uma conexão criptografada. Essa opção é equivalente à opção `ENCRYPT = true`do ADO.net.  
  
-   A opção -C é usada pelo cliente para configurá-lo para confiar implicitamente no certificado do servidor e não validá-lo. Essa opção é equivalente à opção `TRUSTSERVERCERTIFICATE = true`do ADO.net.  
  
 O serviço [!INCLUDE[ssSDS](../../includes/sssds-md.md)] não dá suporte a todas as opções de `SET` disponíveis em uma instância do SQL Server. As opções a seguir emitem um erro quando a opção de `SET` correspondente é definida como `ON` ou `OFF`:  
  
-   SET ANSI_DEFAULTS  
  
-   SET ANSI_NULLS  
  
-   SET REMOTE_PROC_TRANSACTIONS  
  
-   SET ANSI_NULL_DEFAULT  
  
 As opções de SET a seguir não emitem exceções, mas não podem ser usadas. Elas são substituídas:  
  
-   SET CONCAT_NULL_YIELDS_NULL  
  
-   SET ANSI_PADDING  
  
-   SET QUERY_GOVERNOR_COST_LIMIT  
  
#### <a name="syntax"></a>Sintaxe  
 Os exemplos a seguir fazem referência a casos em que as configurações do provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client incluem: `ForceProtocolEncryption = False`, `Trust Server Certificate = No`  
  
 Conectar usando credenciais do Windows e comunicação criptografada:  
  
```  
SQLCMD -E -N  
  
```  
  
 Conectar usando credenciais do Windows e certificado do servidor confiável:  
  
```  
SQLCMD -E -C  
  
```  
  
 Conectar usando credenciais do Windows, comunicação criptografada e certificado do servidor confiável:  
  
```  
SQLCMD -E -N -C  
  
```  
  
 Os exemplos a seguir fazem referência a casos em que as configurações do provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client incluem: `ForceProtocolEncryption = True`, `TrustServerCertificate = Yes`.  
  
 Conectar usando credenciais do Windows, comunicação criptografada e certificado do servidor confiável:  
  
```  
SQLCMD -E  
  
```  
  
 Conectar usando credenciais do Windows, comunicação criptografada e certificado do servidor confiável:  
  
```  
SQLCMD -E -N  
  
```  
  
 Conectar usando credenciais do Windows, comunicação criptografada e certificado do servidor confiável:  
  
```  
SQLCMD -E -T  
  
```  
  
 Conectar usando credenciais do Windows, comunicação criptografada e certificado do servidor confiável:  
  
```  
SQLCMD -E -N -C  
  
```  
  
 Se o provedor especificar `ForceProtocolEncryption = True` a criptografia será habilitada mesmo que `Encrypt=No` esteja na cadeia de conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Usar sqlcmd com variáveis de script](sqlcmd-use-with-scripting-variables.md)   
 [Editar scripts SQLCMD com o Editor de Consultas](edit-sqlcmd-scripts-with-query-editor.md)   
 [Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)   
 [Criar uma etapa de trabalho CmdExec](../../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
