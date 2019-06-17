---
title: Utilitário sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- sqlcmd commands
- ED command
- sqlcmd utility
- command prompt utilities [SQL Server], sqlcmd
- '!! command'
- stored procedures [SQL Server], command prompt
- system stored procedures [SQL Server], command prompt
- sqlcmd utility, about sqlcmd utility
- scripts [SQL Server], command prompt
- RESET command
- GO command
ms.assetid: e1728707-5215-4c04-8320-e36f161b834a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d128085012c0ef3a9bc58b147f982a26d2c094b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035376"
---
# <a name="sqlcmd-utility"></a>sqlcmd Utility
  O `sqlcmd` utilitário permite que você insira [!INCLUDE[tsql](../includes/tsql-md.md)] instruções, procedimentos do sistema e arquivos de script no prompt de comando, na **Editor de consultas** no modo SQLCMD, em um arquivo de script do Windows ou em uma etapa de trabalho do sistema operacional (Cmd.exe) de um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Trabalho do agente. Esse utilitário usa ODBC para executar lotes [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usa o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]SqlClient para execução no normal e o modo SQLCMD na **Editor de consultas**. Quando `sqlcmd` é executado na linha de comando, `sqlcmd` usa o driver ODBC. Devido às diversas opções padrão que podem ser aplicadas, é possível observar um comportamento diferente ao executar a mesma consulta no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no Modo SQLCMD e no utilitário `sqlcmd`.  
  
 Atualmente, `sqlcmd` não requer um espaço entre a opção de linha de comando e o valor. Porém, em uma versão futura, um espaço pode ser necessário entre a opção de linha de comando e o valor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
   sqlcmd  
   -a  
   packet_size  
   -A (dedicated administrator connection)  
-b (terminate batch job if there is an error)  
-cbatch_terminator-C (trust the server certificate)  
-ddb_name-e (echo input)  
-E (use trusted connection)  
-fcodepage | i:codepage[,o:codepage] | o:codepage[,i:codepage]  
-hrows_per_header-Hworkstation_name-iinput_file-I (enable quoted identifiers)  
-k[1 | 2] (remove or replace control characters)  
-Kapplication_intent-llogin_timeout-L[c] (list servers, optional clean output)  
-merror_level-Mmultisubnet_failover-N (encrypt connection)  
-ooutput_file-p[1] (print statistics, optional colon format)  
-Ppassword-q "cmdline query"-Q "cmdline query" (and exit)  
-r[0 | 1] (msgs to stderr)  
-R (use client regional settings)  
-scol_separator-S [protocol:]server[\instance_name][,port]  
-tquery_timeout-u (unicode output file)  
-Ulogin_id-vvar = "value"-Verror_severity_level-wcolumn_width-W (remove trailing spaces)  
-x (disable variable substitution)  
-X[1] (disable commands, startup script, environment variables and optional exit)  
-yvariable_length_type_display_width-Yfixed_length_type_display_width-znew_password -Znew_password (and exit)  
  
-? (usage)  
```  
  
## <a name="command-line-options"></a>Opções de linha de comando  
 **Opções relacionadas a logon**  
  **-A**  
 Fazer logon no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com uma DAC (conexão de administrador dedicada). Esse tipo de conexão é usado para solucionar um problema no servidor. Isso funcionará apenas com computadores servidor que oferecem suporte para DAC. Se a DAC não estiver disponível, o `sqlcmd` gerará uma mensagem de erro e será encerrado. Para obter mais informações sobre a DAC, consulte [Conexão de diagnóstico para administradores de banco de dados](../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
 **-C**  
 Essa opção é usada pelo cliente para configurá-lo para confiar implicitamente no certificado do servidor sem validação. Essa opção é equivalente à opção `TRUSTSERVERCERTIFICATE = true`do ADO.NET.  
  
 **-d** _db_name_  
 Problemas de um `USE` *db_name* instrução ao iniciar `sqlcmd`. Essa opção define a variável de script SQLCMDDBNAME do `sqlcmd`. Isso especifica o banco de dados inicial. O padrão é a propriedade do banco de dados padrão de seu logon. Se o banco de dados não existir, será gerada uma mensagem de erro e o `sqlcmd` é encerrado.  
  
 **-l** _login_timeout_  
 Especifica o número de segundos antes que um logon do `sqlcmd` para o driver ODBC expire, ao tentar conectar a um servidor. Essa opção define a variável de script SQLCMDLOGINTIMEOUT do `sqlcmd`. O tempo limite padrão de logon do `sqlcmd` é de oito segundos. O tempo limite do logon deve ser um número entre 0 e 65534. O `sqlcmd` irá gerar uma mensagem de erro se o valor fornecido não for numérico ou não estiver nesse intervalo. Um valor de 0 especifica o tempo limite como infinito.  
  
 **-E**  
 Usa uma conexão confiável em vez de um nome de usuário e senha para fazer logon no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por padrão, sem a especificação de -E, `sqlcmd` usa a opção de conexão confiável.  
  
 A opção **-E** ignora possíveis definições de variável de ambiente de nome de usuário e senha como SQLCMDPASSWORD. Se a opção **-E** for usada com as opções **-U** ou **-P** , uma mensagem de erro será gerada.  
  
 **-H** _workstation_name_  
 Um nome de estação de trabalho. Essa opção define a variável de script SQLCMDWORKSTATION do `sqlcmd`. O nome da estação de trabalho é listado na coluna **hostname** da exibição de catálogo **sys.processes** e pode ser retornado usando o procedimento armazenado **sp_who**. Se essa opção não for especificada, o padrão será o nome do computador atual. Esse nome pode ser usado para identificar sessões `sqlcmd` diferentes.  
  
 **-K** _application_intent_  
 Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. O único valor com suporte no momento é **ReadOnly**. Se **-K** não estiver especificado, o utilitário sqlcmd não terá suporte à conectividade com uma réplica secundária em um grupo de disponibilidade AlwaysOn. Para obter mais informações, confira [Secundárias ativas: Réplicas secundárias legíveis](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 `-M` *multisubnet_failover*  
 Sempre especifique `-M` ao conectar-se ao ouvinte de um grupo de disponibilidade do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou de uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. `-M` proporciona a detecção mais rápida e a conexão com o servidor (atualmente) ativo. Se `-M` não for especificada, `-M` ficará desativada. Para obter mais informações sobre [!INCLUDE[ssHADR](../includes/sshadr-md.md)], consulte [ouvintes do grupo de disponibilidade, conectividade de cliente e Failover de aplicativo &#40;SQL Server&#41;](../database-engine/listeners-client-connectivity-application-failover.md), [criação e configuração dos grupos de disponibilidade &#40;SQL Server&#41;](../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clustering de Failover e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md), e [secundárias ativas: Réplicas secundárias legíveis](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) .  
  
 **-N**  
 Essa opção é usada pelo cliente para solicitar uma conexão criptografada.  
  
 **-P** _password_  
 É uma senha especificada pelo usuário. Senhas diferenciam maiúsculas e minúsculas. Se a opção - U for usada e o **-P** opção não for usada, e a variável de ambiente SQLCMDPASSWORD não tiver sido definida, `sqlcmd` solicita ao usuário uma senha. Se o **-P** opção é usada no final do prompt de comando sem uma senha `sqlcmd` usa a senha padrão (NULL).  
  
> [!IMPORTANT]  
>  Não use uma senha em branco. Use uma senha forte. Para saber mais, confira [Strong Passwords](../relational-databases/security/strong-passwords.md).  
  
 A solicitação de senha é exibida no console, como a seguir: `Password:`  
  
 A entrada do usuário está oculta. Isso significa que nada é exibido e o cursor fica em posição.  
  
 A variável de ambiente SQLCMDPASSWORD lhe permite definir uma senha padrão para a sessão atual. Assim, senhas não têm de ser hard-coded em arquivos em lote.  
  
 O exemplo a seguir define, em primeiro lugar, a variável SQLCMDPASSWORD no prompt de comando e acessa o utilitário `sqlcmd`. No prompt de comando, digite:  
  
 `SET SQLCMDPASSWORD= p@a$$w0rd`  
  
> [!IMPORTANT]  
>  A senha estará visível para qualquer um que tiver acesso ao monitor do seu computador.  
  
 No prompt de comando a seguir, digite:  
  
 `sqlcmd`  
  
 Se a combinação de nome de usuário e senha estiver incorreta, uma mensagem de erro será gerada.  
  
> [!NOTE]  
>  A variável de ambiente OSQLPASSWORD foi mantida para compatibilidade com versões anteriores. A variável de ambiente SQLCMDPASSWORD tem precedência sobre a variável de ambiente OSQLPASSWORD; Isso significa que `sqlcmd` e **osql** podem ser usados próximos um do outro sem interferência e que scripts antigos continuarão a funcionar.  
  
 Será gerada uma mensagem de erro se a opção **-P** for usada com a opção **-E** .  
  
 Se a opção **-P** for seguida de mais de um argumento, uma mensagem de erro será gerada e o programa será fechado.  
  
 **-S** [*protocol*:]*server*[ **\\** _instance_name_][ **,** _port_]  
 Especifica uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à qual se conectar. Define a variável de script SQLCMDSERVER do `sqlcmd`.  
  
 Especifique *server_name* para se conectar à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nesse computador servidor. Especifique *server_name* [ **\\** _instance_name_ ] para se conectar a uma instância nomeada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nesse computador servidor. Se nenhum servidor for especificado, o `sqlcmd` irá se conectar à instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no computador local. Essa opção é necessária quando se executa o `sqlcmd` de um computador remoto na rede.  
  
 *protocolo* pode ser `tcp` (TCP/IP), `lpc` (memória compartilhada), ou `np` (pipes nomeados).  
  
 Se você não especificar uma *nome_do_servidor* [ **\\** _instance_name_ ] ao iniciar o `sqlcmd`, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verifica e usa o Variável de ambiente SQLCMDSERVER.  
  
> [!NOTE]  
>  A variável de ambiente OSQLSERVER foi mantida para compatibilidade com versões anteriores. A variável de ambiente SQLCMDSERVER tem precedência sobre a variável de ambiente OSQLSERVER; Isso significa que `sqlcmd` e **osql** podem ser usados próximos um do outro sem interferência e que scripts antigos continuarão a funcionar.  
  
 **-U** _login_id_  
 É a identificação de logon do usuário.  
  
> [!NOTE]  
>  A variável de ambiente OSQLUSER está disponível para compatibilidade com versões anteriores. A variável de ambiente SQLCMDUSER tem precedência em relação à variável de ambiente OSQLUSER. Isso significa que `sqlcmd` e **osql** podem ser usados próximos um do outro sem interferência. Significa também que scripts **osql** existentes continuarão funcionando.  
  
 Se nem o **- U** opção nem a **-P** opção for especificada, `sqlcmd` tenta se conectar usando [!INCLUDE[msCoName](../includes/msconame-md.md)] modo de autenticação do Windows. A autenticação baseia-se na conta do Windows do usuário que está executando o `sqlcmd`.  
  
 Se a opção **-U** for usada com a opção **-E** (descrita adiante neste tópico), uma mensagem de erro será gerada. Se a opção **-U** for seguida de mais de um argumento, uma mensagem de erro será gerada e o programa será encerrado.  
  
 **-z** _new_password_  
 Alterar senha:  
  
 `sqlcmd -U someuser -P s0mep@ssword -z a_new_p@a$$w0rd`  
  
 **-Z** _new_password_  
 Alterar senha e sair:  
  
 `sqlcmd -U someuser -P s0mep@ssword -Z a_new_p@a$$w0rd`  
  
 **Opções de entrada/saída**  
  **-f** _codepage_ | **i:** _codepage_[ **,o:** _codepage_] | **o:** _codepage_[ **,i:** _codepage_]  
 Especifica as páginas de código de entrada e saída. O número da página de código é um valor numérico que especifica um código de página instalada do Windows.  
  
 Regras de conversão de página de código:  
  
-   Se não for especificada nenhuma página de código, o `sqlcmd` usará a página de código atual para arquivos de entrada e de saída, a menos que o arquivo de entrada seja um arquivo Unicode, para o qual não é necessária nenhuma conversão.  
  
-   O `sqlcmd` reconhece automaticamente arquivos de entrada Unicode big-endian e little-endian. Se a opção **-u** tiver sido especificada, a saída sempre será Unicode little endian.  
  
-   Se não for especificado nenhum arquivo de saída, a página de código de saída será a página de código de console. Isso habilita a saída a ser exibida corretamente no console.  
  
-   Assume-se que arquivos de entrada múltiplos tenham a mesma página de código. Arquivos de entrada Unicode e não Unicode podem ser misturados.  
  
 Digite `chcp` no prompt de comando para verificar a página de código de Cmd.exe.  
  
 **-i** _input_file_[ **,** _input_file2_...]  
 Identifica o arquivo que contém um lote de instruções SQL ou procedimentos armazenados. Poderão ser especificados vários arquivos para serem lidos e processados em ordem. Não use espaço entre nomes de arquivos. `sqlcmd` verificará primeiramente se todos os arquivos especificados existem. Se um ou mais arquivos não existirem, o `sqlcmd` será encerrado. As opções -i e Q/-q são mutuamente exclusivas.  
  
 Exemplos de caminho:  
  
 **-i** c:\\< nome do arquivo\>  
  
 **-i** \\\\<Server\>\\<Share$>\\<filename\>  
  
 **-i** "C:\Alguma Pasta\\<nome do arquivo\>"  
  
 Os nomes de caminhos que contêm espaços deverão ficar entre aspas.  
  
 Essa opção pode ser usada mais de uma vez: **-i**_input_file_ **-I**_I input_file_.  
  
 **-o** _output_file_  
 Identifica o arquivo que recebe a saída do `sqlcmd`.  
  
 Se **-u** for especificado, *output_file* será armazenado no formato Unicode. Se o nome do arquivo for inválido, uma mensagem de erro será gerada e o `sqlcmd` será encerrado. O `sqlcmd` não oferece suporte à gravação simultânea de vários processos `sqlcmd` no mesmo arquivo. A saída de arquivo será corrompida ou incorreta. Consulte a opção **-f** para obter mais informações sobre formatos de arquivo. Caso não exista, esse arquivo será criado. Será substituído um arquivo com o mesmo nome de uma sessão `sqlcmd` anterior. O arquivo aqui especificado não é o arquivo **stdout** . Se for especificado um arquivo **stdout** este arquivo não será usado.  
  
 Exemplos de caminho:  
  
 **-o** C:\\< filename>  
  
 **-o** \\\\<Server\>\\<Share$>\\<filename\>  
  
 **-o "** C:\Alguma Pasta\\<nome do arquivo\>"  
  
 Os nomes de caminhos que contêm espaços deverão ficar entre aspas.  
  
 **-r**[**0** | **1**]  
 Redireciona a saída da mensagem de erro para a tela (**stderr**). Se você não especificar um parâmetro ou se especificar **0**, serão redirecionadas somente mensagens de erro com nível de severidade 11 ou acima disso. Se você especificar **1**, serão redirecionadas todas as saídas de mensagens de erro inclusive PRINT. Não tem nenhum efeito se você usar -o. Por padrão, mensagens são envidadas para **stdout**.  
  
 **-R**  
 Faz com que `sqlcmd` localizar numérico, moeda, data e colunas de hora recuperadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com base na localidade do cliente. Por padrão, essas colunas são exibidas usando as configurações regionais do servidor.  
  
 **-u**  
 Especifica se *output_file* é armazenado no formato Unicode, independentemente do formato de *input_file*.  
  
 **Opções de execução de consultas**  
  **-e**  
 Grava scripts de entrada no dispositivo de saída padrão (**stdout**).  
  
 **-I**  
 Define a opção de conexão SET QUOTED_IDENTIFIER como ON. Por padrão, ela é definida como OFF. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).  
  
 **-q"** _cmdline query_ **"**  
 Executa uma consulta quando `sqlcmd` é iniciado, mas não encerra `sqlcmd` quando a consulta for concluída. Podem ser executadas consultas delimitadas por vários ponto e vírgula. Use aspas na consulta, conforme o exemplo a seguir.  
  
 No prompt de comando, digite:  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  Não use o terminador GO na consulta.  
  
 Se for especificado `-b` juntamente com essa opção, `sqlcmd` será encerrado com erro. `-b` é descrita posteriormente neste tópico.  
  
 **-Q"** _cmdline query_ **"**  
 Executa uma consulta quando `sqlcmd` é iniciado e imediatamente encerra `sqlcmd`. Podem ser executadas consultas delimitadas por vários ponto e vírgula.  
  
 Use aspas na consulta, conforme o exemplo a seguir.  
  
 No prompt de comando, digite:  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  Não use o terminador GO na consulta.  
  
 Se for especificado `-b` juntamente com essa opção, `sqlcmd` será encerrado com erro. `-b` é descrita posteriormente neste tópico.  
  
 **-t** _query_timeout_  
 Especifica quanto segundos faltam para que um comando (ou instrução SQL) expire. Essa opção define a `sqlcmd` variável de script SQLCMDSTATTIMEOUT. Se um valor *time_out* não for especificado, o comando não atingirá o tempo limite. O *query**time_out* precisa ser um número entre 1 e 65534. O `sqlcmd` irá gerar uma mensagem de erro se o valor fornecido não for numérico ou não estiver nesse intervalo.  
  
> [!NOTE]  
>  O valor do tempo limite real poderá variar em relação ao valor *time_out* especificado em vários segundos.  
  
 **-vvar =** _value_[ **var =** _value_...]  
 Cria uma `sqlcmd`variável de script que pode ser usado em um `sqlcmd` script. Se o valor contiver espaços, mantenha-o entre aspas. Você pode especificar vários  **_var_** = **" *`values`* "** valores. Se houver erros em quaisquer dos valores especificados, o `sqlcmd` irá gerar uma mensagem de erro e então será encerrado.  
  
 `sqlcmd -v MyVar1=something MyVar2="some thing"`  
  
 `sqlcmd -v MyVar1=something -v MyVar2="some thing"`  
  
 **-x**  
 Faz com que o `sqlcmd` ignore variáveis de script. Isso é útil quando um script contém muitas instruções INSERT que podem conter cadeias de caracteres que têm o mesmo formato de variáveis regulares, como $(*variable_name*).  
  
 **Opções de formatação**  
  **-h** _headers_  
 Especifica o número de linhas a imprimir entre os títulos da coluna. O padrão é imprimir títulos uma vez para cada conjunto de resultados de consulta. Essa opção define a variável de script SQLCMDHEADERS do `sqlcmd`. Use **-1** para especificar que os cabeçalhos não devem ser impressos. Qualquer valor inválido faz com que o `sqlcmd` gere uma mensagem de erro e então seja encerrado.  
  
 **-k** [**1** | **2**]  
 Remove todos os caracteres de controle, como tabulações e caracteres de nova linha, da saída. Isso preserva a formatação de coluna quando os dados são retornados. Se for especificado 1, os caracteres de controle serão substituídos por um único espaço. Se for especificado 2, os caracteres de controle consecutivos serão substituídos por um único espaço. **-k** é igual a **-k1**.  
  
 **-s** _col_separator_  
 Especifica o caractere do separador de coluna. O padrão é um espaço em branco. Essa opção define a variável de script SQLCMDCOLSEP do `sqlcmd`. Para usar caracteres com um significado especial para o sistema operacional como, por exemplo, E comercial (&) ou ponto e vírgula (;), use-os entre aspas ("). O separador de coluna pode ser qualquer caractere de 8 bits.  
  
 **-w** _column_width_  
 Especifica a largura de tela para saída. Essa opção define a variável de script SQLCMDCOLWIDTH do `sqlcmd`. A largura da coluna deve ser um número maior que 8 e menor que 65536. Se a largura da coluna especificada não estiver nesse intervalo, o `sqlcmd` irá gerar uma mensagem de erro. A largura padrão é 80 caracteres. Quando uma linha de saída excede a largura de coluna especificada, ela inclui a próxima linha.  
  
 **-W**  
 Essa opção remove espaços à direita de uma coluna. Use esta opção com a opção **-s** ao preparar dados a serem exportados para outro aplicativo. Ela não pode ser usada com as opções **-y** ou **-Y** .  
  
 **-y** _variable_length_type_display_width_  
 Define a variável de script SQLCMDMAXVARTYPEWIDTH do `sqlcmd`. O padrão é 256. Ele limita o número de caracteres retornados para os tipos de dados com comprimento variável grande:  
  
-   `varchar(max)`  
  
-   `nvarchar(max)`  
  
-   `varbinary(max)`  
  
-   `xml`  
  
-   `UDT (user-defined data types)`  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
> [!NOTE]  
>  UDTs podem ter comprimento fixo dependendo da implementação. Se esse tamanho de UDT de tamanho fixo for mais curto que *display_width*, o valor do UDT retornado não será afetado. Porém, se o tamanho for mais longo que *display_width*, a saída será truncada.  
  
 
> [!IMPORTANT]  
>  Use a opção **-y 0** com muito cuidado, porque isso poderá causar graves problemas de desempenho tanto no servidor quanto na rede, dependendo do tamanho dos dados retornados.  
  
 **-Y** _fixed_length_type_display_width_  
 Define a variável de script SQLCMDMAXFIXEDTYPEWIDTH do `sqlcmd`. O padrão é 0 (ilimitado). Limita o número de caracteres retornado para os tipos de dados a seguir:  
  
-   `char(` *n* `)`, em que 1 < = n < = 8000  
  
-   `nchar(n` *n* `)`, em que 1 < = n < = 4000  
  
-   `varchar(n` *n* `)`, em que 1 < = n < = 8000  
  
-   `nvarchar(n` *n* `)`, em que 1 < = n < = 4000  
  
-   `varbinary(n` *n* `)`, em que 1 < = n < = 4000  
  
-   `variant`  
  
 **Opções de relatório de erros**  
  `-b`  
 Especifica que o `sqlcmd` é encerrado e retorna um valor DOS ERRORLEVEL em caso de erro. O valor que é retornado à variável DOS ERRORLEVEL é **1** quando a mensagem de erro [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiver um nível de severidade maior do que 10; caso contrário, o valor retornado é **0**. Se a opção `-V` tiver sido definida além de `-b`, o `sqlcmd` não relatará um erro se o nível de severidade for inferior aos valores definidos usando `-V`. Arquivos em lote do prompt de comando podem testar o valor de ERRORLEVEL e tratar o erro adequadamente. `sqlcmd` não relata erros para nível de severidade 10 (mensagens informativas).  
  
 Se o script `sqlcmd` tiver um comentário incorreto, erro de sintaxe, ou se estiver faltando uma variável de script, ERRORLEVEL retorna 1.  
  
 **-m** _error_level_  
 Controla quais mensagens de erro são enviadas para **stdout**. Mensagens com um nível de severidade maior ou igual a esse nível são enviadas. Quando esse valor for definido como **-1**, todas as mensagens, incluindo mensagens informativas, serão enviadas. Não são permitidos espaços entre **-m** e **-1**. Por exemplo, **-m-1** é válido, e **-m-1** não.  
  
 Essa opção também define a variável de script SQLCMDERRORLEVEL do `sqlcmd`. Essa variável tem um padrão de 0.  
  
 `-V` *error_severity_level*  
 Controla o nível de severidade usado para definir a variável ERRORLEVEL. Mensagens de erro com níveis de severidade maiores ou iguais a esse valor definem ERRORLEVEL. Valores menores que 0 são reportados como 0. Podem ser usados arquivos de lote e CMD para testar o valor da variável ERRORLEVEL.  
  
 **Opções diversas**  
  **-a** _packet_size_  
 Exige um pacote de tamanho diferente. Essa opção define a variável de script SQLCMDPACKETSIZE do `sqlcmd`. *packet_size* deve ser um valor entre 512 e 32767. O padrão é igual a 4096. Um tamanho de pacote maior pode melhorar o desempenho da execução de scripts que tenham muitas instruções SQL entre comandos GO. Pode-se solicitar um tamanho de pacote maior. Porém, se a solicitação for negada, o `sqlcmd` usará o padrão de servidor para tamanho de pacote.  
  
 **-c** _batch_terminator_  
 Especifica o terminador de lote. Por padrão, comandos são finalizados e enviados para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] digitando-se apenas a palavra "GO" em uma linha. Ao redefinir o terminador de lote, não use palavras-chave reservadas do [!INCLUDE[tsql](../includes/tsql-md.md)] ou caracteres que tenham um significado especial para o sistema operacional, mesmo que sejam precedidas por uma barra invertida.  
  
 **-L**[**c**]  
 Lista os computadores servidor localmente configurados e os nomes dos computadores servidor que estão transmitindo na rede. Esse parâmetro não pode ser usado em combinação com outros parâmetros. O número máximo de computadores servidores que pode ser listado é 3000. Se a lista de servidores ficar truncada devido ao tamanho do buffer, será exibida uma mensagem de aviso.  
  
> [!NOTE]  
>  Devido à natureza da transmissão em redes, `sqlcmd` pode não receber uma resposta oportuna de todos os servidores. Assim, a lista de servidores retornada pode variar para cada invocação dessa opção.  
  
 Se for especificado o parâmetro opcional **c** , a saída aparecerá sem os servidores: linha de cabeçalho e cada linha de servidor será listada sem espaços à esquerda. Isso é chamado de saída normal. A saída normal melhora o desempenho de processamento das linguagens dos scripts.  
  
 **-p**[**1**]  
 Imprime estatísticas de desempenho para cada conjunto de resultados. O exemplo a seguir mostra o formato para estatísticas de desempenho:  
  
 `Network packet size (bytes): n`  
  
 `x xact[s]:`  
  
 `Clock Time (ms.): total       t1  avg       t2 (t3 xacts per sec.)`  
  
 Onde:  
  
 `x` = Número de transações processadas pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 `t1` = Tempo total para todas as transações.  
  
 `t2` = Tempo médio de uma única transação.  
  
 `t3` = Número médio de transações por segundo.  
  
 Todos os tempos estão em milissegundos.  
  
 Se o parâmetro opcional **1** for especificado, o formato de saída das estatísticas estará em formato separado por dois pontos, que poderá ser facilmente importado para uma planilha ou processado por um script.  
  
 Se o parâmetro opcional for qualquer valor diferente de **1**, um erro será gerado e `sqlcmd` é encerrado.  
  
 `-X`[**1**]  
 Desabilita comandos que podem comprometer a segurança do sistema quando o `sqlcmd` é executado a partir de um arquivo em lote. Os comandos desabilitados ainda são reconhecidos; o `sqlcmd` emite uma mensagem de aviso e continua. Se o parâmetro opcional **1** for especificado, `sqlcmd` gera uma mensagem de erro e, em seguida, sai. Os comandos a seguir são desabilitados quando for usada a opção `-X`:  
  
-   **ED**  
  
-   **!!** _command_  
  
 Se for especificada a opção `-X`, isso evita que variáveis de ambiente sejam transmitidas para o `sqlcmd`. Evita também que o script de inicialização especificado, usando a variável de script SQLCMDINI, seja executado. Para obter mais informações sobre `sqlcmd` variáveis de script, consulte [usar sqlcmd com variáveis de script](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
 **-?**  
 Exibe o resumo de sintaxe de opções do `sqlcmd`.  
  
## <a name="remarks"></a>Comentários  
 As opções não precisam ser usadas na ordem mostrada na seção de sintaxe.  
  
 Quando são retornados vários resultados, o `sqlcmd` imprime uma linha em branco entre cada conjunto de resultados em um lote. Além disso, o "\<x > linhas afetadas" mensagem não aparece quando não se aplica à instrução executada.  
  
 Para usar `sqlcmd` interativamente, digite `sqlcmd` no prompt de comando com uma ou mais das opções descritas anteriormente neste tópico. Para obter mais informações, consulte [Usar o Utilitário sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
> [!NOTE]  
>  As opções **-L**, **-Q**, **-Z** ou **-i** causar `sqlcmd` seja encerrado após execução.  
  
 O comprimento total da linha de comando `sqlcmd` no ambiente de comando (Cmd.exe), incluindo todos os argumentos e variáveis expandidas, é aquele determinado pelo sistema operacional para Cmd.exe.  
  
## <a name="variable-precedence-low-to-high"></a>Precedência de variável (baixa para alta)  
  
1.  Variáveis ambientais do nível de sistema.  
  
2.  Variáveis ambientais do nível de usuário.  
  
3.  Shell de comando (**definir** X = Y) definido no prompt de comando antes de executar `sqlcmd`.  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  Para exibir as variáveis ambientais, no **Painel de Controle**, abra **Sistema**e clique na guia **Avançado** .  
  
## <a name="sqlcmd-scripting-variables"></a>Variáveis de script do sqlcmd  
  
|Variável|Opção relacionada|R/W|Padrão|  
|--------------|--------------------|----------|-------------|  
|SQLCMDUSER|-U|R|""|  
|SQLCMDPASSWORD|-P|--|""|  
|SQLCMDSERVER|-S|R|"DefaultLocalInstance"|  
|SQLCMDWORKSTATION|-H|R|"ComputerName"|  
|SQLCMDDBNAME|-d|R|""|  
|SQLCMDLOGINTIMEOUT|-l|R/W|"8" (segundos)|  
|SQLCMDSTATTIMEOUT|-T|R/W|"0" = espere indefinidamente|  
|SQLCMDHEADERS|-H|R/W|"0"|  
|SQLCMDCOLSEP|-S|R/W|" "|  
|SQLCMDCOLWIDTH|-w|R/W|"0"|  
|SQLCMDPACKETSIZE|-A|R|"4096"|  
|SQLCMDERRORLEVEL|-M|R/W|0|  
|SQLCMDMAXVARTYPEWIDTH|-y|R/W|"256"|  
|SQLCMDMAXFIXEDTYPEWIDTH|-y|R/W|"0" = ilimitado|  
|SQLCMDEDITOR||R/W|"edit.com"|  
|SQLCMDINI||R|""|  
  
 SQLCMDUSER, SQLCMDPASSWORD e SQLCMDSERVER são definidos quando **:Connect**  
  
 é usado.  
  
 R indica que o valor pode ser definido apenas uma vez durante a inicialização do programa.  
  
 R/W indica que o valor pode ser modificado com o comando **setvar** e que os próximos comandos serão influenciados pelo novo valor.  
  
## <a name="sqlcmd-commands"></a>Comandos sqlcmd  
 Além das instruções do [!INCLUDE[tsql](../includes/tsql-md.md)] no `sqlcmd`, também estão disponíveis os comandos a seguir:  
  
|||  
|-|-|  
|**GO** [*count*]|**:List**|  
|[ **:** ] **RESET**|**:Error**|  
|[ **:** ] **ED**|**:Out**|  
|[ **:** ] **!!**|**:Perftrace**|  
|[ **:** ] **QUIT**|**:Connect**|  
|[ **:** ] **EXIT**|**:On Error**|  
|**:r**|**:Help**|  
|**:ServerList**|**:XML** [**ON** &#124; **OFF**]|  
|**:Setvar**|**:Listvar**|  
  
 Lembre-se do seguinte ao usar comandos do `sqlcmd`:  
  
-   Todos os comandos do `sqlcmd`, exceto GO, devem ser antecedidos de dois pontos (:).  
  
    > [!IMPORTANT]  
    >  Para manter a compatibilidade com versões anteriores de scripts **osql** existentes, alguns dos comandos serão reconhecidos sem os dois-pontos. Isso é indicado pelo [ **:** ].  
  
-   Os comandos do `sqlcmd` serão reconhecidos apenas se aparecerem no início de uma linha.  
  
-   Todos os comandos do `sqlcmd` não diferenciam maiúsculas de minúsculas.  
  
-   Cada comando deve estar em uma linha separada. Um comando não pode ser seguido por uma instrução do [!INCLUDE[tsql](../includes/tsql-md.md)] ou por outro comando.  
  
-   Comandos são executados imediatamente. Eles não são colocados no buffer de execução como as instruções [!INCLUDE[tsql](../includes/tsql-md.md)] .  
  
 **Comandos de Edição**  
  [ **:** ] **ED**  
 Inicie o editor de textos. Esse editor pode ser usado para editar o lote atual do [!INCLUDE[tsql](../includes/tsql-md.md)] ou o último lote executado. Para editar o último lote executado, o comando **ED** deve ser digitado imediatamente depois da execução do último lote.  
  
 O editor de textos é definido pela variável de ambiente SQLCMDEDITOR. O editor padrão é 'Editar.' Para alterar o editor, defina a variável de ambiente SQLCMDEDITOR. Por exemplo, para definir o editor como [!INCLUDE[msCoName](../includes/msconame-md.md)] Notepad, no prompt de comando, digite:  
  
 `SET SQLCMDEDITOR=notepad`  
  
 [ **:** ] **RESET**  
 Desmarca o cache de instruções.  
  
 **:List**  
 Imprime o conteúdo do cache de instrução.  
  
 **Variáveis**  
  **:Setvar** \<**var**> [ **" *`value`* "** ]  
 Define as variáveis de script do `sqlcmd`. Variáveis de script têm o seguinte formato: `$(VARNAME)`.  
  
 Nomes de variáveis não diferenciam maiúsculas de minúsculas.  
  
 Variáveis de script podem ser definidas da seguinte forma:  
  
-   Usando-se implicitamente uma opção de linha de comando. Por exemplo, o **-l** opção define a SQLCMDLOGINTIMEOUT `sqlcmd` variável.  
  
-   Explicitamente, usando o comando **:Setvar** .  
  
-   Definindo uma variável de ambiente antes de executar o `sqlcmd`.  
  
> [!NOTE]  
>  A opção `-X` evita que variáveis de ambiente sejam passadas para o `sqlcmd`.  
  
 Se uma variável definida com **:Setvar** e uma variável de ambiente tiverem o mesmo nome, a variável definida com **:Setvar** terá precedência.  
  
 Nomes de variáveis não devem conter caracteres de espaço em branco.  
  
 Nomes de variáveis não podem ter a mesma forma que uma expressão variável, como $ (var).  
  
 Se o valor da cadeia de caracteres da variável de script tiver espaços em branco, use aspas. Se não for especificado um valor para uma variável de script, a variável de script será descartada.  
  
 **:Listvar**  
 Exibe uma lista das variáveis de script definidas atualmente.  
  
> [!NOTE]  
>  Somente variáveis que são definidas por de script `sqlcmd`e aquelas definidas usando o **: Setvar** comando será exibido.  
  
 **Comandos de Saída**  
  **:Error**   
 ** _\<_ ** _filename_  ** _>|_ STDERR|STDOUT**  
 Redireciona toda a saída de erro para o arquivo especificado por *nome do arquivo*para **stderr** ou **stdout**. O comando **Error** pode aparecer várias vezes em um script. Por padrão, saída de erro é enviada para **stderr**.  
  
 *nome do arquivo*  
 Cria e abre um arquivo que receberá a saída. Se o arquivo já existir, será truncado para zero bytes. Se o arquivo não estiver disponível devido a permissões ou outras razões, a saída não será alternada e será enviada ao último destino especificado ou ao destino padrão.  
  
 **STDERR**  
 Muda a saída de erro para o fluxo **stderr** . Se houver redirecionamento, o destino para o qual o fluxo foi redirecionado receberá a saída de erro.  
  
 **STDOUT**  
 Muda a saída de erro para o fluxo **stdout** . Se houver redirecionamento, o destino para o qual o fluxo foi redirecionado receberá a saída de erro.  
  
 **:Out \<** _filename_ **>** | **STDERR**| **STDOUT**  
 Cria e redireciona todos os resultados da consulta para o arquivo especificado por *nome do arquivo*para **stderr** ou **stdout**. Por padrão, a saída é enviada para **stdout**. Se o arquivo já existir, será truncado para zero bytes. O comando **Out** pode aparecer várias vezes em um script.  
  
 **:Perftrace \<** _filename_ **>** | **STDERR**| **STDOUT**  
 Cria e redireciona todas as informações de rastreamento de desempenho para o arquivo especificado por *nome do arquivo*para **stderr** ou **stdout**. Por padrão a saída de rastreamento de desempenho é enviada para **stdout**. Se o arquivo já existir, será truncado para zero bytes. O comando **Perftrace** pode aparecer várias vezes em um script.  
  
 **Comandos de controle de execução**  
  **:On Error**[ `exit` | `ignore`]  
 Define a ação a ser executada no caso de um erro durante a execução de script ou em lote.  
  
 Quando a opção `exit` é usada, o `sqlcmd` é fechado com o valor de erro adequado.  
  
 Quando é usada a opção `ignore`, o `sqlcmd` ignora o erro e continua executando o lote ou script. Por padrão, será impressa uma mensagem de erro.  
  
 [ **:** ] **QUIT**  
 Faz com que o `sqlcmd` seja encerrado.  
  
 [ **:** ] **EXIT**[ **( *`statement`* )** ]  
 Permite usar o resultado de uma instrução SELECT como o valor de retorno do `sqlcmd`. Se numérico, a primeira coluna da última linha do resultado será convertida em um inteiro de 4 bytes (longo). O MS-DOS transmite o byte baixo para o processo pai ou nível de erro do sistema operacional. O Windows 200x passa todo o número inteiro de 4 bytes. A sintaxe é:  
  
 `:EXIT(query)`  
  
 Por exemplo:  
  
 `:EXIT(SELECT @@ROWCOUNT)`  
  
 É possível incluir também o parâmetro **EXIT** como parte de um arquivo em lote. Por exemplo, no prompt de comando, digite:  
  
 `sqlcmd -Q "EXIT(SELECT COUNT(*) FROM '%1')"`  
  
 O `sqlcmd` utilitário envia tudo entre os parênteses **()** para o servidor. Se um procedimento armazenado de sistema selecionar um conjunto e retornar um valor, somente a seleção será retornada. A instrução EXIT **()** sem nada entre os parênteses executa tudo antes dela no lote e é fechada sem um valor de retorno.  
  
 Quando é especificada uma consulta incorreta, o `sqlcmd` é encerrado sem um valor de retorno.  
  
 Eis uma lista de formatos EXIT:  
  
-   :EXIT  
  
 Não executa o lote e então sai imediatamente e não retorna valor algum.  
  
-   :EXIT( )  
  
 Executa o lote e então sai imediatamente e não retorna valor algum.  
  
-   :EXIT(query)  
  
 Executa o lote que inclui a consulta, e então sai depois de retornar os resultados da consulta.  
  
 Se for usado RAISERROR em um `sqlcmd` é gerado o script e um estado 127, `sqlcmd` sairá e retornará a ID da mensagem para o cliente. Por exemplo:  
  
 `RAISERROR(50001, 10, 127)`  
  
 Esse erro fará com que o script do `sqlcmd` seja encerrado e retorne a ID de mensagem 50001 ao cliente.  
  
 Os valores de retorno -1 a -99 são reservados pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]; `sqlcmd` define os seguintes valores de retorno adicionais:  
  
|Valores de retorno|Descrição|  
|-------------------|-----------------|  
|-100|Erro encontrado antes da seleção do valor de retorno.|  
|-101|Nenhuma linha encontrada ao se selecionar o valor de retorno.|  
|-102|Erro de conversão ao selecionar valor de retorno.|  
  
 **GO** [*count*]  
 GO sinaliza tanto o término de um lote quanto a execução de qualquer instrução de cachê do [!INCLUDE[tsql](../includes/tsql-md.md)]. Ao especificar um valor para *count*, serão executadas as instruções de cache *count* vezes, como um único lote.  
  
 **Comandos diversos**  
  **:r \<** _filename_ **>**  
 Analisa adicionais [!INCLUDE[tsql](../includes/tsql-md.md)] instruções e `sqlcmd` comandos do arquivo especificado por **< *`filename`* >** no cache de instrução.  
  
 Se o arquivo contiver instruções [!INCLUDE[tsql](../includes/tsql-md.md)] que não são seguidas por **GO**, digite **GO** na linha que segue **:r**.  
  
> [!NOTE]  
>  **\<** _nome do arquivo_ **>** é lido em relação ao diretório de inicialização no qual `sqlcmd` foi executado.  
  
 O arquivo será lido e executado depois que for encontrado um terminador de lote. Podem ser emitidos vários comandos **:r** . O arquivo pode incluir qualquer comando `sqlcmd`. Isso inclui o terminador de lote **GO**.  
  
> [!NOTE]  
>  A contagem de linha que é exibida em modo interativo será aumentada em um para cada comando **:r** encontrado. O comando **:r** aparecerá na saída do comando de lista.  
  
 **:Serverlist**  
 Lista os servidores configurados localmente e os nomes dos servidores que estão transmitindo na rede.  
  
 **:Connect** _server_name_[ **\\** _instance_name_] [-l *timeout*] [-U *user_name* [-P *password*]]  
 Conecta-se a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Além disso fecha a conexão atual.  
  
 Opções de tempo limite:  
  
|||  
|-|-|  
|0|esperar|  
|n>0|esperar por n segundos|  
  
 A variável de script SQLCMDSERVER refletirá a conexão ativa atual.  
  
 Se não for especificado *timeout* , o valor da variável SQLCMDLOGINTIMEOUT será o padrão.  
  
 Se apenas *user_name* for especificado (como uma opção ou variável de ambiente), será solicitado que o usuário insira uma senha. Isso não ocorre se as variáveis de ambiente SQLCMDUSER ou SQLCMDPASSWORD tiverem sido definidas. Se as opções e as variáveis de ambiente não forem fornecidas, o modo de Autenticação do Windows será usado para fazer logon. Por exemplo, para conectar-se a uma instância, `instance1`, do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], `myserver`, usando segurança integrada você usaria o seguinte:  
  
 `:connect myserver\instance1`  
  
 Para conectar-se à instância padrão do `myserver` usando variáveis de script, você usaria o seguinte:  
  
 `:setvar myusername test`  
  
 `:setvar myservername myserver`  
  
 `:connect $(myservername) $(myusername)`  
  
 [ **:** ] **!!** \< *command*>  
 Executa comandos de sistema operacional. Para executar um comando do sistema operacional, inicie uma linha com dois pontos de exclamação ( **!!** ) seguida do comando do sistema operacional. Por exemplo:  
  
 `:!! Dir`  
  
> [!NOTE]  
>  O comando é executado no computador no qual o `sqlcmd` está sendo executado.  
  
 **:XML** [**ON** | **OFF**]  
 Para obter mais informações, consulte "XML Output Format", posteriormente neste tópico.  
  
 **:Help**  
 Lista comandos do `sqlcmd` juntamente com uma breve descrição de cada comando.  
  
### <a name="sqlcmd-file-names"></a>Nomes de arquivos sqlcmd  
 `sqlcmd` arquivos de entrada podem ser especificados com o **-i** opção ou o **: r** comando. Arquivos de saída podem ser especificados com a opção **-o** ou os comandos **:Error**, **:Out** e **:Perftrace** . A seguir algumas diretrizes sobre como trabalhar com esses arquivos:  
  
-   **: Error**, **: Out** e **: Perftrace** devem usar separado **< *`filename`* >** . Se o mesmo **< *`filename`* >** é usado, entradas dos comandos poderão ser misturadas.  
  
-   Se for chamado um arquivo de entrada em um servidor remoto do `sqlcmd` em um computador local e o arquivo tiver um caminho de arquivo de unidade como: c:\OutputFile.txt. O arquivo de saída será criado no computador local e não no servidor remoto.  
  
-   Caminhos de arquivo válidos incluem: C:\\ **< *`filename`* >** , \\ \\< servidor\>\\< Share$ >\\ **< *`filename`* >** e "C:\Some pasta\\  **< *`file name`* >** ". Se houver um espaço no caminho, use aspas.  
  
-   Cada nova sessão do `sqlcmd` substituirá arquivos existentes que tenham os mesmos nomes.  
  
### <a name="informational-messages"></a>Mensagens informativas  
 O `sqlcmd` imprime qualquer mensagem informativa enviada pelo servidor. No exemplo a seguir, depois que as instruções do [!INCLUDE[tsql](../includes/tsql-md.md)] são executadas, é impressa uma mensagem informativa.  
  
 No prompt de comando, digite o seguinte:  
  
 `sqlcmd`  
  
 `At the sqlcmd prompt type:`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 Quando você pressiona ENTER, a seguinte mensagem informativa é impresso: "Contexto de banco de dados alterado para 'AdventureWorks2012'".  
  
### <a name="output-format-from-transact-sql-queries"></a>Formato de saída do Transact-SQL Queries  
 O `sqlcmd` imprime, em primeiro lugar, um cabeçalho de coluna com os nomes de coluna especificados na lista de seleção. Os nomes de coluna são separados usando-se o caractere SQLCMDCOLSEP. Por padrão, esse é um espaço. Se o nome de coluna for mais curto do que a largura de coluna, a saída será preenchida com espaços até a coluna seguinte.  
  
 Essa linha será seguida por uma linha divisória formada por uma série de tracejados. A saída a seguir mostra um exemplo.  
  
 Inicie o `sqlcmd`. No prompt de comando do `sqlcmd`, digite o seguinte:  
  
 `USE AdventureWorks2012;`  
  
 `SELECT TOP (2) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 Quando você pressiona Enter, o seguinte conjunto de resultados é retornado.  
  
 `BusinessEntityID FirstName    LastName`  
  
 `---------------- ------------ ----------`  
  
 `285              Syed         Abbas`  
  
 `293              Catherine    Abel`  
  
 `(2 row(s) affected)`  
  
 Embora a coluna `BusinessEntityID` tenha apenas 4 caracteres de largura, ela foi expandida para acomodar o nome de coluna mais longo. Por padrão, a saída é finalizada com 80 caracteres. Isso pode ser alterado com a opção **-w** ou com a definição da variável de script SQLCMDCOLWIDTH.  
  
### <a name="xml-output-format"></a>Formato de saída XML  
 Saída XML é o resultado de uma cláusula FOR XML, não formatada, em um fluxo contínuo.  
  
 Quando você esperar uma saída XML, use o seguinte comando: `:XML ON`.  
  
> [!NOTE]  
>  O `sqlcmd` retorna mensagens de erro no formato habitual. Observe que as mensagens de erro também são produzidas no fluxo de texto XML em formato XML. Usando `:XML ON`, o `sqlcmd` não exibe mensagens informativas.  
  
 Para definir XML em modo off, use o seguinte comando: `:XML OFF`.  
  
 O comando GO não deve aparecer antes de o comando XML OFF ser emitido porque o comando XML OFF retorna o `sqlcmd` para a saída orientada por linhas.  
  
 Dados XML (em fluxo) e dados de conjunto de linhas não podem ser misturados. Se o comando XML ON não tiver sido emitido antes da execução de uma instrução do [!INCLUDE[tsql](../includes/tsql-md.md)] que gera protocolos XML, a saída será adulterada. Se o comando XML ON tiver sido emitido, não será possível executar instruções do [!INCLUDE[tsql](../includes/tsql-md.md)] que gerem conjuntos de linhas normais.  
  
> [!NOTE]  
>  O comando **:XML** não oferece suporte para a instrução SET STATISTICS XML.  
  
## <a name="sqlcmd-best-practices"></a>Práticas recomendadas sqlcmd  
 Use as seguintes práticas para ajudar a maximizar a segurança e a eficiência.  
  
-   Use segurança integrada.  
  
-   Use `-X` em ambientes automatizados.  
  
-   Proteja arquivos de entrada e de saída usando permissões adequadas de sistema de arquivos NTFS.  
  
-   Para aumentar o desempenho, faça o máximo possível em uma sessão `sqlcmd`, em vez de usar uma série de sessões.  
  
-   Defina valores mais altos de tempo limite para execução em lote ou de consulta do que você imagina que levará para a execução em lote ou de consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o utilitário sqlcmd](../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [Executar arquivos de script Transact-SQL usando sqlcmd](../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)   
 [Usar o utilitário sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [Usar sqlcmd com variáveis de script](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [Conectar-se ao mecanismo de banco de dados com sqlcmd](../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)   
 [Editar scripts SQLCMD com o Editor de Consultas](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [Gerenciar etapas de trabalho](../ssms/agent/manage-job-steps.md)   
 [Criar uma etapa de trabalho CmdExec](../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
