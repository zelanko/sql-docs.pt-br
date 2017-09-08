---
title: "Problemas conhecidos para serviços de aprendizado de máquina | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 53
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7b9d53a87490e83f888b47b1cff87191b9693a8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="known-issues-for-machine-learning-services"></a>Problemas conhecidos para serviços de aprendizado de máquina

Este tópico descreve problemas conhecidos ou limitações com componentes que são fornecidos como uma opção no SQL Server 2016 e no SQL Server 2017 de aprendizado de máquina.

Aplica-se a todos os itens a seguir, a menos que especificamente indicado:

+ SQL Server 2016

  - R Services (no banco de dados)
  - Microsoft R Server (Autônomo)

+ SQL Server 2017

  - Serviços de R (no banco de dados) de aprendizado de máquina
  - Serviços para Python (no banco de dados) de aprendizado de máquina
  - Servidor do Machine Learning (Autônomo)

## <a name="setup-and-configuration-issues"></a>Problemas de instalação e configuração

Uma descrição de perguntas processadas e comuns relacionada à configuração inicial e configuração estão listados aqui: [atualização e instalação perguntas frequentes sobre](r/upgrade-and-installation-faq-sql-server-r-services.md).

Também consulte este artigo para obter informações sobre atualizações, a instalação lado a lado e a instalação de novos componentes de R ou Python.

### <a name="unable-to-install-python-components-in-in-offline-installs-of-sql-server-2017"></a>Não é possível instalar componentes Python em instalações offline de 2017 do SQL Server

Se você instalar o SQL Server 2017 em um computador sem acesso à Internet, o instalador pode falhar exibir a página que solicita a localização dos componentes do Python baixados; Portanto, você poderá instalar o recurso Serviços de aprendizado de máquina, mas não os componentes do Python.

Esse problema será corrigido em uma versão futura. Como alternativa, você pode habilitar temporariamente o acesso à Internet durante a instalação. Essa limitação não se aplica a R.

**Aplica-se a:** SQL Server 2017 com Python

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Instalar a última versão do serviço para garantir a compatibilidade com o Cliente do Microsoft R

Se você instalar a versão mais recente do cliente do Microsoft R e usá-lo para executar R contexto de computação do SQL Server usando um controle remoto, você poderá receber um erro semelhante ao seguinte:

*Você está executando 9.x.x de versão do cliente do Microsoft R no seu computador, que é incompatível com o Microsoft R Server versão 8.x.x. Baixe e instale uma versão compatível.*

SQL Server 2016 necessário que as bibliotecas de R no cliente correspondem exatamente as bibliotecas de R no servidor. Se a restrição foi removida para versões mais tarde do que R Server 9.0.1. No entanto, se você encontrar esse erro, verifique se a versão das bibliotecas de R usados pelo cliente e servidor, nad se necessário, atualize o cliente para corresponder à versão do servidor.

A versão do R que é instalado com o SQL Server R Services é atualizada sempre que uma versão de serviço do SQL Server está instalada. Portanto, para garantir que você sempre tenha as versões mais recentes dos componentes de R, você deve instalar todos os service packs.

Para compatibilidade com o Cliente do Microsoft R 9.0.0, é necessário instalar as atualizações descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).

Para evitar problemas com pacotes de R, você também pode atualizar a versão das bibliotecas de R que estão instalados no servidor, alterando-se para a política de ciclo de vida modernos conforme descrito em [nesta seção](#bkmk_sqlbindr). Quando você fizer isso, a versão de R instalado com o SQL Server é atualizada na mesma agenda que as atualizações são publicadas para o Microsoft R Server, garantindo que cliente e servidor podem sempre tenha as versões mais recentes do Microsoft R.

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="bkmk_sqlbindr"></a>Aviso de versão incompatível ao conectar-se a versão mais antiga do SQL Server R Services de um cliente usando o[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Se você tiver instalado o Microsoft R Server em um computador cliente usando o assistente de instalação do [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] ou o novo instalador autônomo para o [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)e estiver executando o código R em um contexto de computação que usa uma versão anterior do SQL Server R Services, poderá receber um erro semelhante a este:

*Você está executando a versão 9.0.0 do Cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

A ferramenta **SqlBindR.exe** é fornecida no Microsoft R Server versão 9.0 para dar suporte à atualização de instâncias do SQL Server para uma versão 9.0 compatível. O suporte à atualização de instâncias do R Services para o 9.0 será adicionado no SQL Server como parte de uma versão de serviço futura. Versões que são candidatos para a atualização futura incluem SQL Server 2016 RTM CU3 + e SP1 + e SQL Server 2017 CTP 1.1.

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>A instalação de versões de serviço do SQL Server 2016 poderá falhar ao instalar versões mais novas dos componentes do R

Quando você instala uma atualização cumulativa ou um service pack para o SQL Server 2016 em um computador que não está conectado à Internet, o assistente de instalação poderá falhar ao exibir o aviso que permite atualizar os componentes do R usando os arquivos CAB baixados. Normalmente, isso ocorre quando vários componentes são instalados juntos com o mecanismo de banco de dados.

Como alternativa, você pode instalar a versão de serviço usando a linha de comando e especificando o */MRCACHEDIRECTORY* argumento conforme mostrado neste exemplo, que instala atualizações CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obter os instaladores mais recentes, consulte [instalando os componentes de aprendizado de máquina sem acesso à Internet](r/installing-ml-components-without-internet-access.md).

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>Os serviços do Launchpad não serão iniciados se a versão for diferente da versão do R

Se você instala o R Services separadamente do mecanismo de banco de dados e as versões de compilação forem diferentes, você poderá ver esse erro no log de eventos do sistema: _o Launchpad do SQL Server service não pôde ser iniciado devido ao seguinte erro: O serviço não Responda à solicitação de início ou controle de maneira oportuna._

Por exemplo, esse erro poderá ocorrer se você instalar o mecanismo de banco de dados usando a versão de lançamento, aplicar um patch para atualizar o mecanismo de banco de dados e, em seguida, adicionar o R Services usando a versão de lançamento.

Para evitar esse problema, verifique se todos os componentes têm o mesmo número de versão. Se você atualizar um componente, lembre-se de aplicar a mesma atualização a todos os outros componentes instalados.

Para exibir uma lista dos números de versão do R necessários para cada versão do SQL Server 2016, consulte [Instalando os componentes do R sem acesso à Internet](r/installing-ml-components-without-internet-access.md).

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>Contextos de computação remota bloqueados pelo firewall nas instâncias do SQL Server em execução em Máquinas Virtuais do Microsoft Azure

Se você tiver instalado o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] em uma Máquina Virtual do Windows Azure, não será possível usar os contextos de computação que exigem o uso do espaço de trabalho da máquina virtual. O motivo é que, por padrão, o firewall da VM do Azure inclui uma regra de bloqueio para o acesso de rede das contas de usuários locais de R.

Como alternativa, abra o **Firewall do Windows com Segurança Avançada**na VM do Azure, escolha **Regras de Saída**e desabilite a seguinte regra: "Bloquear acesso de rede para contas de usuário locais do R na instância MSSQLSERVER do SQL Server".

### <a name="implied-authentication-in-sqlexpress"></a>Autenticação implícita em SQLEXPRESS

Quando você executar trabalhos do R em uma estação de trabalho de ciência de dados remota usando a autenticação integrada do Windows, o SQL Server usará a *autenticação implícita* para gerar as chamadas ODBC locais que poderão ser exigidas pelo script. No entanto, esse recurso não funcionou no build RTM do SQL Server Express Edition.

Para corrigir o problema, recomendamos atualizar para uma versão de serviço posterior.

Se não for possível atualizá-la, use um logon SQL para executar trabalhos remotos do R que podem exigir chamadas ODBC incorporadas.

**Aplica-se a:** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-r-libraries-are-called-from-standalone-r-tools"></a>Limites de desempenho quando bibliotecas de R são chamadas de ferramentas autônomas R

É possível chamar as ferramentas de R e bibliotecas que são instaladas para o SQL Server R Services de um aplicativo externo de R como RGui. Isso pode ser útil quando você estiver instalando novos pacotes, ou executando testes ad hoc em exemplos de código muito curto.

No entanto, lembre-se de que fora do SQL Server, desempenho será limitado. Por exemplo, mesmo se você tiver comprado o Enterprise Edition do SQL Server, R será executado no modo de thread único, quando você executar o código de R usando ferramentas externas. O desempenho será melhor se você executar seu código R iniciando uma conexão do SQL Server e usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), que chamará bibliotecas de R para você.

+ Evite chamar as bibliotecas do R usadas pelo SQL Server em ferramentas do R externas.
+ Se você precisar executar código R extensivo no computador do SQL Server sem usar o SQL server, instale uma instância separada do R, como o cliente do Microsoft R e, em seguida, verifique se as ferramentas de desenvolvimento R apontam para a nova biblioteca.

Para obter mais informações, consulte [Criar um R Server autônomo](r/create-a-standalone-r-server.md).

### <a name="r-script-throttled-due-to-resource-governance-default-values"></a>Script de R limitado devido a valores de padrão de controle de recursos

No Enterprise Edition, você pode usar pools de recursos para gerenciar processos de script externo. Em alguns compilações de versão anteriores, a memória máxima que pode ser alocada para os processos de R foi 20%. Portanto, se o servidor tinha 32 GB de RAM, os executáveis do R (RTerm.exe e BxlServer.exe) podiam usar um máximo de 6,4 GB em uma única solicitação.

Se você tiver limitações de recursos, verifique o padrão atual e se 20% não for suficiente, consulte a documentação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para saber como alterar esse valor.

**Aplica-se a:** R Services do SQL Server 2016, Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>A execução de código R e o pacote ou problemas de função

Esta seção contém os problemas conhecidos que são específicos à execução de R no SQL Server, bem como alguns problemas relacionados a bibliotecas de R e ferramentas publicadas pela Microsoft, incluindo o RevoScaleR.

Para mais problemas conhecidos que podem afetar a soluções de R, consulte o site do Microsoft R Server: [problemas conhecidos com o Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-known-issues)

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Limitações na afinidade do processador para trabalhos do R

Na compilação de versão inicial do SQL Server 2016, você pode definir a afinidade do processador somente para CPUs no primeiro grupo de k. Por exemplo, se o servidor for um computador de dois soquetes com dois grupos k, apenas os processadores do primeiro grupo k serão usados para os processos do R. A mesma limitação se aplica ao configurar a governança de recursos para trabalhos de script do R.

Esse problema é corrigido no SQL Server 2016 Service Pack 1.

**Aplica-se a:** versão RTM do SQL Server 2016 R Services

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

**Aplica-se a:** SQL Server 2016 R Services

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>Evitar a limpeza dos espaços de trabalho ao executar o código R em um contexto de computação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Se você usar o comando do R para limpar o espaço de trabalho de objetos durante a execução de código R em um contexto de computação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou se limpar o espaço de trabalho como parte de um script do R chamado pelo uso de [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), você poderá receber este erro: *objeto da estação de trabalho “revoScriptConnection” não encontrado*

O`revoScriptConnection` é um objeto no espaço de trabalho do R que contém informações sobre uma sessão do R chamada por meio de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, se o código R incluir um comando para limpar o espaço de trabalho (como `rm(list=ls()))`), todas as informações sobre a sessão e outros objetos no espaço de trabalho do R também serão limpos.

Como alternativa, evite a limpeza indiscriminada de variáveis e outros objetos ao executar o R no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Embora a limpeza do espaço de trabalho seja comum ao trabalhar no console do R, ela poderá trazer consequências indesejadas.

+ Para excluir variáveis específicas, use a função *remove* do R: `remove('name1', 'name2', ...)`
+ Se houver várias variáveis a serem excluídas, salve os nomes das variáveis temporárias em uma lista e execute a coleta de lixo periódica.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Restrições sobre dados que podem ser fornecidos como entrada para um script R

O sistema não permite usar os seguintes tipos de resultados de consulta em um script R:

- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência às colunas AlwaysEncrypted.
  
- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência à colunas mascaradas.
  
     Se precisar usar dados mascarados em um script R, uma solução alternativa é copiar os dados em uma tabela temporária e usar esses dados.

### <a name="arguments-varstokeep-and-varstodrop-not-supported-for-sql-server-data-sources"></a>Argumentos *varsToKeep* e *varsToDrop* não tem suporte para fontes de dados do SQL Server

Quando você usa a função rxDataStep para gravar os resultados em uma tabela, usando o *varsToKeep* e *varsToDrop* é uma maneira útil de especificar as colunas a serem incluídos ou excluídos como parte da operação. Atualmente, esses argumentos não têm suporte para fontes de dados do SQL Server.

Essa limitação será removida em uma versão posterior.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Suporte limitado para tipos de dados SQL em`sp_execute_external_script`

Nem todos os tipos de dados com suporte no SQL podem ser usados no R. Como alternativa, considere a conversão do tipo de dados sem suporte para um tipo de dados com suporte antes de passar os dados para sp_execute_external_script.

Para obter mais informações, consulte [tipos de dados e bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="possible-string-corruption"></a>Cadeia de caracteres possivelmente corrompida

As viagens de ida e volta de dados de cadeia de caracteres do [!INCLUDE[tsql](../includes/tsql-md.md)] para R e em seguida para [!INCLUDE[tsql](../includes/tsql-md.md)] podem resultar em dados corrompidos. Isso ocorre devido às diferentes codificações usadas em R e em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], bem como aos diferentes agrupamentos e linguagens com suporte em R e em [!INCLUDE[tsql](../includes/tsql-md.md)]. As cadeias de caracteres em codificação não-ASCII podem ser possivelmente tratadas de forma incorreta.

Ao enviar dados de cadeia de caracteres para R, converta-os, se possível, em uma representação de ASCII.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>Apenas um valor do tipo `raw` pode ser retornado de`sp_execute_external_script`

Quando um tipo de dados binário é retornado de R (o tipo de dados **raw** de R), o valor deve corresponder ao valor do quadro de saída.

Adicionaremos suporte para várias saídas **raw** em versões futuras.

A única solução possível, caso pretenda usar vários conjuntos de saída, é fazer várias chamadas do procedimento armazenado e enviar os conjuntos de resultados para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o ODBC.

Observe que é possível retornar valores de parâmetro junto com os resultados do procedimento armazenado apenas adicionando a palavra-chave OUTPUT. Para obter mais informações, consulte [Retornando dados usando parâmetros OUTPUT](https://technet.microsoft.com/library/ms187004.aspx).

### <a name="loss-of-precision"></a>Perda de precisão

O[!INCLUDE[tsql](../includes/tsql-md.md)] e R dão suporte a diferentes tipos de dados; portanto, os tipos de dados numéricos podem sofrer perda de precisão durante a conversão.

Para obter mais informações sobre a conversão implícita de tipos de dados, consulte [Working with R Data Types](r/r-libraries-and-data-types.md).

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


Para evitar o erro, reescreva como segue:

```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

### <a name="data-import-and-manipulation-using-revoscaler"></a>Importação e manipulação de dados usando o RevoScaleR

Durante a leitura de colunas **varchar** em um banco de dados, o sistema retira um espaço em branco. Para evitar isso, coloque as cadeias de caracteres entre caracteres de espaço não em branco.

Quando usar funções, como `rxDataStep` , para criar tabelas de bancos de dados com colunas **varchar** , a largura da coluna é calculada com base em uma amostra dos dados. Se a largura for variável, pode ser necessário preencher todas as cadeias de caracteres com um comprimento comum.

O uso de uma transformação para alterar o tipo de dados de uma variável não terá suporte quando chamadas repetidas para `rxImport` ou `rxTextToXdf` sejam usadas para importar e anexar linhas, combinando vários arquivos de entrada em um único arquivo .xdf.

### <a name="limited-support-for-rxexec"></a>Suporte limitado para rxExec

No SQL Server 2016, o `rxExec` função fornecida pelo pacote RevoScaleR pode ser usada apenas no modo de thread único.

O paralelismo para o `rxExec` em vários processos será adicionado em uma versão futura.

### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>Aumentar o tamanho máximo do parâmetro para dar suporte à função rxGetVarInfo

Se usar conjuntos de dados com um número muito grande de variáveis (por exemplo, mais de 40.000), defina o sinalizador `max-ppsize` quando iniciar R para usar funções, como `rxGetVarInfo`.  O sinalizador `max-ppsize` especifica o tamanho máximo da pilha de proteção do ponteiro.

Se estiver usando o console de R, por exemplo, em rgui.exe ou em rterm.exe, você pode definir o valor máximo de max-ppsize em 500000 digitando:

```  
R --max-ppsize=500000  
```  
  
Se estiver usando o ambiente [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] , você pode definir o sinalizador `max-ppsize` fazendo a seguinte chamada para o executável RevoIDE:

```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  

### <a name="issues-with-the-rxdtree-function"></a>Problemas com a função rxDTree

Atualmente, a função `rxDTree` não tem suporte para transformações dentro da fórmula. Não temos suporte para o uso da sintaxe `F()` , em especial, para a criação de fatores dinâmicos. No entanto, os dados numéricos serão compartimentalizados automaticamente.

Os fatores ordenados são tratados da mesma forma que os fatores de todas as funções de análise RevoScaleR, exceto o `rxDTree`.

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open

Esta seção lista problemas específicos à conectividade, ao desenvolvimento e às ferramentas de desempenho do R fornecidas pela Revolution Analytics. Essas ferramentas foram fornecidas em versões de pré-lançamento anteriores do  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. 

Em geral, é recomendável que você desinstale essas versões anteriores e instala a versão mais recente do SQL Server ou Microsoft R Server.

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Versões do Revolution R Enterprise em execução lado a lado

Não há suporte para a instalação do Revolution R Enterprise lado a lado com nenhuma versão do [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] .

Se tiver uma licença para usar uma versão diferente do Revolution R Enterprise, coloque-a em um computador separado, na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e na estação de trabalho que pretende usar para se conectar à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

### <a name="use-of-r-productivity-environment-not-supported"></a>Uso de R Productivity Environment não tem suportada

Algumas versões de pré-lançamento do [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluíram um ambiente de desenvolvimento do R para o Windows criado pela Revolution Analytics. Essa ferramenta não é mais fornecida e não tem suporte.

Para compatibilidade com [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], é altamente recomendável que você instale o cliente do Microsoft R ou o Microsoft R Server em vez de ferramentas da Revolution Analytics. As[ferramentas do R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) são outro cliente recomendado que dá suporte às soluções do Microsoft R.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Problemas de compatibilidade com o driver ODBC do SQLite e o RevoScaleR

A revisão 0.92 do driver ODBC do SQLite é incompatível com o RevoScaleR; as revisões de 0.88 a 0.91, 0.93 e posteriores são compatíveis.

## <a name="see-also"></a>Consulte também

[Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)


