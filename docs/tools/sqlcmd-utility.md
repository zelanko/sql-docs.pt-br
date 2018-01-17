---
title: "Utilitário Sqlcmd | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: sqlcmd
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "155"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 44464415177cffc2e09c5218ecd9440801be7d96
ms.sourcegitcommit: 0c6d858a507bd38b9b06eb7676736de5d38a1c87
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="sqlcmd-utility"></a>sqlcmd Utility
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

 > Para SQL Server 2014 e inferior, consulte [utilitário sqlcmd](https://msdn.microsoft.com/en-US/library/ms162773(SQL.120).aspx).


  O **sqlcmd** utilitário permite que você insira instruções Transact-SQL, procedimentos do sistema e arquivos de script no prompt de comando, em **Editor de consultas** no modo SQLCMD, em um arquivo de script do Windows ou em uma etapa de trabalho do sistema operacional (Cmd.exe) de um trabalho do SQL Server Agent. Esse utilitário usa ODBC para executar lotes Transact-SQL. 
  
> [!NOTE]
> As versões mais recentes do utilitário sqlcmd estão disponíveis como uma versão da Web no [Centro de Download](http://go.microsoft.com/fwlink/?LinkID=825643). Você precisa de versão 13,1 ou superior para dar suporte ao sempre criptografado (`-g`) e autenticação do Active Directory do Azure (`-G`). (Você poderá ter várias versões do sqlcmd.exe instaladas no computador. Verifique se você está usando a versão correta. Para determinar a versão, execute `sqlcmd -?`.)

Você pode tentar o utilitário sqlcmd do Shell de nuvem do Azure, pois ele já está instalado por padrão: [ ![inicie o Shell de nuvem](https://shell.azure.com/images/launchcloudshell.png "inicie o Shell de nuvem")](https://shell.azure.com)

  Para executar instruções sqlcmd no SSMS, selecione o Modo SQLCMD na lista suspensa Menu de Consulta do painel de navegação superior.  
  
> [!IMPORTANT] 
> [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)](SSMS) usa o Microsoft [!INCLUDE[dnprdnshort_md](../includes/dnprdnshort-md.md)] SqlClient para execução em regular e o modo SQLCMD na **Editor de consultas**. Quando o **sqlcmd** é executado na linha de comando, o **sqlcmd** usa o driver ODBC. Devido às diferentes opções padrão que podem ser aplicadas, é possível observar um comportamento diferente ao executar a mesma consulta no [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] no Modo SQLCMD e no utilitário **sqlcmd** .  
>   
  
 Atualmente, o **sqlcmd** não requer um espaço entre a opção de linha de comando e o valor. Porém, em uma versão futura, um espaço pode ser necessário entre a opção de linha de comando e o valor.  
 
 Outros tópicos:
- [Iniciar o utilitário sqlcmd](../relational-databases/scripting/sqlcmd-start-the-utility.md)   
-  [Usar o utilitário sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md)   
  
## <a name="syntax"></a>Sintaxe  
  
```  
sqlcmd   
   -a packet_size  
   -A (dedicated administrator connection)  
   -b (terminate batch job if there is an error)  
   -c batch_terminator  
   -C (trust the server certificate)  
   -d db_name  
   -e (echo input)  
   -E (use trusted connection)  
   -f codepage | i:codepage[,o:codepage] | o:codepage[,i:codepage] 
   -g (enable column encryption) 
   -G (use Azure Active Directory for authentication)
   -h rows_per_header  
   -H workstation_name  
   -i input_file  
   -I (enable quoted identifiers)  
   -j (Print raw error messages)
   -k[1 | 2] (remove or replace control characters)  
   -K application_intent  
   -l login_timeout  
   -L[c] (list servers, optional clean output)  
   -m error_level  
   -M multisubnet_failover  
   -N (encrypt connection)  
   -o output_file  
   -p[1] (print statistics, optional colon format)  
   -P password  
   -q "cmdline query"  
   -Q "cmdline query" (and exit)  
   -r[0 | 1] (msgs to stderr)  
   -R (use client regional settings)  
   -s col_separator  
   -S [protocol:]server[instance_name][,port]  
   -t query_timeout  
   -u (unicode output file)  
   -U login_id  
   -v var = "value"  
   -V error_severity_level  
   -w column_width  
   -W (remove trailing spaces)  
   -x (disable variable substitution)  
   -X[1] (disable commands, startup script, environment variables, optional exit)  
   -y variable_length_type_display_width  
   -Y fixed_length_type_display_width  
   -z new_password   
   -Z new_password (and exit)  
   -? (usage)  
```  
  
## <a name="command-line-options"></a>Opções de linha de comando  
 **Opções relacionadas a logon**  
  **-A**  
 Logs no SQL Server com uma Conexão de administrador dedicada (DAC). Esse tipo de conexão é usado para solucionar um problema no servidor. Isso funcionará apenas com computadores servidor que oferecem suporte para DAC. Se a DAC não estiver disponível, o **sqlcmd** vai gerar uma mensagem de erro e será encerrado. Para obter mais informações sobre a DAC, consulte [Conexão de diagnóstico para administradores de banco de dados](../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md). Não há suporte para a opção - A com a opção -G. Ao se conectar ao banco de dados SQL usando - A, você deve ser um administrador do SQL server. A DAC não está disponível para um administrador do Active Directory do Azure.
  
 **-C**  
 Essa opção é usada pelo cliente para configurá-lo para confiar implicitamente no certificado do servidor sem validação. Essa opção é equivalente à opção `TRUSTSERVERCERTIFICATE = true`do ADO.NET.  
  
 **-d** *db_name*  
 Emite uma instrução `USE` *db_name* ao iniciar o **sqlcmd**. Essa opção define a variável de script SQLCMDDBNAME do **sqlcmd** . Isso especifica o banco de dados inicial. O padrão é a propriedade do banco de dados padrão de seu logon. Se o banco de dados não existir, será gerada uma mensagem de erro e o **sqlcmd** será encerrado.  
  
 **-l** *login_timeout*  
 Especifica o número de segundos antes que um logon do **sqlcmd** no driver ODBC expire quando você tentar se conectar a um servidor. Essa opção define a variável de script SQLCMDLOGINTIMEOUT do **sqlcmd** . O tempo limite padrão de logon do **sqlcmd** é de oito segundos. Ao usar a opção **- G** para se conectar ao Banco de Dados SQL ou o SQL Data Warehouse e autenticar usando o Azure Active Directory, é recomendado estipular um valor de tempo limite de pelo menos 30 segundos. O tempo limite do logon deve ser um número entre 0 e 65534. Se o valor fornecido não for numérico ou se não estiver nesse intervalo, o **sqlcmd** vai gerar uma mensagem de erro. Um valor de 0 especifica o tempo limite como infinito.
  
 **-E**  
 Usa uma conexão confiável em vez de usar um nome de usuário e senha para fazer logon no SQL Server. Por padrão, sem a especificação de **-E** , o **sqlcmd** usa a opção de conexão confiável.  
  
 A opção **-E** ignora possíveis definições de variável de ambiente de nome de usuário e senha como SQLCMDPASSWORD. Se a opção **-E** for usada com as opções **-U** ou **-P** , uma mensagem de erro será gerada.  

**-g**  
Define a Configuração de Criptografia de Coluna como `Enabled`. Para obter mais informações, consulte [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md). Há suporte apenas para as chaves mestras armazenadas no Repositório de Certificados do Windows. A opção -g exige, no mínimo, a versão **13.1** do [sqlcmd](http://go.microsoft.com/fwlink/?LinkID=825643). Para determinar a versão, execute `sqlcmd -?`.

 **-G**  
 Essa opção é usada pelo cliente ao se conectar ao Banco de Dados SQL ou o SQL Data Warehouse para especificar que o usuário seja autenticado usando a autenticação do Azure Active Directory. Essa opção define a variável de script SQLCMDUSEAAD do **sqlcmd** = true. A opção -G exige, no mínimo, a versão **13.1** do [sqlcmd](http://go.microsoft.com/fwlink/?LinkID=825643). Para determinar a versão, execute `sqlcmd -?`. Para obter mais informações, consulte [Conectando-se ao Banco de Dados SQL ou ao SQL Data Warehouse usando a Autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). Não há suporte para a opção - A com a opção -G.

> [!IMPORTANT]
> A opção **- G** só se aplica ao Banco de Dados SQL e ao Azure Data Warehouse. 

- **Nome de usuário do Azure Active Directory e senha:** 

    Quando desejar usar um nome de usuário do Azure Active Directory e uma senha, você poderá fornecer a opção **- G** e também usar o nome de usuário e a senha fornecendo as opções **-U** e **-P** .
    ``` 
    Sqlcmd -S testsrv.database.windows.net -d Target_DB_or_DW -U bob@contoso.com -P MyAADPassword -G 
    ``` 
    Isso gerará a seguinte cadeia de conexão no back-end: 

    ```
     SERVER = Target_DB_or_DW.testsrv.database.windows.net;UID= bob@contoso.com;PWD=MyAADPassword;AUTHENTICATION = ActiveDirectoryPassword 
    ```

- **Integração ao Azure Active Directory** 
 
   Para a autenticação Integrada do Azure Active Directory, forneça a opção **-G** sem um nome de usuário e uma senha: 

    ```
    Sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G
    ```  

    Isso gerará a seguinte cadeia de conexão no back-end: 

    ```
    SERVER = Target_DB_or_DW.testsrv.database.windows.net Authentication = ActiveDirectoryIntegrated; Trusted_Connection=NO
    ``` 

    > [!NOTE] 
    > A opção -E (Trusted_Connection) não pode ser usada junto com a opção -G.

    
 **-H** *workstation_name*  
 Um nome de estação de trabalho. Essa opção define a variável de script SQLCMDWORKSTATION do **sqlcmd** . O nome da estação de trabalho é listado na coluna **hostname** da exibição de catálogo **sys.sysprocesses** e pode ser retornado usando o procedimento armazenado **sp_who**. Se essa opção não for especificada, o padrão será o nome do computador atual. Esse nome pode ser usado para identificar diferentes sessões do **sqlcmd** .  


**-j** Imprime mensagens de erro bruto na tela.
  
 **-K** *application_intent*  
 Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. O único valor com suporte no momento é **ReadOnly**. Se **-K** não for especificado, o utilitário sqlcmd não dará suporte à conectividade com uma réplica secundária em um grupo de disponibilidade AlwaysOn. Para obter mais informações, consulte [Secundárias ativas: Réplicas secundárias legíveis (Grupos de Disponibilidade AlwaysOn)](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)  
  
 **-M** *multisubnet_failover*  
 Sempre especifique **- M** ao conectar-se ao ouvinte do grupo de disponibilidade de um grupo de disponibilidade do SQL Server ou uma instância de Cluster de Failover do SQL Server. **-M** proporciona maior rapidez na detecção do servidor (atualmente) ativo e na conexão a ele. Se **-M** não for especificado, **-M** estará desativado. Para obter mais informações sobre [! INCLUIR[ssHADR](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [criação e configuração de grupos de disponibilidade &#40; SQL Server &#41; ](../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clustering de Failover e grupos de disponibilidade AlwaysOn (SQL Server)] (https://msdn.microsoft.comlibrary/ff929171.aspx, e [secundárias ativas: réplicas secundárias legíveis (sempre em grupos de disponibilidade)](https://msdn.microsoft.com/library/ff878253.aspx.  
  
 **-N**  
 Essa opção é usada pelo cliente para solicitar uma conexão criptografada.  
  
 **-P** *password*  
 É uma senha especificada pelo usuário. Senhas diferenciam maiúsculas e minúsculas. Se a opção -U for usada e a opção **-P** não for usada, e a variável de ambiente SQLCMDPASSWORD não tiver sido definida, o **sqlcmd** solicitará uma senha ao usuário. Para especificar uma senha nula (não recomendável), use **-P ""**. E lembre-se sempre:
 
#### <a name="use-a-strong-passwordhttpsmsdnmicrosoftcomlibraryms161962sql130aspx"></a>[**Use uma senha forte!!**](https://msdn.microsoft.com/library/ms161962(SQL.130).aspx)
  
  
 A solicitação de senha é exibida no console, como a seguir: `Password:`  
  
 A entrada do usuário está oculta. Isso significa que nada é exibido e o cursor fica em posição.  
  
 A variável de ambiente SQLCMDPASSWORD lhe permite definir uma senha padrão para a sessão atual. Assim, senhas não têm de ser hard-coded em arquivos em lote.  
  
 O exemplo a seguir define, em primeiro lugar, a variável SQLCMDPASSWORD no prompt de comando e acessa o utilitário **sqlcmd** . No prompt de comando, digite:  
  
 `SET SQLCMDPASSWORD= p@a$$w0rd`  
 No prompt de comando a seguir, digite:  
  
 `sqlcmd`  
  
 Se a combinação de nome de usuário e senha estiver incorreta, uma mensagem de erro será gerada.  
  
**OBSERVAÇÃO!**  A variável de ambiente OSQLPASSWORD foi mantida para compatibilidade com versões anteriores. A variável de ambiente SQLCMDPASSWORD tem precedência em relação à variável de ambiente OSQLPASSWORD; isso significa que **sqlcmd** e **osql** podem ser usados próximos um do outro sem interferência e que scripts antigos continuarão funcionado.  
  
 Será gerada uma mensagem de erro se a opção **-P** for usada com a opção **-E** .  
  
 Se a opção **-P** for seguida de mais de um argumento, uma mensagem de erro será gerada e o programa será fechado.  
  
 **-S** [*protocol*:]*server*[**\\***instance_name*][**,***port*]  
 Especifica a instância do SQL Server ao qual se conectar. Define a variável de script SQLCMDSERVER do **sqlcmd** .  
  
 Especifique *nome_do_servidor* para se conectar à instância padrão do SQL Server no computador servidor. Especifique *nome_do_servidor* [**\\* nome_da_instância* ] para se conectar a uma instância nomeada do SQL Server no computador servidor. Se nenhum servidor for especificado, **sqlcmd** se conecta à instância padrão do SQL Server no computador local. Essa opção é necessária quando você executa o **sqlcmd** em um computador remoto na rede.  
  
 O*protocolo* pode ser **tcp** (TCP/IP), **lpc** (memória compartilhada) ou **np** (pipes nomeados).  
  
 Se você não especificar um *nome_do_servidor* [**\\* nome_da_instância* ] ao iniciar **sqlcmd**, SQL Server verifica e usa o ambiente SQLCMDSERVER variável.  
  
> [!NOTE]  
>  A variável de ambiente OSQLSERVER foi mantida para compatibilidade com versões anteriores. A variável de ambiente SQLCMDSERVER tem precedência em relação à variável de ambiente OSQLSERVER; o que significa que o **sqlcmd** e **osql** podem ser usados próximos um do outro sem interferência e que scripts antigos continuarão funcionado.  
  
 **-U** *login_id*  
 Nome de logon ou nome de usuário de banco de dados independente. Para usuários de banco de dados independente, é necessário fornecer a opção de nome de banco de dados (-d).  
  
> [!NOTE]  
>  A variável de ambiente OSQLUSER está disponível para compatibilidade com versões anteriores. A variável de ambiente SQLCMDUSER tem precedência em relação à variável de ambiente OSQLUSER. Isso significa que o **sqlcmd** e **osql** podem ser usados próximos um do outro sem interferência. Significa também que scripts **osql** existentes continuarão funcionando.  
  
 Se nem o **- U** opção nem o **-P** opção for especificada, **sqlcmd** tenta se conectar usando o modo de autenticação do Microsoft Windows. A autenticação se baseia na conta do Windows do usuário que está executando o **sqlcmd**.  
  
 Se a opção **-U** for usada com a opção **-E** (descrita adiante neste tópico), uma mensagem de erro será gerada. Será gerada uma mensagem de erro e o programa será encerrado se a opção **–U** for seguida por mais de um argumento.  
  
 **-z** *new_password*  
 Alterar senha:  
  
 `sqlcmd -U someuser -P s0mep@ssword -z a_new_p@a$$w0rd`  
  
 **-Z** *new_password*  
 Alterar senha e sair:  
  
 `sqlcmd -U someuser -P s0mep@ssword -Z a_new_p@a$$w0rd`  
  
 **Opções de entrada/saída**  
  **-f** *codepage* | **i: * **codepage*[**, o:***codepage *] | **o: * **codepage*[**, i:***codepage *]  
 Especifica as páginas de código de entrada e saída. O número da página de código é um valor numérico que especifica um código de página instalada do Windows.  
  
 Regras de conversão de página de código:  
  
-   Se nenhuma página de código for especificada, o **sqlcmd** usará a página de código atual para arquivos de entrada e de saída, a menos que o arquivo de entrada seja um arquivo Unicode, para o qual nenhuma conversão é necessária.  
  
-   O**sqlcmd** reconhece arquivos de entrada Unicode big endian e little endian automaticamente. Se a opção **-u** tiver sido especificada, a saída sempre será Unicode little endian.  
  
-   Se não for especificado nenhum arquivo de saída, a página de código de saída será a página de código de console. Isso habilita a saída a ser exibida corretamente no console.  
  
-   Assume-se que arquivos de entrada múltiplos tenham a mesma página de código. Arquivos de entrada Unicode e não Unicode podem ser misturados.  
  
 Digite **chcp** no prompt de comando para verificar a página de código de Cmd.exe.  
  
 **-i** *input_file*[**,***input_file2*...]  
 Identifica o arquivo que contém um lote de instruções SQL ou procedimentos armazenados. Poderão ser especificados vários arquivos para serem lidos e processados em ordem. Não use espaço entre nomes de arquivos. O**sqlcmd** verificará primeiramente se todos os arquivos especificados existem. Se um ou mais arquivos não existirem, o **sqlcmd** será encerrado. As opções -i e Q/-q são mutuamente exclusivas.  
  
 Exemplos de caminho:  

```  
-i C:\<filename>  
-i \\<Server>\<Share$>\<filename>  
-i "C:\Some Folder\<file name>"  
```
  
 Os nomes de caminhos que contêm espaços deverão ficar entre aspas.  
  
 Esta opção pode ser usada mais de uma vez: **-i * input_file* **-, *, input_file.*  
  
 **-o** *output_file*  
 Identifica o arquivo que recebe a saída do **sqlcmd**.  
  
 Se **-u** for especificado, *output_file* será armazenado no formato Unicode. Se o nome do arquivo não for válido, uma mensagem de erro será gerada e o **sqlcmd** será encerrado. O**sqlcmd** não permite gravação simultânea de vários processos **sqlcmd** no mesmo arquivo. A saída de arquivo será corrompida ou incorreta. Consulte a opção **-f** para obter mais informações sobre formatos de arquivo. Caso não exista, esse arquivo será criado. Um arquivo com o mesmo nome de uma sessão **sqlcmd** anterior será substituído. O arquivo aqui especificado não é o arquivo **stdout** . Se for especificado um arquivo **stdout** este arquivo não será usado.  
  
 Exemplos de caminho:  

```  
-o C:< filename>  
-o \\<Server>\<Share$>\<filename>  
-o "C:\Some Folder\<file name>"  
 ``` 
 Os nomes de caminhos que contêm espaços deverão ficar entre aspas.  
  
 **-r**[**0** | **1**]  
 Redireciona a saída da mensagem de erro para a tela (**stderr**). Se você não especificar um parâmetro ou se especificar **0**, serão redirecionadas somente mensagens de erro com nível de severidade 11 ou acima disso. Se você especificar **1**, serão redirecionadas todas as saídas de mensagens de erro inclusive PRINT. Não tem nenhum efeito se você usar -o. Por padrão, mensagens são envidadas para **stdout**.  
  
 **-R**  
 Faz com que **sqlcmd** localizar colunas de hora, moeda, data e numérico recuperados do SQL Server com base na localidade do cliente. Por padrão, essas colunas são exibidas usando as configurações regionais do servidor.  
  
 **-u**  
 Especifica se *output_file* é armazenado no formato Unicode, independentemente do formato de *input_file*.  
  
 **Opções de execução de consultas**  
  **-e**  
 Grava scripts de entrada no dispositivo de saída padrão (**stdout**).  
  
 **-I**  
 Define a opção de conexão SET QUOTED_IDENTIFIER como ON. Por padrão, ela é definida como OFF. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](~/t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 **-q"** *cmdline query* **"**  
 Executa uma consulta quando o **sqlcmd** é iniciado, mas não fecha o **sqlcmd** após a execução da consulta. Podem ser executadas consultas delimitadas por vários ponto e vírgula. Use aspas na consulta, conforme o exemplo a seguir.  
  
 No prompt de comando, digite:  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  Não use o terminador GO na consulta.  
  
 Se **-b** for especificado junto com esta opção, **sqlcmd** será fechado com um erro. **-b** é descrito posteriormente neste tópico.  
  
 **-Q"** *cmdline query* **"**  
 Executa uma consulta quando o **sqlcmd** é iniciado e fecha o **sqlcmd**imediatamente. Podem ser executadas consultas delimitadas por vários ponto e vírgula.  
  
 Use aspas na consulta, conforme o exemplo a seguir.  
  
 No prompt de comando, digite:  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  Não use o terminador GO na consulta.  
  
 Se **-b** for especificado junto com esta opção, **sqlcmd** será fechado com um erro. **-b** é descrito posteriormente neste tópico.  
  
 **-t** *query_timeout*  
 Especifica quanto segundos faltam para que um comando (ou instrução SQL) expire. Essa opção define a variável de script SQLCMDSTATTIMEOUT do **sqlcmd** . Se um valor *time_out* não for especificado, o comando não atingirá o tempo limite. O *consulta * * time_out* deve ser um número entre 1 e 65534. Se o valor fornecido não for numérico ou se não estiver nesse intervalo, o **sqlcmd** vai gerar uma mensagem de erro.  
  
> [!NOTE]  
>  O valor do tempo limite real poderá variar em relação ao valor *time_out* especificado em vários segundos.  
  
 **-vvar =**  *value*[ **var =** *value*...]  
 Cria uma variável de script **sqlcmd**que pode ser usada em um script **sqlcmd** . Se o valor contiver espaços, mantenha-o entre aspas. Você pode especificar vários ***var***=**"***valores***"** valores. Se houver erros em algum dos valores especificados, o **sqlcmd** vai gerar uma mensagem de erro e será encerrado.  
  
 `sqlcmd -v MyVar1=something MyVar2="some thing"`  
  
 `sqlcmd -v MyVar1=something -v MyVar2="some thing"`  
  
 **-x**  
 Faz com que o **sqlcmd** ignore variáveis de script. Isso é útil quando um script contém muitas instruções INSERT que podem conter cadeias de caracteres que têm o mesmo formato de variáveis regulares, como $(*variable_name*).  
  
 **Opções de formatação**  
  **-h** *headers*  
 Especifica o número de linhas a imprimir entre os títulos da coluna. O padrão é imprimir títulos uma vez para cada conjunto de resultados de consulta. Essa opção define a variável de script SQLCMDHEADERS do **sqlcmd** . Use **-1** para especificar que os cabeçalhos não devem ser impressos. Qualquer valor inválido faz com que o **sqlcmd** gere uma mensagem de erro e seja encerrado.  
  
 **-k** [**1** | **2**]  
 Remove todos os caracteres de controle, como tabulações e caracteres de nova linha, da saída. Isso preserva a formatação de coluna quando os dados são retornados. Se for especificado 1, os caracteres de controle serão substituídos por um único espaço. Se for especificado 2, os caracteres de controle consecutivos serão substituídos por um único espaço. **-k** é igual a **-k1**.  
  
 **-s** *col_separator*  
 Especifica o caractere do separador de coluna. O padrão é um espaço em branco. Essa opção define a variável de script SQLCMDCOLSEP do **sqlcmd** . Para usar caracteres com um significado especial para o sistema operacional como, por exemplo, E comercial (&) ou ponto e vírgula (;), use-os entre aspas ("). O separador de coluna pode ser qualquer caractere de 8 bits.  
  
 **-w** *column_width*  
 Especifica a largura de tela para saída. Essa opção define a variável de script SQLCMDCOLWIDTH do **sqlcmd** . A largura da coluna deve ser um número maior que 8 e menor que 65536. Se a largura da coluna especificada não estiver nesse intervalo, o **sqlcmd** vai gerar uma mensagem de erro. A largura padrão é 80 caracteres. Quando uma linha de saída excede a largura de coluna especificada, ela inclui a próxima linha.  
  
 **-W**  
 Essa opção remove espaços à direita de uma coluna. Use esta opção com a opção **-s** ao preparar dados a serem exportados para outro aplicativo. Ela não pode ser usada com as opções **-y** ou **-Y** .  
  
 **-y** *variable_length_type_display_width*  
 Define a variável de script **sqlcmd** `SQLCMDMAXVARTYPEWIDTH`. O padrão é 256. Ele limita o número de caracteres retornados para os tipos de dados com comprimento variável grande:  
  
-   **varchar(max)**  
  
-   **nvarchar(max)**  
  
-   **varbinary(max)**  
  
-   **xml**  
  
-   **UDT (tipos de dados definidos pelo usuário)**  
  
-   **texto**  
  
-   **ntext**  
  
-   **imagem**  
  
> [!NOTE]  
>  UDTs podem ter comprimento fixo dependendo da implementação. Se esse tamanho de UDT de tamanho fixo for mais curto que *display_width*, o valor do UDT retornado não será afetado. Porém, se o tamanho for mais longo que *display_width*, a saída será truncada.  
   
  
> [!IMPORTANT]  
>  Use a opção **-y 0** com muito cuidado, porque isso poderá causar graves problemas de desempenho tanto no servidor quanto na rede, dependendo do tamanho dos dados retornados.  
  
 **-Y** *fixed_length_type_display_width*  
 Define a variável de script **sqlcmd** `SQLCMDMAXFIXEDTYPEWIDTH`. O padrão é 0 (ilimitado). Limita o número de caracteres retornado para os tipos de dados a seguir:  
  
-   **char(** *n* **)**, where 1<=n<=8000  
  
-   **nchar(n** *n* **)**, where 1<=n<=4000  
  
-   **varchar(n** *n* **)**, where 1<=n<=8000  
  
-   **nvarchar(n** *n* **)**, where 1<=n<=4000  
  
-   **varbinary(n** *n* **)**, where 1<=n\<=4000  
  
-   **variant**  
  
 **Opções de relatório de erros**  
  **-b**  
 Especifica que o **sqlcmd** é fechado e retorna um valor DOS ERRORLEVEL em caso de erro. O valor retornado à variável DOS ERRORLEVEL é **1** quando a mensagem de erro do SQL Server tem um nível de severidade maior que 10; caso contrário, o valor retornado é **0**. Se a opção **-V** tiver sido definida além de **-b**, o **sqlcmd** não relatará um erro se o nível de severidade for inferior aos valores definidos com **-V**. Arquivos em lote do prompt de comando podem testar o valor de ERRORLEVEL e tratar o erro adequadamente. O**sqlcmd** não relata erros para o nível de severidade 10 (mensagens informativas).  
  
 Se o script **sqlcmd** tiver um comentário incorreto, erro de sintaxe, ou se estiver faltando uma variável de script, ERRORLEVEL retorna 1.  
  
 **-m** *error_level*  
 Controla quais mensagens de erro são enviadas para **stdout**. Mensagens com um nível de severidade maior ou igual a esse nível são enviadas. Quando esse valor for definido como **-1**, todas as mensagens, incluindo mensagens informativas, serão enviadas. Não são permitidos espaços entre **-m** e **-1**. Por exemplo, **-m-1** é válido, e **-m-1** não.  
  
 Essa opção também define a variável de script SQLCMDERRORLEVEL do **sqlcmd** . Essa variável tem um padrão de 0.  
  
 **-V** *error_severity_level*  
 Controla o nível de severidade usado para definir a variável ERRORLEVEL. Mensagens de erro com níveis de severidade maiores ou iguais a esse valor definem ERRORLEVEL. Valores menores que 0 são reportados como 0. Podem ser usados arquivos de lote e CMD para testar o valor da variável ERRORLEVEL.  
  
 **Opções diversas**  
  **-a** *packet_size*  
 Exige um pacote de tamanho diferente. Essa opção define a variável de script SQLCMDPACKETSIZE do **sqlcmd** . *packet_size* deve ser um valor entre 512 e 32767. O padrão é igual a 4096. Um tamanho de pacote maior pode melhorar o desempenho da execução de scripts que tenham muitas instruções SQL entre comandos GO. Pode-se solicitar um tamanho de pacote maior. Porém, se a solicitação for negada, o **sqlcmd** usará o padrão de servidor para tamanho de pacote.  
  
 **-c** *batch_terminator*  
 Especifica o terminador de lote. Por padrão, os comandos são terminados e enviados para o SQL Server, digitando a palavra "GO" em uma linha por si só. Quando você redefinir o terminador de lote, não use palavras-chave reservada Transact-SQL ou caracteres que têm um significado especial para o sistema operacional, mesmo se elas são precedidas por uma barra invertida.  
  
 **-L**[**c**]  
 Lista os computadores servidor localmente configurados e os nomes dos computadores servidor que estão transmitindo na rede. Esse parâmetro não pode ser usado em combinação com outros parâmetros. O número máximo de computadores servidores que pode ser listado é 3000. Se a lista de servidores ficar truncada devido ao tamanho do buffer, será exibida uma mensagem de aviso.  
  
> [!NOTE]  
>  Devido à natureza da transmissão em redes, o **sqlcmd** pode não receber a tempo uma resposta de todos os servidores. Assim, a lista de servidores retornada pode variar para cada invocação dessa opção.  
  
 Se for especificado o parâmetro opcional **c** , a saída aparecerá sem os servidores: linha de cabeçalho e cada linha de servidor será listada sem espaços à esquerda. Isso é chamado de saída normal. A saída normal melhora o desempenho de processamento das linguagens dos scripts.  
  
 **-p**[**1**]  
 Imprime estatísticas de desempenho para cada conjunto de resultados. O exemplo a seguir mostra o formato para estatísticas de desempenho:  
  
 `Network packet size (bytes): n`  
  
 `x xact[s]:`  
  
 `Clock Time (ms.): total       t1  avg       t2 (t3 xacts per sec.)`  
  
 Onde:  
  
 `x`= Número de transações que são processadas pelo SQL Server.  
  
 `t1` = Tempo total para todas as transações.  
  
 `t2` = Tempo médio de uma única transação.  
  
 `t3` = Número médio de transações por segundo.  
  
 Todos os tempos estão em milissegundos.  
  
 Se o parâmetro opcional **1** for especificado, o formato de saída das estatísticas estará em formato separado por dois pontos, que poderá ser facilmente importado para uma planilha ou processado por um script.  
  
 Se o parâmetro opcional for qualquer valor diferente de **1**, será gerado um erro e o **sqlcmd** será encerrado.  
  
 **-X**[**1**]  
 Desabilita os comandos que podem comprometer a segurança do sistema quando o **sqlcmd** é executado em um arquivo em lotes. Os comandos desabilitados ainda são reconhecidos; o **sqlcmd** emite uma mensagem de aviso e continua. Se for especificado o parâmetro opcional **1** , o **sqlcmd** vai gerar uma mensagem de erro e será encerrado. Os seguintes comandos são desabilitados quando a opção **-X** é usada:  
  
-   **ED**  
  
-   **!!** *command*  
  
 Se a opção **-X** for especificada, isso prevenirá que variáveis de ambiente sejam passadas para o **sqlcmd**. Evita também que o script de inicialização especificado, usando a variável de script SQLCMDINI, seja executado. Para obter mais informações sobre as variáveis de script do **sqlcmd** , consulte [Usar o sqlcmd com variáveis de script](~/relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
 **-?**  
 Exibe a versão do **sqlcmd** e um resumo da sintaxe das opções do **sqlcmd** .  
  
## <a name="remarks"></a>Remarks  
 As opções não precisam ser usadas na ordem mostrada na seção de sintaxe.  
  
 Quando são retornados vários resultados, o **sqlcmd** imprime uma linha em branco entre cada conjunto de resultados em um lote. Além disso, a mensagem `<x> rows affected` não é exibida quando não se aplica à instrução executada.  
  
 Para usar o **sqlcmd** interativamente, digite **sqlcmd** no prompt de comando com uma ou mais das opções descritas anteriormente neste tópico. Para obter mais informações, consulte [Usar o Utilitário sqlcmd](~/relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
> [!NOTE]  
>  As opções **-L**, **-Q**, **-Z** ou **-i** fazem com que o **sqlcmd** seja fechado após a execução.  
  
 O tamanho total da linha de comando do **sqlcmd** no ambiente de comando (Cmd.exe), incluindo todos os argumentos e variáveis expandidas, é aquele determinado pelo sistema operacional para Cmd.exe.  
  
## <a name="variable-precedence-low-to-high"></a>Precedência de variável (baixa para alta)  
  
1.  Variáveis ambientais do nível de sistema.  
  
2.  Variáveis ambientais do nível de usuário.  
  
3.  Shell de comando (**SET** X=Y) definido no prompt de comando antes da execução do **sqlcmd**.  
  
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
|SQLCMDSTATTIMEOUT|-t|R/W|"0" = espere indefinidamente|  
|SQLCMDHEADERS|-H|R/W|"0"|  
|SQLCMDCOLSEP|-S|R/W|" ."|  
|SQLCMDCOLWIDTH|-w|R/W|"0"|  
|SQLCMDPACKETSIZE|-A|R|"4096"|  
|SQLCMDERRORLEVEL|-M|R/W|0|  
|SQLCMDMAXVARTYPEWIDTH|-y|R/W|"256"|  
|SQLCMDMAXFIXEDTYPEWIDTH|-y|R/W|"0" = ilimitado|  
|SQLCMDEDITOR||R/W|"edit.com"|  
|SQLCMDINI||R|""|
|SQLCMDUSEAAD  | - G | R/W | "" |  
  
 SQLCMDUSER, SQLCMDPASSWORD e SQLCMDSERVER são definidos ao usar **:Connect** .  
  
 R indica que o valor pode ser definido apenas uma vez durante a inicialização do programa.  
  
 R/W indica que o valor pode ser modificado com o comando **setvar** e que os próximos comandos serão influenciados pelo novo valor.  
  
## <a name="sqlcmd-commands"></a>Comandos sqlcmd  
 Além de instruções Transact-SQL em **sqlcmd**, os comandos a seguir também estão disponíveis:  
  
|||  
|-|-|  
|**GO** [*count*]|**:List**|  
|[**:**] **RESET**|**:Error**|  
|[**:**] **ED**|**:Out**|  
|[**:**] **!!**|**:Perftrace**|  
|[**:**] **QUIT**|**:Connect**|  
|[**:**] **EXIT**|**:On Error**|  
|**:r**|**:Help**|  
|**:ServerList**|**:XML** [**ON** &#124; **OFF**]|  
|**:Setvar**|**:Listvar**|  
  
 Lembre-se do seguinte ao usar comandos **sqlcmd** :  
  
-   Todos os comandos do **sqlcmd** , exceto GO, devem ser prefixados com dois-pontos (:).  
  
    > [!IMPORTANT]  
    >  Para manter a compatibilidade com versões anteriores de scripts **osql** existentes, alguns dos comandos serão reconhecidos sem os dois-pontos. Isso é indicado pelo [**:**].  
  
-   Os comandos**sqlcmd** serão reconhecidos apenas se aparecerem no início de uma linha.  
  
-   Todos os comandos **sqlcmd** não diferenciam maiúsculas de minúsculas.  
  
-   Cada comando deve estar em uma linha separada. Um comando não pode ser seguido por uma instrução Transact-SQL ou outro comando.  
  
-   Comandos são executados imediatamente. Eles não são colocados no buffer de execução como instruções Transact-SQL.  
  
 **Comandos de Edição**  
  [**:**] **ED**  
 Inicie o editor de textos. Esse editor pode ser usado para editar o lote Transact-SQL atual ou a última execução em lotes. Para editar o último lote executado, o comando **ED** deve ser digitado imediatamente depois da execução do último lote.  
  
 O editor de textos é definido pela variável de ambiente SQLCMDEDITOR. O editor padrão é 'Editar.' Para alterar o editor, defina a variável de ambiente SQLCMDEDITOR. Por exemplo, para definir o editor para o Microsoft Notepad, no prompt de comando, digite:  
  
 `SET SQLCMDEDITOR=notepad`  
  
 [**:**] **RESET**  
 Desmarca o cache de instruções.  
  
 **:List**  
 Imprime o conteúdo do cache de instrução.  
  
 **Variables**  
  **:Setvar** \<**var**> [ **"***value***"** ]  
 Define as variáveis de script do **sqlcmd** . Variáveis de script têm o seguinte formato: `$(VARNAME)`.  
  
 Nomes de variáveis não diferenciam maiúsculas de minúsculas.  
  
 Variáveis de script podem ser definidas da seguinte forma:  
  
-   Usando-se implicitamente uma opção de linha de comando. Por exemplo, a opção **-l** define a variável SQLCMDLOGINTIMEOUT do **sqlcmd** .  
  
-   Explicitamente, usando o comando **:Setvar** .  
  
-   Definindo uma variável de ambiente antes de executar o **sqlcmd**.  
  
> [!NOTE]  
>  A opção **-X** previne que variáveis de ambiente sejam passadas para o **sqlcmd**.  
  
 Se uma variável definida com **:Setvar** e uma variável de ambiente tiverem o mesmo nome, a variável definida com **:Setvar** terá precedência.  
  
 Nomes de variáveis não devem conter caracteres de espaço em branco.  
  
 Nomes de variáveis não podem ter a mesma forma que uma expressão variável, como $ (var).  
  
 Se o valor da cadeia de caracteres da variável de script tiver espaços em branco, use aspas. Se não for especificado um valor para uma variável de script, a variável de script será descartada.  
  
 **:Listvar**  
 Exibe uma lista das variáveis de script definidas atualmente.  
  
> [!NOTE]  
>  Serão exibidas somente variáveis de script definidas pelo **sqlcmd**e aquelas definidas usando o comando **:Setvar** .  
  
 **Comandos de Saída**  
  **:Error**   
 ***\<***  *filename*  ***>|* STDERR|STDOUT**  
 Redireciona toda a saída de erro para o arquivo especificado por *nome do arquivo*para **stderr** ou **stdout**. O comando **Error** pode aparecer várias vezes em um script. Por padrão, saída de erro é enviada para **stderr**.  
  
 *nome do arquivo*  
 Cria e abre um arquivo que receberá a saída. Se o arquivo já existir, será truncado para zero bytes. Se o arquivo não estiver disponível devido a permissões ou outras razões, a saída não será alternada e será enviada ao último destino especificado ou ao destino padrão.  
  
 **STDERR**  
 Muda a saída de erro para o fluxo **stderr** . Se houver redirecionamento, o destino para o qual o fluxo foi redirecionado receberá a saída de erro.  
  
 **STDOUT**  
 Muda a saída de erro para o fluxo **stdout** . Se houver redirecionamento, o destino para o qual o fluxo foi redirecionado receberá a saída de erro.  
  
 **:Out \<** *filename* **>**| **STDERR**| **STDOUT**  
 Cria e redireciona todos os resultados da consulta para o arquivo especificado por *nome do arquivo*para **stderr** ou **stdout**. Por padrão, a saída é enviada para **stdout**. Se o arquivo já existir, será truncado para zero bytes. O comando **Out** pode aparecer várias vezes em um script.  
  
 **:Perftrace \<** *filename* **>**| **STDERR**| **STDOUT**  
 Cria e redireciona todas as informações de rastreamento de desempenho para o arquivo especificado por *nome do arquivo*para **stderr** ou **stdout**. Por padrão a saída de rastreamento de desempenho é enviada para **stdout**. Se o arquivo já existir, será truncado para zero bytes. O comando **Perftrace** pode aparecer várias vezes em um script.  
  
 **Comandos de controle de execução**  
  **:On Error**[ **exit** | **ignore**]  
 Define a ação a ser executada no caso de um erro durante a execução de script ou em lote.  
  
 Quando a opção **exit** é usada, o **sqlcmd** é encerrado com o valor de erro adequado.  
  
 Quando é usada a opção **ignore** , o **sqlcmd** ignora o erro e continua executando o lote ou script. Por padrão, será impressa uma mensagem de erro.  
  
 [**:**] **QUIT**  
 Faz com que o **sqlcmd** seja fechado.  
  
 [**:**] **EXIT**[ **(***instrução***)** ]  
 Permite usar o resultado de uma instrução SELECT como o valor de retorno do **sqlcmd**. Se numérico, a primeira coluna da última linha do resultado será convertida em um inteiro de 4 bytes (longo). O MS-DOS transmite o byte baixo para o processo pai ou nível de erro do sistema operacional. O Windows 200x passa todo o número inteiro de 4 bytes. A sintaxe é:  
  
 `:EXIT(query)`  
  
 Por exemplo:  
  
 `:EXIT(SELECT @@ROWCOUNT)`  
  
 É possível incluir também o parâmetro **EXIT** como parte de um arquivo em lote. Por exemplo, no prompt de comando, digite:  
  
 `sqlcmd -Q "EXIT(SELECT COUNT(*) FROM '%1')"`  
  
 O utilitário **sqlcmd** envia tudo entre os parênteses **()** para o servidor. Se um procedimento armazenado de sistema selecionar um conjunto e retornar um valor, somente a seleção será retornada. A instrução EXIT**()** sem nada entre os parênteses executa tudo antes dela no lote e é fechada sem um valor de retorno.  
  
 Quando é especificada uma consulta incorreta, o **sqlcmd** é encerrado sem um valor de retorno.  
  
 Eis uma lista de formatos EXIT:  
  
-   :EXIT  
  
 Não executa o lote e então sai imediatamente e não retorna valor algum.  
  
-   :EXIT( )  
  
 Executa o lote e então sai imediatamente e não retorna valor algum.  
  
-   :EXIT(query)  
  
 Executa o lote que inclui a consulta, e então sai depois de retornar os resultados da consulta.  
  
 Se for usado RAISERROR em um script do **sqlcmd** e ocorrer um estado 127, o **sqlcmd** será encerrado e retornará a ID da mensagem para o cliente. Por exemplo:  
  
 `RAISERROR(50001, 10, 127)`  
  
 Esse erro fará com que o script do **sqlcmd** seja encerrado e retorne a ID de mensagem 50001 ao cliente.  
  
 Os valores de retorno -1 a -99 são reservados pelo SQL Server. **sqlcmd** define os seguintes valores de retorno adicionais:  
  
|Valores de retorno|Description|  
|-------------------|-----------------|  
|-100|Erro encontrado antes da seleção do valor de retorno.|  
|-101|Nenhuma linha encontrada ao se selecionar o valor de retorno.|  
|-102|Erro de conversão ao selecionar valor de retorno.|  
  
 **GO** [*count*]  
 GO sinaliza tanto o término de um lote e a execução de qualquer cache instruções Transact-SQL. O lote é executado várias vezes como lotes separados; Você não pode declarar uma variável de mais de uma vez em um único lote.
  
 **Comandos diversos**  
  **:r \<** *filename***>**  
 Analisa instruções Transact-SQL adicionais e **sqlcmd** comandos do arquivo especificado por  **\< ***filename***>**na instrução cache.  
  
 Se o arquivo contém instruções de Transact-SQL que não são seguidas por **VÁ**, você deve inserir **VÁ** na linha que segue **: r**.  
  
> [!NOTE]  
>  **\<** *filename* **>** é lido em relação ao diretório de inicialização no qual o **sqlcmd** foi executado.  
  
 O arquivo será lido e executado depois que for encontrado um terminador de lote. Podem ser emitidos vários comandos **:r** . O arquivo pode incluir qualquer comando **sqlcmd** . Isso inclui o terminador de lote **GO**.  
  
> [!NOTE]  
>  A contagem de linha que é exibida em modo interativo será aumentada em um para cada comando **:r** encontrado. O comando **:r** aparecerá na saída do comando de lista.  
  
 **:Serverlist**  
 Lista os servidores configurados localmente e os nomes dos servidores que estão transmitindo na rede.  
  
 **: Conectar***nome_do_servidor*[**\\* nome_da_instância*] [-l *timeout*] [-U *user_name* [-P *senha*]]    
 Conecta-se a uma instância do SQL Server. Além disso fecha a conexão atual.  
  
 Opções de tempo limite:  
  
|||  
|-|-|  
|0|esperar|  
|n>0|esperar por n segundos|  
  
 A variável de script SQLCMDSERVER refletirá a conexão ativa atual.  
  
 Se não for especificado *timeout* , o valor da variável SQLCMDLOGINTIMEOUT será o padrão.  
  
 Se apenas *user_name* for especificado (como uma opção ou variável de ambiente), será solicitado que o usuário insira uma senha. Isso não ocorre se as variáveis de ambiente SQLCMDUSER ou SQLCMDPASSWORD tiverem sido definidas. Se as opções e as variáveis de ambiente não forem fornecidas, o modo de Autenticação do Windows será usado para fazer logon. Por exemplo, para se conectar a uma instância, `instance1`, do SQL Server, `myserver`, usando segurança integrada você usaria o seguinte:  
  
 `:connect myserver\instance1`  
  
 Para conectar-se à instância padrão do `myserver` usando variáveis de script, você usaria o seguinte:  
  
 `:setvar myusername test`  
  
 `:setvar myservername myserver`  
  
 `:connect $(myservername) $(myusername)`  
  
 [**:**] **!!**< *command*>  
 Executa comandos de sistema operacional. Para executar um comando do sistema operacional, inicie uma linha com dois pontos de exclamação (**!!**) seguida do comando do sistema operacional. Por exemplo:  
  
 `:!! Dir`  
  
> [!NOTE]  
>  O comando é executado no computador em que o **sqlcmd** está sendo executado.  
  
 **:XML** [**ON** | **OFF**]  
 Para obter mais informações, consulte [Formato de saída XML](#OutputXML) e [Formato de saída JSON](#OutputJSON) neste tópico  
  
 **:Help**  
 Lista comandos do **sqlcmd** , juntamente com uma breve descrição de cada comando.  
  
### <a name="sqlcmd-file-names"></a>Nomes de arquivos sqlcmd  
 Arquivos de entrada do**sqlcmd** podem ser especificados com a opção **-i** ou o comando **:r** . Arquivos de saída podem ser especificados com a opção **-o** ou os comandos **:Error**, **:Out** e **:Perftrace** . A seguir algumas diretrizes sobre como trabalhar com esses arquivos:  
  
-   **: Erro**, **: Out** e **: Perftrace** devem usar separada  **\< ***filename***>**. Se o mesmo  **\< ***filename*** >**  é usado, entradas dos comandos poderão ser misturadas.  
  
-   Se um arquivo de entrada localizado em um servidor remoto for chamado no **sqlcmd** em um computador local e o arquivo contiver um caminho de arquivo de unidade como :out c:\OutputFile.txt. O arquivo de saída será criado no computador local e não no servidor remoto.  
  
-   Caminhos de arquivo válidos incluem: `C:\<filename>`, `\\<Server>\<Share$>\<filename>` e `"C:\Some Folder\<file name>"`. Se houver um espaço no caminho, use aspas.  
  
-   Cada nova sessão do **sqlcmd** substituirá arquivos existentes que tenham os mesmos nomes.  
  
### <a name="informational-messages"></a>Mensagens informativas  
 O**sqlcmd** imprime qualquer mensagem informativa enviada pelo servidor. No exemplo a seguir, após a execução de instruções Transact-SQL, é impressa uma mensagem informativa.  
  
 No prompt de comando, digite o seguinte:  
  
 `sqlcmd`  
  
 `At the sqlcmd prompt type:`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 Ao pressionar ENTER, será impressa a seguinte mensagem informativa: "Contexto de banco de dados alterado para 'AdventureWorks2012'."  
  
### <a name="output-format-from-transact-sql-queries"></a>Formato de saída do Transact-SQL Queries  
 O**sqlcmd** imprime, em primeiro lugar, um cabeçalho de coluna com os nomes de coluna especificados na lista de seleção. Os nomes de coluna são separados usando-se o caractere SQLCMDCOLSEP. Por padrão, esse é um espaço. Se o nome de coluna for mais curto do que a largura de coluna, a saída será preenchida com espaços até a coluna seguinte.  
  
 Essa linha será seguida por uma linha divisória formada por uma série de tracejados. A saída a seguir mostra um exemplo.  
  
 Inicie o **sqlcmd**. No prompt de comando do **sqlcmd** , digite o seguinte:  
  
 `USE AdventureWorks2012;`  
  
 `SELECT TOP (2) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 Ao pressionar ENTER, o seguinte conjunto de resultados é reajustado.  
  
 `BusinessEntityID FirstName    LastName`  
  
 `---------------- ------------ ----------`  
  
 `285              Syed         Abbas`  
  
 `293              Catherine    Abel`  
  
 `(2 row(s) affected)`  
  
 Embora a coluna `BusinessEntityID` tenha apenas 4 caracteres de largura, ela foi expandida para acomodar o nome de coluna mais longo. Por padrão, a saída é finalizada com 80 caracteres. Isso pode ser alterado com a opção **-w** ou com a definição da variável de script SQLCMDCOLWIDTH.  
  
###  <a name="OutputXML"></a> Formato de saída XML  
 Saída XML é o resultado de uma cláusula FOR XML, não formatada, em um fluxo contínuo.  
  
 Quando você esperar uma saída XML, use o seguinte comando: `:XML ON`.  
  
> [!NOTE]  
>  O**sqlcmd** retorna mensagens de erro no formato habitual. Observe que as mensagens de erro também são produzidas no fluxo de texto XML em formato XML. Usando `:XML ON`, o **sqlcmd** não exibe mensagens informativas.  
  
 Para definir XML em modo off, use o seguinte comando: `:XML OFF`.  
  
 O comando GO não deve ser exibido antes que o comando XML OFF seja emitido, pois o comando XML OFF muda o **sqlcmd** de volta para a saída orientada por linhas.  
  
 Dados XML (em fluxo) e dados de conjunto de linhas não podem ser misturados. Se o comando XML ON não tiver sido emitido antes de uma instrução Transact-SQL que gera protocolos XML é executada, a saída será adulterada. Se o comando XML ON tiver sido emitido, não é possível executar instruções Transact-SQL que gerem conjuntos de linhas normais.  
  
> [!NOTE]  
>  O comando **:XML** não oferece suporte para a instrução SET STATISTICS XML.  
  
###  <a name="OutputJSON"></a> Formato de saída JSON  
 Quando você espera uma saída JSON, use o seguinte comando: `:XML ON`. Caso contrário, a saída incluirá o nome da coluna e o texto JSON. Essa saída não é JSON válido.  
  
 Para definir XML em modo off, use o seguinte comando: `:XML OFF`.  
  
 Para saber mais, confira [Formato de saída XML](#OutputXML) neste tópico.  

### <a name="using-azure-active-directory-authentication"></a>Usando a Autenticação do Azure Active Directory  
Exemplos que usam a Autenticação do Azure Active Directory:
```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  -l 30
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```
  
## <a name="sqlcmd-best-practices"></a>Práticas recomendadas sqlcmd  
 Use as seguintes práticas para ajudar a maximizar a segurança e a eficiência.  
  
-   Use segurança integrada.  
  
-   Use **-X** em ambientes automatizados.  
  
-   Proteja arquivos de entrada e de saída usando permissões adequadas de sistema de arquivos NTFS.  
  
-   Para aumentar o desempenho, faça o máximo possível em uma sessão **sqlcmd** , em vez de usar uma série de sessões.  
  
-   Defina valores mais altos de tempo limite para execução em lote ou de consulta do que você imagina que levará para a execução em lote ou de consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o utilitário sqlcmd](~/relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [Executar arquivos de script Transact-SQL usando sqlcmd](~/relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)   
 [Usar o utilitário sqlcmd](~/relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [Usar sqlcmd com variáveis de script](~/relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [Conectar-se ao mecanismo de banco de dados com sqlcmd](~/relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)   
 [Editar scripts SQLCMD com o Editor de Consultas](~/relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [Gerenciar etapas de trabalho](~/ssms/agent/manage-job-steps.md)   
 [Criar uma etapa de trabalho CmdExec](~/ssms/agent/create-a-cmdexec-job-step.md)  
  
  









