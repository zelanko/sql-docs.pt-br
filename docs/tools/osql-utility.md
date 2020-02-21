---
title: Utilitário osql
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- operating systems [SQL Server], commands
- osql utility [SQL Server]
- stored procedures [SQL Server], command prompt
- scripts [SQL Server], command prompt
- RESET command
- GO command
- command prompt utilities [SQL Server], osql
- CTRL+C command
ms.assetid: cf530d9e-0609-4528-8975-ab8e08e40b9a
author: markingmyname
ms.author: maghan
ms.manageR: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/16/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: dbc103ea44027056541dada86451c757a27619ff
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307360"
---
# <a name="osql-utility"></a>Utilitário osql

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O utilitário **osql** permite inserir instruções [!INCLUDE[tsql](../includes/tsql-md.md)] , procedimentos de sistema e arquivos de script. Esse utilitário usa o ODBC para comunicar-se com o servidor.  
  
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Evite usar esse recurso em novo trabalho de desenvolvimento e planeje modificar os aplicativos que utilizam o recurso atualmente. Use **sqlcmd** em vez disso. Para saber mais, confira [sqlcmd Utility](../tools/sqlcmd-utility.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
osql  
[-?] |  
[-L] |  
[  
  {  
     {-Ulogin_id [-Ppassword]} | -E }  
     [-Sserver_name[\instance_name]] [-Hwksta_name] [-ddb_name]  
     [-ltime_out] [-ttime_out] [-hheaders]  
     [-scol_separator] [-wcolumn_width] [-apacket_size]  
     [-e] [-I] [-D data_source_name]  
     [-ccmd_end] [-q "query"] [-Q"query"]  
     [-n] [-merror_level] [-r {0 | 1}]  
     [-iinput_file] [-ooutput_file] [-p]  
     [-b] [-u] [-R] [-O]  
]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Exibe o resumo da sintaxe de opções **osql** .  
  
 **-L**  
 Lista os servidores configurados localmente e os nomes dos servidores que estão transmitindo na rede.  
  
> [!NOTE]  
>  Devido à natureza da transmissão em redes, o **osql** pode não receber a tempo uma resposta de todos os servidores. Assim, a lista de servidores retornada pode variar para cada invocação dessa opção.  
  
 **-U** _login_id_  
 É a identificação de logon do usuário. IDs de logon diferenciam maiúsculas de minúsculas.  
  
 **-P** _password_  
 É uma senha especificada pelo usuário. Se a opção **-P** não for usada, o **osql** solicitará a senha. Se a opção **-P** for usada ao término do prompt de comando sem uma senha, **osql** usará a senha padrão (NULL).  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Para saber mais, confira [Strong Passwords](../relational-databases/security/strong-passwords.md).  
  
 As senhas diferenciam maiúsculas de minúsculas.  
  
 A variável de ambiente OSQLPASSWORD permite definir uma senha padrão para a sessão atual. Assim, senhas não têm de ser codificadas em arquivos em lote.  
  
 Se você não especificar uma senha com a opção **-P** , **osql** verificará primeiro a variável OSQLPASSWORD. Se nenhum valor for definido, o **osql** usará a senha padrão, NULL. O exemplo seguinte define a variável OSQLPASSWORD em um prompt de comando e então acessa o utilitário **osql** :  
  
```  
C:\>SET OSQLPASSWORD=abracadabra  
C:\>osql   
```  
  
> [!IMPORTANT]  
>  Para mascarar a senha, não especifique a opção **-P** juntamente com a opção **-U** . Em vez disso, depois de especificar o **osql** juntamente com a opção **-U** e outras opções (não especificar **-P**), pressione ENTER e o **osql** solicitará uma senha. Esse método garante que sua senha será mascarada quando for inserida.  
  
 **-E**  
 Usa uma conexão confiável em vez de pedir uma senha.  
  
 **-S** _server\_name_[ **\\** _instance\_name_]  
 Especifica uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a qual se conectar. Especifica *server_name* para a conexão com a instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nesse servidor. Especifica _server\_name_ **\\** _instance\_name_ para conectar-se a uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nesse servidor. Se nenhum servidor for especificado, o **osql** se conectará à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local. Essa opção é obrigatória quando o **osql** é executado de um computador remoto na rede.  
  
 **-H** _wksta_name_  
 É um nome de estação de trabalho. O nome de estação de trabalho é armazenado em **sysprocesses.hostname** e exibido por **sp_who**. Se essa opção não for especificada, o nome do computador atual será presumido.  
  
 **-d** _db_name_  
 Emite uma instrução USE *db_name* quando **osql**é iniciado.  
  
 **-l** _time_out_  
 Especifica o número de segundos antes de um logon do **osql** expirar. O tempo limite padrão de logon do **osql** é de oito segundos.  
  
 **-t** _time_out_  
 Especifica o número de segundos antes de um comando expirar. Se não for especificado um valor de *time_out* , os comandos não vão atingir o tempo limite.  
  
 **-h** _headers_  
 Especifica o número de linhas a imprimir entre cabeçalhos de coluna. O padrão é imprimir títulos uma vez para cada conjunto de resultados de consulta. Use -1 para especificar que nenhum cabeçalho será impresso. Se -1 for usado, não deverá haver nenhum espaço entre o parâmetro e a configuração ( **-h-1**, não **-h -1**).  
  
 **-s** _col_separator_  
 Especifica o caractere do separador de colunas que, por padrão, é um espaço em branco. Para usar um caractere com um significado especial para o sistema operacional como, por exemplo, | ; & < >), coloque-o entre aspas duplas (").  
  
 **-w** _column_width_  
 Permite ao usuário definir a largura da tela de saída. O padrão é 80 caracteres. Quando uma linha de saída alcança sua largura de tela máxima, ela é quebrada em várias linhas.  
  
 **-a** _packet_size_  
 Permite solicitar um pacote de tamanho diferente. Os valores válidos para *packet_size* são 512 a 65.535. O valor padrão **osql** é o padrão do servidor. Um tamanho de pacote maior pode aumentar o desempenho na execução de scripts maiores, em que a quantidade de instruções SQL entre comandos GO é substancial. [!INCLUDE[msCoName](../includes/msconame-md.md)] indicam que 8192 geralmente é a configuração mais rápida para operações de cópia em massa. Um tamanho de pacote maior pode ser solicitado, mas o **osql** assumirá como padrão o padrão do servidor se a solicitação não puder ser atendida.  
  
 **-e**  
 Duplica a entrada.  
  
 **-I**  
 Ativa a opção de conexão QUOTED_IDENTIFIER.  
  
 **-D** _data_source_name_  
 Conecta-se a uma fonte de dados ODBC que é definida usando o driver ODBC do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A conexão **osql** usa as opções especificadas na fonte de dados.  
  
> [!NOTE]  
>  Essa opção não trabalha com fontes de dados definidas para outros drivers.  
  
 **-c** _cmd_end_  
 Especifica o terminador de comando. Por padrão, comandos são encerrados e enviados ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se GO for inserido sozinho em uma linha. Quando você redefinir o terminador de comando, não use palavras reservadas do [!INCLUDE[tsql](../includes/tsql-md.md)] nem caracteres que tenham significado especial para o sistema operacional, sejam ou não precedidos por uma barra invertida.  
  
 **-q "** _query_ **"**  
 Executa uma consulta quando o **osql** é iniciado, mas não encerra o **osql** quando a consulta é concluída. (Observe que a instrução de consulta não deve incluir a instrução GO). Se você emitir uma consulta de um arquivo em lote, use %variáveis ou %variáveis% de ambiente. Por exemplo:  
  
```  
SET table=sys.objects  
osql -E -q "select name, object_id from %table%"  
```  
  
 Coloque a consulta entre aspas duplas e qualquer coisa incorporada na consulta entre aspas simples.  
  
 **-Q"** _query_ **"**  
 Executa uma consulta e imediatamente encerra o **osql**. Coloque a consulta entre aspas duplas e qualquer coisa incorporada na consulta entre aspas simples.  
  
 **-n**  
 Remove a numeração e o símbolo de prompt (>) das linhas de entrada.  
  
 **-m** _error_level_  
 Personaliza a exibição de mensagens de erro. São exibidos o número da mensagem, o estado e o nível de erros com o nível de severidade especificado ou superior. Nada é exibido para erros de níveis abaixo do nível especificado. Use **-1** para especificar que todos os cabeçalhos retornem com mensagens, até mesmo mensagens informativas. Se **-1**for usado, não deverá haver espaço entre o parâmetro e a configuração ( **-m-1**, não **-m -1**).  
  
 **-r** { **0**| **1**}  
 Redireciona a saída da mensagem para a tela (**stderr**). Se você não especificar um parâmetro ou especificar **0**, serão redirecionadas somente mensagens de erro com nível de severidade 11 ou superior. Se você especificar **1**, serão redirecionadas todas as saídas da mensagem, incluindo “print”.  
  
 **-i** _input_file_  
 Identifica o arquivo que contém um lote de instruções SQL ou procedimentos armazenados. O operador de comparação menor que ( **\<** ) pode ser usado no lugar de **-i**.  
  
 **-o** _output_file_  
 Identifica o arquivo que recebe a saída do **osql**. O operador de comparação maior que ( **>** ) pode ser usado no lugar de **-o**.  
  
 Se *input_file* não for Unicode e **-u** não for especificado, *output_file* será armazenado no formato OEM. Se *input_file* for Unicode ou **-u** for especificado, *output_file* será armazenado em formato Unicode.  
  
 **-p**  
 Imprime estatísticas de desempenho.  
  
 **-b**  
 Especifica que o **osql** é encerrado e retorna um valor DOS ERRORLEVEL em caso de erro. O valor retornado à variável DOS ERRORLEVEL será 1 quando a mensagem de erro do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiver um nível de severidade de 11 ou superior, caso contrário, o valor retornado será 0. [!INCLUDE[msCoName](../includes/msconame-md.md)] Arquivos em lote do MS-DOS podem testar o valor de DOS ERRORLEVEL e tratar o erro adequadamente.  
  
 **-u**  
 Especificar que *output_file* será armazenado em formato Unicode, independentemente do formato de *input_file*.  
  
 **-R**  
 Especifica que o driver ODBC do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa configurações de cliente ao converter dados de moeda, data e hora em dados de caractere.  
  
 **-O**  
 Especifica que certos recursos do **osql** sejam desativados para corresponder ao comportamento de versões anteriores do **isql**. Estes recursos são desativados:  
  
-   Processamento em lote de EOF  
  
-   Escalonamento automático da largura do console  
  
-   Mensagens largas  
  
 Também define o valor DOS ERRORLEVEL padrão como -1.  
  
> [!NOTE]  
>  As opções **-n**, **-O** e **-D** já não têm suporte do **osql**.  
  
## <a name="remarks"></a>Comentários  
 O utilitário **osql** é iniciado diretamente do sistema operacional com as opções que diferenciam maiúsculas de minúsculas listadas aqui. Depois que o **osql**é iniciado, ele aceita instruções SQL e as envia interativamente ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Os resultados são formatados e exibidos na tela (**stdout**). Use QUIT ou EXIT para sair do **osql**.  
  
 Se você não especificar um nome de usuário ao iniciar o **osql**, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fará a verificação e usará variáveis de ambiente, como **osqluser=(** _user_ **)** ou **osqlserver=(** _server_ **)** . Se nenhuma variável de ambiente for definida, o nome de usuário da estação de trabalho será usado. Se você não especificar um servidor, o nome da estação de trabalho será usado.  
  
 Se as opções **-U** ou **-P** não forem usadas, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tentará conectar usando o Modo de Autenticação do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. A autenticação baseia-se na conta do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows do usuário que está executando o **osql**.  
  
 O utilitário **osql** usa a API ODBC. O utilitário usa as configurações padrão do driver ODBC do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para as opções de conexão ISO do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obter mais informações, consulte Efeitos de Opções ANSI.  
  
> [!NOTE]  
>  O utilitário **osql** não dá suporte a tipos de dados CLR definidos pelo usuário. Para processar esses tipos de dados, você deve usar o utilitário **sqlcmd** . Para saber mais, confira [sqlcmd Utility](../tools/sqlcmd-utility.md).  
  
## <a name="osql-commands"></a>Comandos OSQL  
 Além das instruções [!INCLUDE[tsql](../includes/tsql-md.md)] dentro do **osql**, os comandos a seguir também estão disponíveis.  
  
|Comando|Descrição|  
|-------------|-----------------|  
|GO|Executa todas as instruções inseridas depois do último GO.|  
|RESET|Apaga as instruções inseridas.|  
|QUIT ou EXIT( )|Sai do **osql**.|  
|CTRL+C|Finaliza uma consulta sem sair do **osql**.|  
  
> [!NOTE]  
>  Os comandos !! e ED não têm mais suporte no **osql**.  
  
 Os terminadores de comando GO (por padrão), RESET EXIT, QUIT e CTRL+C só serão reconhecidos se forem exibidos no início de uma linha, imediatamente após o prompt do **osql** .  
  
 GO sinaliza tanto o término de um lote quanto a execução de qualquer instrução de cachê do [!INCLUDE[tsql](../includes/tsql-md.md)] . Quando você pressiona ENTER ao término de cada linha de entrada, o **osql** armazena as instruções nessa linha em cache. Quando você pressiona ENTER depois de digitar GO, todas as instruções atualmente em cache são enviadas como um lote ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 O utilitário **osql** atual funciona como se houvesse um comando GO implícito ao final de qualquer script executado, portanto todas as instruções no script são executadas.  
  
 Termine um comando digitando um começo de linha com um terminador de comando. Você pode seguir o terminador de comando com um inteiro para especificar quantas vezes o comando deve ser executado. Por exemplo, para executar esse comando 100 vezes, digite:  
  
```  
SELECT x = 1  
GO 100  
```  
  
 Os resultados são impressos após o término de execução. O**osql** não aceita mais de 1.000 caracteres por linha. Instruções grandes devem ser divididas em várias linhas.  
  
 Os recursos de recall de comando do Windows podem ser usados para chamar novamente e modificar instruções **osql** . O buffer de consulta existente pode ser desmarcado digitando RESET.  
  
 Ao executar procedimentos armazenados, o **osql** imprime uma linha em branco entre cada conjunto de resultados em um lote. Além disso, a mensagem "0 linhas afetadas" não aparece quando não se aplica à instrução executada.  
  
## <a name="using-osql-interactively"></a>Usando o osql interativamente  
 Para usar o **osql** interativamente, digite o comando **osql** (e qualquer uma das opções) em um prompt de comando.  
  
 Você pode ler em um arquivo contendo uma consulta (como Stores.qry) para execução pelo **osql** digitando um comando semelhante a este:  
  
```  
osql -E -i stores.qry  
```  
  
 Você pode ler em um arquivo contendo uma consulta (como Titles.qry) e direcionar os resultados a outro arquivo digitando um comando semelhante a este:  
  
```  
osql -E -i titles.qry -o titles.res  
```  
  
> [!IMPORTANT]  
>  Quando possível, use a opção **-E**(conexão de confiança).  
  
 Ao usar o **osql** interativamente, você pode ler um arquivo do sistema operacional no buffer de comandos com **:r**_file\_name_. Isso envia o script SQL no *file_name* diretamente para o servidor como um único lote.  
  
> [!NOTE]  
>  Ao usar o **osql**, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] trata o separador em lote GO, se ele for exibido em um arquivo de script SQL, como um erro de sintaxe.  
  
## <a name="inserting-comments"></a>Inserindo comentários  
 Você pode incluir comentários em uma instrução Transact-SQL enviada ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pelo **osql**. São permitidos dois tipos de estilos de comentário: `--` e `/*...*/`.  
  
## <a name="using-exit-to-return-results-in-osql"></a>Usando EXIT para retornar resultados no osql  
 Você pode usar o resultado de uma instrução SELECT como o valor de retorno do **osql**. Se ele for numérico, a última coluna da última linha do resultado será convertida em um inteiro de 4 bytes (longo). O MS-DOS transmite o byte baixo para o processo pai ou nível de erro do sistema operacional. O Windows passa o número inteiro de 4 bytes. A sintaxe do é:  
  
```  
EXIT ( < query > )  
```  
  
 Por exemplo:  
  
```  
EXIT(SELECT @@ROWCOUNT)  
```  
  
 É possível incluir também o parâmetro EXIT como parte de um arquivo em lote. Por exemplo:  
  
```  
osql -E -Q "EXIT(SELECT COUNT(*) FROM '%1')"  
```  
  
 O utilitário **osql** passa tudo entre os parênteses **()** para o servidor exatamente como digitado. Se um procedimento de sistema armazenado selecionar um conjunto e retornar um valor, somente a seleção será retornada. A instrução EXIT **()** sem nada entre os parênteses executa tudo que a precede no lote e é encerrada sem valor retornado.  
  
 Há quatro formatos EXIT:  
  
-   EXIT  
  
> [!NOTE]  
>  Não executa o lote; sai imediatamente e não retorna valor algum.  
  
-   EXIT **()**  
  
> [!NOTE]  
>  Executa o lote e então sai imediatamente e não retorna valor algum.  
  
-   EXIT **(** _query_ **)**  
  
> [!NOTE]  
>  Executa o lote, incluindo a consulta, e sai depois de retornar os resultados da consulta.  
  
-   RAISERROR com estado de 127  
  
> [!NOTE]  
>  Se for usado RAISERROR em um script **osql** e ocorrer um estado 127, o **osql** sairá e retornará a ID da mensagem para o cliente. Por exemplo:  
  
```  
RAISERROR(50001, 10, 127)  
```  
  
 Esse erro fará com que o script **osql** seja encerrado e retorne a ID da mensagem 50001 ao cliente.  
  
 Os valores de retorno de -1 a -99 são reservados pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]; o **osql** define estes valores:  
  
-   -100  
  
     Erro encontrado antes da seleção do valor de retorno.  
  
-   -101  
  
     Nenhuma linha encontrada ao se selecionar o valor de retorno.  
  
-   -102  
  
     Erro de conversão ao selecionar valor de retorno.  
  
## <a name="displaying-money-and-smallmoney-data-types"></a>Exibindo Tipos de Dados money e smallmoney  
 O**osql** exibe os tipos de dados **money** e **smallmoney** com duas casas decimais, embora o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] armazene o valor internamente com quatro casas decimais. Considere o exemplo:  
  
```  
SELECT CAST(CAST(10.3496 AS money) AS decimal(6, 4))  
GO  
```  
  
 Essa instrução produz um resultado de `10.3496`, que indica que o valor é armazenado com todas as casas decimais intactas.  
  
## <a name="see-also"></a>Consulte Também  
 [Comentário &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [-- &#40;Comment&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [CAST e CONVERT &#40;Transact-SQL&#41;](../t-sql/functions/cast-and-convert-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
