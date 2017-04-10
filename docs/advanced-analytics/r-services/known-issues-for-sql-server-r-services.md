---
title: "Problemas conhecidos do SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 52
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 49
---
# Problemas conhecidos do SQL Server R Services
  Este tópico descreve as limitações e os problemas com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] e os componentes relacionados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].  
  
> [!NOTE]
> Outros problemas relacionados à instalação e configuração iniciais são listados aqui: [ Perguntas frequentes sobre a atualização e instalação do](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md).  
  
## <a name="r-services-in-database"></a>R Services (no banco de dados)  
 Esta seção lista problemas específicos ao recurso do mecanismo de banco de dados que dá suporte à integração do R.  

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Instalar a última versão do serviço para garantir a compatibilidade com o Cliente do Microsoft R

Se você instalar a última versão do Cliente do Microsoft R e usá-la para executar o R no SQL Server usando um contexto de computação remota, poderá receber o seguinte erro:

*Você está executando a versão 9.0.0 do cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

Normalmente, a versão do R instalada com o SQL Server R Services é atualizada quando as versões de serviço são publicadas. Para garantir que você sempre tem as versões mais atualizadas dos componentes do R, instale todos os service packs. Para compatibilidade com o Cliente do Microsoft R 9.0.0, é necessário instalar as atualizações descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262). 
  
### <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>Novo contrato de licença para componentes do R necessários para instalações autônomas  
 Se você usar a linha de comando para instalar uma instância do SQL Server que já tem o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] instalado, será necessário editar a linha de comando para usar o novo parâmetro de contrato de licença, */IACCEPTROPENLICENSEAGREEMENT*. O uso mal-sucedido do argumento correto pode causar uma falha na configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="warning-of-incompatible-version-when-connecting-to-older-version-of-sql-server--r-services-from-a-client-using-includesssqlv14mdtokensqlv14sssqlv14mdmd"></a>Aviso de versão incompatível ao se conectar à versão anterior do SQL Server R Services por meio de um cliente usando o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 

Se você tiver instalado o Microsoft R Server em um computador cliente usando o assistente de instalação do [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] ou o novo instalador autônomo para o [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) e estiver executando o código R em um contexto de computação que usa uma versão anterior do SQL Server R Services, poderá receber um erro semelhante a este:

*Você está executando a versão 9.0.0 do Cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

A ferramenta **SqlBindR.exe** é fornecida no Microsoft R Server versão 9.0 para dar suporte à atualização de instâncias do SQL Server para uma versão 9.0 compatível. O suporte à atualização de instâncias do R Services para o 9.0 será adicionado no SQL Server como parte de uma versão de serviço futura. Versões que são candidatas à atualização futura incluem o SQL Server 2016 RTM CU3+ e SP1+, bem como o SQL Server vNext CTP 1.1. 

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>A instalação de versões de serviço do SQL Server 2016 poderá falhar ao instalar versões mais novas dos componentes do R

Quando você instala uma atualização cumulativa ou um service pack para o SQL Server 2016 em um computador que não está conectado à Internet, o assistente de instalação poderá falhar ao exibir o aviso que permite atualizar os componentes do R usando os arquivos CAB baixados. Normalmente, isso ocorre quando vários componentes são instalados juntos com o mecanismo de banco de dados.
 
Como alternativa, você pode instalar a versão de serviço usando a linha de comando e especificando o argumento /MRCACHEDIRECTORY, conforme mostrado neste exemplo para o CU1: 

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obter os últimos arquivos CAB, consulte [Instalando os componentes do R sem acesso à Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).

### <a name="windows-group-created-for-launchpad-must-have-an-account-in-the-sql-server-instance"></a>O grupo do Windows criado para o Launchpad deve ter uma conta na instância do SQL Server
 Durante a instalação do SQL Server R Services, um grupo de usuários do Windows é criado com o nome padrão **SQLRUsers**, que é usado pelo Launchpad Confiável para executar trabalhos do R. Se precisar executar trabalhos do R por meio de um cliente remoto usando a autenticação integrada do Windows, será necessário conceder a esse grupo de usuários do Windows a permissão para fazer logon na instância do SQL Server em que o R está habilitado.

Em um ambiente no qual o grupo **SQLRUsers** não tem essa permissão, os seguintes erros poderão ser exibidos:  
  
-   Quando tentar executar scripts R:  
  
     *Não é possível iniciar o tempo de execução para o script do “R”. Verifique a configuração do tempo de execução do script do R.*  
  
     *Erro de script externo. Não é possível iniciar o tempo de execução.*  
  
-   Erros gerados pelo serviço do [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] :  
  
     *Falha ao inicializar o inicializador RLauncher.dll*  
  
     *Nenhuma dll do inicializador foi registrada!*  
  
-   Os logs de segurança indicam que a conta NT SERVICE\MSSQLLAUNCHPAD está desabilitada para logon.  
 
> [!NOTE]
> Se você executar trabalhos do R no SQL Server Management Studio usando a Memória Compartilhada, só será possível obter essa limitação quando o trabalho do R usar uma chamada ODBC incorporada. 
> 
> Essa solução alternativa não será necessária se você usar logons SQL na estação de trabalho remota.

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>Os serviços do Launchpad não serão iniciados se a versão for diferente da versão do R
Se você instalar o R Services separadamente do mecanismo de banco de dados e as versões forem diferentes, você poderá receber este erro no log de Eventos do Sistema: _Falha de inicialização do Launchpad no SQL Server devido ao seguinte erro: o serviço não respondeu à solicitação de início ou de controle em tempo hábil._

Por exemplo, esse erro poderá ocorrer se você instalar o mecanismo de banco de dados usando a versão de lançamento, aplicar um patch para atualizar o mecanismo de banco de dados e, em seguida, adicionar o R Services usando a versão de lançamento.

Para evitar esse problema, verifique se todos os componentes têm o mesmo número de versão. Se você atualizar um componente, lembre-se de aplicar a mesma atualização a todos os outros componentes instalados.

Para exibir uma lista dos números de versão do R necessários para cada versão do SQL Server 2016, consulte [Instalando os componentes do R sem acesso à Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).


### <a name="service-account-for-launchpad-requires-permission-replace-process-level-token"></a>A conta de serviço do Launchpad exige a permissão Substituir Token no Nível de Processo
 Durante a instalação do SQL Server R Services, o Launchpad Confiável é iniciado usando a conta NT Service\MSSQLLaunchpad, que, por padrão, é provisionada com as permissões necessárias. No entanto, se você estiver usando uma conta diferente ou alterar os privilégios associados a essa conta, o Launchpad poderá falhar ao ser iniciado.
 
 Para garantir que a conta de serviço do Launchpad possa fazer logon, conceda à conta o privilégio: `Replace Process Level Token`. Para obter mais informações, consulte [Substituir um token no nível de processo](https://technet.microsoft.com/itpro/windows/keep-secure/replace-a-process-level-token).

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>Contextos de computação remota bloqueados pelo firewall nas instâncias do SQL Server em execução em Máquinas Virtuais do Microsoft Azure  
 Se você tiver instalado o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em uma Máquina Virtual do Windows Azure, não será possível usar os contextos de computação que exigem o uso do espaço de trabalho da máquina virtual. O motivo é que, por padrão, o firewall da VM do Azure inclui uma regra de bloqueio para o acesso de rede das contas de usuários locais de R.  
  
 Como alternativa, abra o **Firewall do Windows com Segurança Avançada**na VM do Azure, escolha **Regras de Saída**e desabilite a seguinte regra: "Bloquear acesso de rede para contas de usuário locais do R na instância MSSQLSERVER do SQL Server".  
  
### <a name="implied-authentication-in-sqlexpress"></a>Autenticação implícita em SQLEXPRESS
Quando você executar trabalhos do R em uma estação de trabalho de ciência de dados remota usando a autenticação integrada do Windows, o SQL Server usará a *autenticação implícita* para gerar as chamadas ODBC locais que poderão ser exigidas pelo script. No entanto, esse recurso não funcionou no build RTM do SQL Server Express Edition. 

Para corrigir o problema, recomendamos atualizar para uma versão de serviço posterior.

Se não for possível atualizá-la, use um logon SQL para executar trabalhos remotos do R que podem exigir chamadas ODBC incorporadas. 

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Limitações na afinidade do processador para trabalhos do R 
 
No build RTM do SQL Server 2016, você podia definir a afinidade do processador somente para CPUs no primeiro grupo k. Por exemplo, se o servidor for um computador de dois soquetes com dois grupos k, apenas os processadores do primeiro grupo k serão usados para os processos do R. A mesma limitação se aplica ao configurar a governança de recursos para trabalhos de script do R.

Esse problema é corrigido no SQL Server 2016 Service Pack 1.

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>Não é possível fazer alterações nos tipos de coluna durante a leitura de dados em um contexto de computação do SQL Server

Se o contexto de computação estiver definido como a instância do SQL Server, não será possível usar o argumento _colClasses_ (ou outros argumentos semelhante) para alterar o tipo de dados das colunas no código R. 

Por exemplo, a seguinte instrução resultará em um erro se a coluna CRSDepTimeStr ainda não for um inteiro:

~~~~
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
~~~~

Esse problema será corrigido em uma versão posterior. 

Como alternativa, você pode reescrever a consulta SQL para usar CAST ou CONVERT e apresentar os dados ao R usando o tipo de dados correto. Em geral, é melhor para o desempenho trabalhar com os dados usando o SQL em vez de alterar dados no código R.
  
### <a name="resource-governance-default-values"></a>Valores padrão de governança de recursos  
No Enterprise Edition, você pode usar pools de recursos para gerenciar processos de script externo. Em alguns builds, a memória máxima que podia ser alocada para os processos do R era de 20%. Portanto, se o servidor tinha 32 GB de RAM, os executáveis do R (RTerm.exe e BxlServer.exe) podiam usar um máximo de 6,4 GB em uma única solicitação. 

Se você tiver limitações de recursos, verifique o padrão atual e se 20% não for suficiente, consulte a documentação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para saber como alterar esse valor.  

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversiontokenssnoversionmdmd-compute-context"></a>Evitar a limpeza dos espaços de trabalho ao executar o código R em um contexto de computação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Se você usar o comando do R para limpar o espaço de trabalho de objetos durante a execução de código R em um contexto de computação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou se limpar o espaço de trabalho como parte de um script do R chamado pelo uso de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), você poderá receber este erro: *objeto da estação de trabalho “revoScriptConnection” não encontrado*

O `revoScriptConnection` é um objeto no espaço de trabalho do R que contém informações sobre uma sessão do R chamada por meio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, se o código R incluir um comando para limpar o espaço de trabalho (como `rm(list=ls()))`), todas as informações sobre a sessão e outros objetos no espaço de trabalho do R também serão limpos.

Como alternativa, evite a limpeza indiscriminada de variáveis e outros objetos ao executar o R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Embora a limpeza do espaço de trabalho seja comum ao trabalhar no console do R, ela poderá trazer consequências indesejadas. 

+ Para excluir variáveis específicas, use a função *remove* do R: `remove('name1', 'name2', ...)` 
+ Se houver várias variáveis a serem excluídas, salve os nomes das variáveis temporárias em uma lista e execute a coleta de lixo periódica. 
   
### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Restrições sobre dados que podem ser fornecidos como entrada para um script R  
 O sistema não permite usar os seguintes tipos de resultados de consulta em um script R:  
  
-   Dados de uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] que faz referência às colunas AlwaysEncrypted.  
  
-   Dados de uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] que faz referência à colunas mascaradas.  
  
     Se precisar usar dados mascarados em um script R, uma solução alternativa é copiar os dados em uma tabela temporária e usar esses dados.  
   
  
## <a name="microsoft-r-server-standalone"></a>Microsoft R Server (Autônomo)  
 Esta seção lista problemas específicos à versão autônoma do Microsoft R Server. 
  
### <a name="multiple-r-libraries-and-executables-are-installed-if-you-install-both-standalone-and-in-database"></a>Várias bibliotecas e vários executáveis do R são instalados se a versão Autônoma e no Banco de Dados são instaladas  
 A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui a opção de instalar o Microsoft R Server (Autônomo). A opção Microsoft R Server (Autônomo) pode ser usada no Enterprise Edition para instalar um servidor Autônomo do Windows que dá suporte ao R, mas que não exige interatividade com o SQL Server.    

> [!TIP] Essa opção autônoma **não** é necessária para usar o R com o [!INCLUDE[tsql](../../includes/tsql-md.md)].
> 
> Se você precisar configurar um computador de cliente de ciência de dados que pode se conectar ao [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ou ao Microsoft R Server (Autônomo), recomendamos o uso do [Cliente do Microsoft R](http://go.microsoft.com/fwlink/?LinkId=799768).  

Se você instalar o R Services (no Banco de Dados) e o Microsoft R Server (Autônomo) no mesmo computador, fique ciente de que uma instância separada do R será criada para cada instância do SQL Server que tem o R habilitado, bem como uma instância separada do R para o Microsoft R Server (Autônomo).  Por exemplo, se você tiver instalado a instância padrão e uma instância nomeada, bem como o R Server (Autônomo), você poderá ter três instâncias do R no mesmo computador:  
  
-   **Autônoma:** C:\Arquivos de Programas\Microsoft SQL Server\130\R_SERVER  
  
-   **Instância padrão:** C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES  
  
-   **Instância nomeada:** C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.<nome_da_instância>\R_SERVICES  
  
> [!NOTE] 
> 
> Use as bibliotecas e ferramentas do R associadas a uma instância de banco de dados somente por meio do contexto do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se precisar executar o R usando outras ferramentas do R, lembre-se de fazer referência às bibliotecas do R usadas pelo R Server (Autônomo), que são instaladas por padrão em C:\Arquivos de Programas\Microsoft SQL Server\130\R_SERVER.  

### <a name="performance-limits-when-r-services-libraries-are-called-from-standalone-r-tools"></a>Limites de desempenho quando as bibliotecas do R Services são chamadas por meio de ferramentas autônomas do R

As bibliotecas do R usadas pelo SQL Server R Services são instaladas por padrão em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES. É *possível* chamar as ferramentas e bibliotecas do R instaladas para o SQL Server R Services em um aplicativo externo do R como o RGui. 

No entanto, se você fizer isso, o desempenho será limitado. Por exemplo, mesmo se você tiver comprado o Enterprise Edition do SQL Server, o R será executado no modo single-threaded, caso você execute o código R usando ferramentas externas. O desempenho será superior se você executar o código R iniciando uma conexão do SQL Server e usando [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), que chamará as bibliotecas do R Services para você.

+ Evite chamar as bibliotecas do R usadas pelo SQL Server em ferramentas do R externas. 
+ Se precisar executar o R no computador do SQL Server usando ferramentas externas, será necessário instalar uma instância separada do R e, em seguida, verificar se as ferramentas do R apontam para a nova biblioteca. 
+ Se estiver usando o Enterprise Edition, recomendamos a instalação do Microsoft R Server (Autônomo) no computador do SQL Server. Em seguida, na ferramenta externa usada para executar o código R, faça referência às bibliotecas do R Server, que são instaladas por padrão em C:\Arquivos de Programas\Microsoft SQL Server\<número de versão>\R_SERVER. 

Para obter mais informações, consulte [Criar um R Server autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md).  
  
  
## <a name="general-r-issues"></a>Problemas gerais do R  

 Esta seção lista problemas específicos à conectividade e às ferramentas de desempenho do R.  
  
### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Suporte limitado para tipos de dados SQL em sp_execute_external_script  

 Nem todos os tipos de dados com suporte no SQL podem ser usados no R. Como alternativa, considere a conversão do tipo de dados sem suporte para um tipo de dados com suporte antes de passar os dados para sp_execute_external_script.  
  
 Para obter mais informações, consulte [Trabalhando com tipos de dados do R](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
### <a name="possible-string-corruption"></a>Cadeia de caracteres possivelmente corrompida  

 As viagens de ida e volta de dados de cadeia de caracteres do [!INCLUDE[tsql](../../includes/tsql-md.md)] para R e em seguida para [!INCLUDE[tsql](../../includes/tsql-md.md)] podem resultar em dados corrompidos. Isso ocorre devido às diferentes codificações usadas em R e em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], bem como aos diferentes agrupamentos e linguagens com suporte em R e em [!INCLUDE[tsql](../../includes/tsql-md.md)]. As cadeias de caracteres em codificação não-ASCII podem ser possivelmente tratadas de forma incorreta.  
  
 Ao enviar dados de cadeia de caracteres para R, converta-os, se possível, em uma representação de ASCII.  
  
### <a name="only-one-raw-value-can-be-returned-from-spexecuteexternalscript"></a>O sistema pode retornar apenas um valor bruto em sp_execute_external_script  

 Quando um tipo de dados binário é retornado de R (o tipo de dados **raw** de R), o valor deve corresponder ao valor do quadro de saída.  
  
 Adicionaremos suporte para várias saídas **raw** em versões futuras.  
  
 A única solução possível, caso pretenda usar vários conjuntos de saída, é fazer várias chamadas do procedimento armazenado e enviar os conjuntos de resultados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o ODBC.  
  
 Observe que é possível retornar valores de parâmetro junto com os resultados do procedimento armazenado apenas adicionando a palavra-chave OUTPUT. Para obter mais informações, consulte [Retornando dados usando parâmetros OUTPUT](https://technet.microsoft.com/library/ms187004.aspx).
  
### <a name="loss-of-precision"></a>Perda de precisão  

 O [!INCLUDE[tsql](../../includes/tsql-md.md)] e R dão suporte a diferentes tipos de dados; portanto, os tipos de dados numéricos podem sofrer perda de precisão durante a conversão.  
  
 Para obter mais informações sobre a conversão implícita de tipos de dados, consulte [Working with R Data Types](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
### <a name="variable-scoping-error-the-sample-data-set-for-the-analysis-has-no-variables-when-using-the-transformfunc-parameter"></a>Erro de escopo de variável "O conjunto de dados de amostra para a análise não apresenta variáveis" durante o uso do parâmetro transformFunc  

 Você pode passar um argumento *transfoumFunc* em uma função, como `rxLinmod` ou `rxLogit` to transfoum the data while modelling. No entanto, as chamadas de função aninhadas podem gerar erros de escopo no contexto de computação do SQL Server, mesmo que as chamadas funcionem corretamente no contexto de computação local.  
  
 Por exemplo, digamos que você define duas funções `f` e `g` no ambiente global local e `g` chama `f`. Nas chamadas distribuídas ou remotas envolvendo `g`, a chamada para `g` pode falhar porque `f` não pode ser encontrado, mesmo se você passar `f` e `g` para a chamada remota.  
  
 Para contornar esse problema, caso o encontre, incorpore a definição de `f` em qualquer local dentro da sua definição de `g`, antes que `g` possa chamar `f`normalmente.  
  
 Por exemplo:  
  
```  
f <- function(x) { 2*x + 3 }  
g <- function(y) {   
              a <- 10 * y  
               f(a)  
}  
  
```  
  
 Para evitar o erro, reescreva como:  
  
```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

  
## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open 
 
 Esta seção lista problemas específicos à conectividade, ao desenvolvimento e às ferramentas de desempenho do R fornecidas pela Revolution Analytics. Essas ferramentas foram fornecidas em versões de pré-lançamento anteriores do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 

Em geral, recomendamos a desinstalação dessas versões anteriores e a instalação da última versão do SQL Server R Services, Microsoft R Server ou Cliente do Microsoft R.
  
### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Versões do Revolution R Enterprise em execução lado a lado  

 Não há suporte para a instalação do Revolution R Enterprise lado a lado com nenhuma versão do [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)].  
  
 Se tiver uma licença para usar uma versão diferente do Revolution R Enterprise, coloque-a em um computador separado, na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e na estação de trabalho que pretende usar para se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="limited-support-for-revoscaler-rxexec"></a>Suporte limitado para RevoScaleR rxExec  

 A partir do RC0, a função `rxExec` fornecida pelo [!INCLUDE[rsql_rre-short](../../includes/rsql-rre-short-md.md)] pode ser usada apenas no modo de thread único.  
  
 O paralelismo para o `rxExec` em vários processos será adicionado em uma versão futura.  
  
### <a name="data-import-and-manipulation-using-revoscaler"></a>Importação e manipulação de dados usando o RevoScaleR  

 Durante a leitura de colunas **varchar** em um banco de dados, o sistema retira um espaço em branco. Para evitar isso, coloque as cadeias de caracteres entre caracteres de espaço não em branco.  
  
 Quando usar funções, como `rxDataStep` , para criar tabelas de bancos de dados com colunas **varchar** , a largura da coluna é calculada com base em uma amostra dos dados. Se a largura for variável, pode ser necessário preencher todas as cadeias de caracteres com um comprimento comum.  
  
 O uso de uma transformação para alterar o tipo de dados de uma variável não terá suporte quando chamadas repetidas para `rxImport` ou `rxTextToXdf` sejam usadas para importar e anexar linhas, combinando vários arquivos de entrada em um único arquivo .xdf.  
  
### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>Aumentar o tamanho máximo do parâmetro para dar suporte à função rxGetVarInfo  

 Se usar conjuntos de dados com um número muito grande de variáveis (por exemplo, mais de 40.000), defina o sinalizador `max-ppsize` quando iniciar R para usar funções, como `rxGetVarInfo`.  O sinalizador `max-ppsize` especifica o tamanho máximo da pilha de proteção do ponteiro.  
  
 Se estiver usando o console de R, por exemplo, em rgui.exe ou em rterm.exe, você pode definir o valor máximo de max-ppsize em 500000 digitando:  
  
```  
R --max-ppsize=500000  
```  
  
 Se estiver usando o ambiente [!INCLUDE[rsql_developr](../../includes/rsql-developr-md.md)] , você pode definir o sinalizador `max-ppsize` fazendo a seguinte chamada para o executável RevoIDE:  
  
```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  
  
### <a name="issues-with-rxdtree-function"></a>Problemas com a função rxDTree  

 Atualmente, a função `rxDTree` não tem suporte para transformações dentro da fórmula. Não temos suporte para o uso da sintaxe `F()` , em especial, para a criação de fatores dinâmicos. No entanto, os dados numéricos serão compartimentalizados automaticamente.  
  
 Os fatores ordenados são tratados da mesma forma que os fatores de todas as funções de análise RevoScaleR, exceto o `rxDTree`.  
  
### <a name="using-the-r-productivity-environment"></a>Usando o R Productivity Environment  

Algumas versões de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluíram um ambiente de desenvolvimento do R para o Windows criado pela Revolution Analytics. 

No entanto, para compatibilidade com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], é altamente recomendável a instalação do Cliente do Microsoft R ou do Microsoft R Server em vez das ferramentas da Revolution Analytics. As [ferramentas do R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) são outro cliente recomendado que dá suporte às soluções do Microsoft R.
  
### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Problemas de compatibilidade com o driver ODBC do SQLite e o RevoScaleR  
 A revisão 0.92 do driver ODBC do SQLite é incompatível com o RevoScaleR; as revisões de 0.88 a 0.91, 0.93 e posteriores são compatíveis.  
  
## <a name="see-also"></a>Consulte também  
[Novidades no SQL Server 2016](../../sql-server/what-s-new-in-sql-server-2016.md)
  