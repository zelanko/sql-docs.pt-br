---
title: "Problemas conhecidos de serviços de aprendizado de máquina | Microsoft Docs"
ms.date: 01/19/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: "53"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 197bfc48d000246b59b983fbf890e998cc2b5beb
ms.sourcegitcommit: d7dcbcebbf416298f838a39dd5de6a46ca9f77aa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="known-issues-in-machine-learning-services"></a>Problemas conhecidos nos serviços de aprendizado de máquina

Este artigo descreve problemas conhecidos ou limitações com componentes que são fornecidos como uma opção no SQL Server 2016 e no SQL Server 2017 de aprendizado de máquina.

As informações aqui se aplica a todos os itens a seguir, a menos que indicado o contrário:

* SQL Server 2016

  - R Services (no Banco de Dados)
  - Microsoft R Server (Autônomo)

* SQL Server 2017

  - Serviços de R (no banco de dados) de aprendizado de máquina
  - Serviços para Python (no banco de dados) de aprendizado de máquina
  - Servidor do Machine Learning (Autônomo)

## <a name="setup-and-configuration-issues"></a>Problemas de instalação e configuração

Para obter uma descrição dos processos e perguntas comuns relacionadas à configuração inicial e a configuração, consulte [perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md). Ele contém informações sobre atualizações, a instalação lado a lado e a instalação de novos componentes de R ou Python.

### <a name="unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>Não é possível instalar os recursos de aprendizado de máquina do SQL Server em um controlador de domínio

Se você tentar instalar o SQL Server 2016 R Services ou serviços de aprendizado de máquina do SQL Server 2017 em um controlador de domínio, a instalação falha, com esses erros:

>*"Ocorreu um erro durante o processo de instalação do recurso."*
> 
>*"Não é possível localizar o grupo com identidade..."*
> 
>*"Código de erro do componente: 0x80131509"*

A falha ocorre porque, em um controlador de domínio, o serviço não é possível criar as 20 contas locais necessárias para executar o aprendizado de máquina. Em geral, não recomendamos a instalação do SQL Server em um controlador de domínio. Para obter mais informações, consulte [boletim suporte 2032911](https://support.microsoft.com/en-us/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Instalar a versão mais recente do serviço para garantir a compatibilidade com o cliente do Microsoft R

Se você instala a versão mais recente do cliente do Microsoft R e usá-lo para executar R no SQL Server em um contexto de computação remota, você poderá receber um erro semelhante ao seguinte:

>*Você está executando a versão 9.x.x do cliente do Microsoft R no seu computador, que é incompatível com o Microsoft R Server versão 8.x.x. Baixe e instale uma versão compatível.*

SQL Server 2016 requer que as bibliotecas de R no cliente correspondem exatamente as bibliotecas de R no servidor. A restrição foi removida para versões mais tarde do que R Server 9.0.1. No entanto, se você encontrar esse erro, verifique se a versão das bibliotecas de R que é usada pelo seu cliente e o servidor e, se necessário, atualize o cliente para corresponder à versão do servidor.

A versão do R que é instalado com o SQL Server R Services é atualizada sempre que uma versão de serviço do SQL Server está instalada. Para garantir que você sempre tenha as versões mais recentes dos componentes de R, certifique-se de instalar todos os service packs.

Para garantir a compatibilidade com o cliente do Microsoft R 9.0.0, instalar as atualizações que estão descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).

Para evitar problemas com pacotes de R, você também pode atualizar a versão das bibliotecas de R que estão instalados no servidor, alterando seu contrato de serviço para usar a política de suporte do ciclo de vida moderno, conforme descrito em [a próxima seção](#bkmk_sqlbindr). Quando você fizer isso, a versão do R que é instalado com o SQL Server é atualizada na mesma agenda usada para as atualizações da máquina de servidor de aprendizado (anteriormente Microsoft R Server).

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>Não é possível instalar componentes do Python em offline instalações do SQL Server de 2017 CTP 2.0 ou posterior

Se você instalar uma versão de pré-lançamento do SQL Server 2017 em um computador sem acesso à internet, o instalador pode falhar exibir a página que solicita a localização dos componentes do Python baixados. Nesse caso, você pode instalar o recurso Serviços de aprendizado de máquina, mas não os componentes do Python.

Esse problema é corrigido na versão de lançamento. Se você encontrar esse problema, como alternativa, você pode habilitar temporariamente o acesso à internet durante a instalação. Essa limitação não se aplica a R.

**Aplica-se a:** SQL Server 2017 com Python

### <a name="bkmk_sqlbindr"></a>Quando você conecta a uma versão mais antiga do SQL Server R Services de um cliente por meio de aviso de versão incompatível[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Quando você executa o código R em um contexto de computação do SQL Server 2016, você verá um erro semelhante ao seguinte:

*Você está executando a versão 9.0.0 do Cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

Esta mensagem é exibida se qualquer uma das duas instruções a seguir for verdadeira,

+ Você instalou o R Server (autônomo) em um computador cliente usando o Assistente para instalação [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
+ Você instalou o Microsoft R Server usando o [separadas do Windows installer](https://docs.microsoft.com/r-server/install/r-server-install-windows).

Para assegurar que o servidor e o cliente usam a mesma versão que você talvez precise usar _associação_, com suporte para o Microsoft R Server 9.0 e versões posteriores, para atualizar os componentes de R em instâncias do SQL Server 2016. Para determinar se há suporte para atualizações disponíveis para sua versão dos serviços do R, consulte [atualizar uma instância dos serviços do R usando SqlBindR.exe](/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>A instalação de versões de serviço do SQL Server 2016 poderá falhar ao instalar versões mais novas dos componentes do R

Quando você instala uma atualização cumulativa ou instala um service pack para SQL Server 2016 em um computador que não está conectado à internet, o Assistente de instalação pode falhar ao exibir o prompt que permite que você atualize os componentes de R usando arquivos CAB baixados. Esta falha ocorre normalmente quando vários componentes foram instalados junto com o mecanismo de banco de dados.

Como alternativa, você pode instalar a versão de serviço usando a linha de comando e especificando o `MRCACHEDIRECTORY` argumento conforme mostrado neste exemplo, que instala atualizações CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obter os instaladores mais recentes, consulte [instalar componentes de aprendizado de máquina sem acesso à internet](r/installing-ml-components-without-internet-access.md).

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>Serviços de barra inicial não será iniciado se a versão for diferente da versão do R

Se você instalar o SQL Server R Services separadamente do mecanismo de banco de dados e as versões de compilação forem diferentes, você verá o seguinte erro no log de eventos do sistema:

>_O serviço do Launchpad do SQL Server não pôde ser iniciado devido ao seguinte erro: O serviço não respondeu à solicitação de início ou controle de maneira oportuna._

Por exemplo, esse erro pode ocorrer se você instalar o mecanismo de banco de dados usando a versão de lançamento, aplicar um patch para atualizar o mecanismo de banco de dados e, em seguida, adicione o recurso Serviços de R usando a versão de lançamento.

Para evitar esse problema, use um utilitário como o Gerenciador de arquivos para comparar as versões do Launchpad.exe com versão dos binários do SQL, como sqldk.dll. Todos os componentes devem ter o mesmo número de versão. Se você atualizar um componente, lembre-se de aplicar a mesma atualização a todos os outros componentes instalados.

Procure a barra inicial no `Binn` pasta para a instância. Por exemplo, em uma instalação padrão do SQL Server 2016, o caminho pode ser "C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn". 

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>Contextos de computação remota estão bloqueados por um firewall em instâncias do SQL Server em execução em máquinas virtuais do Azure

Se você tiver instalado [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] em uma máquina virtual do Windows Azure, você não poderá usar os contextos de computação que exigem o uso de espaço de trabalho da máquina virtual. O motivo é que, por padrão, o firewall em máquinas virtuais do Azure inclui uma regra que bloqueia o acesso para contas de usuário locais do R de rede.

Como alternativa, na VM do Azure, abra **Firewall do Windows com segurança avançada**, selecione **as regras de saída**e desabilitar a regra a seguir: **bloquear o acesso de rede para contas de usuário local do R no A instância do SQL Server MSSQLSERVER**. Você também pode deixar a regra habilitada, mas altere a propriedade de segurança para **permitir se seguro**.

### <a name="implied-authentication-in-sqlexpress"></a>Autenticação implícita em SQLEXPRESS

Quando você executar trabalhos de R de uma estação de trabalho de ciência de dados remota usando a autenticação integrada do Windows, o SQL Server usa *autenticação implícita* para gerar qualquer local chamada ODBC que pode ser necessárias pelo script. No entanto, esse recurso não funcionou no build RTM do SQL Server Express Edition.

Para corrigir o problema, recomendamos atualizar para uma versão de serviço posterior.

Se não for possível atualizá-la, use um logon SQL para executar trabalhos remotos do R que podem exigir chamadas ODBC incorporadas.

**Aplica-se a:** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>Limites de desempenho quando bibliotecas usadas pelo SQL Server são chamadas de outras ferramentas

É possível chamar a bibliotecas que são instaladas para o SQL Server de um aplicativo externo, como RGui de aprendizado de máquina. Isso pode ser a maneira mais conveniente de executar determinadas tarefas, como instalar novos pacotes, ou executando testes ad hoc em exemplos de código muito curto. No entanto, fora do SQL Server, o desempenho pode ser limitado. 

Por exemplo, mesmo se você estiver usando a Enterprise Edition do SQL Server, R é executado no modo de thread único, quando você executa o código de R usando ferramentas externas. Para obter os benefícios de desempenho no SQL Server, iniciar uma conexão do SQL Server e usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para chamar o tempo de execução do script externo.

+ Em geral, evite chamar a bibliotecas que são usadas pelo SQL Server de ferramentas externas de aprendizado de máquina. Se você precisar depurar R ou o código Python, é normalmente mais fácil de fazer isso fora do SQL Server. Para obter as mesmas bibliotecas que estejam no SQL Server, você pode instalar o cliente do Microsoft R ou [Server de aprendizado de máquina](r/create-a-standalone-r-server.md).

### <a name="sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>SQL Server Data Tools não suporta permissões exigidas para scripts externos

Ao usar o Visual Studio ou o SQL Server Data Tools para publicar um projeto de banco de dados, se qualquer entidade tem permissões específicas para a execução do script externo, você poderá receber um erro como este:

"Modelo TSQL: Erro detectado quando o banco de dados de engenharia reversa. A permissão não foi reconhecida e não foi importada."

Atualmente, o modelo de DACPAC não oferece suporte as permissões usadas por serviços de R ou serviços de aprendizado de máquina, como GRANT ANY EXTERNAL SCRIPT ou EXECUTE ANY EXTERNAL SCRIPT. Esse problema será corrigido em uma versão posterior.

Como alternativa, execute a concessão adicional instruções em um script de pós-implantação.

### <a name="external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>Execução do script externo está limitada devido a valores de padrão de controle de recursos

No Enterprise Edition, você pode usar pools de recursos para gerenciar processos de script externo. Em alguns compilações de versão anteriores, a memória máxima que pode ser alocada para os processos de R foi 20 por cento. Portanto, se o servidor tiver 32 GB de RAM, os executáveis de R (RTerm.exe e BxlServer.exe) podem usar um máximo de 6,4 GB em uma única solicitação.

Se você encontrar as limitações de recursos, verifique o padrão atual. Se 20% não seja suficiente, consulte a documentação para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sobre como alterar esse valor.

**Aplica-se a:** R Services do SQL Server 2016, Enterprise Edition

## <a name="r-issues"></a>Problemas de R

Esta seção contém os problemas conhecidos que são específicos à execução de R no SQL Server, bem como alguns problemas relacionados a bibliotecas de R e ferramentas publicadas pela Microsoft, incluindo o RevoScaleR.

Para mais problemas conhecidos que podem afetar a soluções de R, consulte o [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/resources-known-issues) site.

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Limitações na afinidade do processador para trabalhos do R

Na compilação de versão inicial do SQL Server 2016, você pode definir a afinidade do processador somente para CPUs no primeiro grupo de k. Por exemplo, se o servidor for uma máquina de 2 soquetes com dois grupos de k, processadores somente do primeiro grupo k são usados para os processos de R. As mesmas limitações se aplicam quando você configura o controle de recursos para trabalhos de script R.

Esse problema é corrigido no SQL Server 2016 Service Pack 1. É recomendável que você atualize para a versão mais recente do serviço.

**Aplica-se a:** versão RTM do SQL Server 2016 R Services

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>Não é possível fazer alterações nos tipos de coluna durante a leitura de dados em um contexto de computação do SQL Server

Se o contexto de computação estiver definido como a instância do SQL Server, não será possível usar o argumento _colClasses_ (ou outros argumentos semelhante) para alterar o tipo de dados das colunas no código R.

Por exemplo, a seguinte instrução resultará em um erro se a coluna CRSDepTimeStr ainda não for um inteiro:

```r
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

Como alternativa, você pode reescrever a consulta SQL para usar CAST ou converter e apresentar os dados em R usando o tipo de dados correto. Em geral, desempenho é melhor quando você trabalha com dados usando SQL em vez de alteração de dados no código de R.

**Aplica-se a:** SQL Server 2016 R Services

### <a name="limits-on-size-of-serialized-models"></a>Limites de tamanho de modelos serializados

Quando você salvar um modelo em uma tabela do SQL Server, você deve serializar o modelo e salvá-lo em um formato binário. Teoricamente, o tamanho máximo de um modelo que pode ser armazenado com esse método é 2 GB, que é o tamanho máximo de colunas varbinary no SQL Server.

Se você precisar usar modelos mais amplos, soluções alternativas a seguir estão disponíveis:

+ Etapas para reduzir o tamanho do seu modelo. Alguns pacotes de software livre R incluir uma grande quantidade de informações no objeto de modelo, e muitas dessas informações podem ser removida para a implantação. 
+ Use seleção de recursos para remover colunas desnecessárias.
+ Se você estiver usando um algoritmo de software livre, considere uma implementação semelhante usando o algoritmo correspondente em MicrosoftML ou RevoScaleR. Esses pacotes foram otimizados para cenários de implantação.
+ Depois que o modelo tenha sido planejado e o tamanho reduzido usando as etapas anteriores, veja se o [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) função em R base pode ser usada para reduzir o tamanho do modelo antes de passá-lo para o SQL Server. Essa opção é recomendada quando o modelo estiver próximo ao limite de 2 GB.
+ Para modelos mais amplos, você pode usar o SQL Server [FileTable](..\relational-databases\blob\filetables-sql-server.md) para armazenar os modelos de recursos, em vez de usar uma coluna varbinary.

    Para usar FileTables, você deve adicionar uma exceção de firewall, porque os dados armazenados em FileTables são gerenciados pelo driver do sistema de arquivos Filestream no SQL Server e as regras de firewall padrão bloqueiam o acesso de arquivo de rede. Para obter mais informações, consulte [habilitar pré-requisitos para FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md). 

    Depois que você habilitou a FileTable gravar o modelo, que obter um caminho de SQL usando a API de FileTable e, em seguida, gravar o modelo para o local do seu código. Quando você precisar ler o modelo, você obtém o caminho do SQL e, em seguida, chame o modelo usando o caminho do seu script. Para obter mais informações, consulte [acessar FileTables com APIs de arquivo de entrada e saída](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>Evitar limpar espaços de trabalho quando você executar o código R em um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contexto de computação

Se você usar um comando de R para limpar seu espaço de trabalho de objetos durante a execução de código R em uma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computação contexto, ou se você limpar o espaço de trabalho como parte de um script de R chamado usando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), você poderá receber este erro : *revoScriptConnection de objeto do espaço de trabalho não encontrado*

O`revoScriptConnection` é um objeto no espaço de trabalho do R que contém informações sobre uma sessão do R chamada por meio de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, se o código R incluir um comando para limpar o espaço de trabalho (como `rm(list=ls()))`), todas as informações sobre a sessão e outros objetos no espaço de trabalho do R também serão limpos.

Como alternativa, evite limpando indiscriminado de variáveis e outros objetos enquanto você estiver executando o R no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Embora limpar o espaço de trabalho é comum quando trabalha no console de R, ele pode ter consequências não intencionais.

* Para excluir variáveis específicas, use o R `remove` função: por exemplo,`remove('name1', 'name2', ...)`
* Se houver várias variáveis a serem excluídas, salve os nomes das variáveis temporárias em uma lista e execute a coleta de lixo periódica.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Restrições sobre dados que podem ser fornecidos como entrada para um script R

O sistema não permite usar os seguintes tipos de resultados de consulta em um script R:

- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência às colunas AlwaysEncrypted.
  
- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência à colunas mascaradas.
  
     Se precisar usar dados mascarados em um script R, uma solução alternativa é copiar os dados em uma tabela temporária e usar esses dados.

### <a name="use-of-strings-as-factors-can-lead-to-performance-degradation"></a>Uso de cadeias de caracteres como fatores podem levar à degradação do desempenho

Usando variáveis de tipo de cadeia de caracteres como fatores podem aumentar significativamente a quantidade de memória usada para operações de R. Esse é um problema conhecido com R em geral, e há vários artigos sobre o assunto. Por exemplo, consulte [fatores não são objetos de primeira classe em R por João montagem, em R bloggers)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) ou [stringsAsFactors: uma biografia não autorizada, por Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Embora o problema não é específico para o SQL Server, ele pode afetar significativamente o desempenho do código R executado no SQl Server. Cadeias de caracteres geralmente são armazenadas como varchar ou nvarchar e, se uma coluna de dados de cadeia de caracteres tiver muitos valores exclusivos, o processo de converter esses para números inteiros e de volta para cadeias de caracteres por R internamente ainda pode levar a erros de alocação de memória.

Se você não absolutamente requerem um tipo de dados de cadeia de caracteres para outras operações, mapeia os valores de cadeia de caracteres para um numérico (inteiro) tipo de dados como parte da preparação de dados seria útil de uma perspectiva de desempenho e escalabilidade.

Para uma discussão sobre esse problema e outras dicas, consulte [desempenho para serviços do R - otimização dados](r/r-and-data-optimization-r-services.md).

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>Argumentos *varsToKeep* e *varsToDrop* não há suporte para fontes de dados do SQL Server

Quando você usa a função rxDataStep para gravar os resultados em uma tabela, usando o *varsToKeep* e *varsToDrop* é uma maneira útil de especificar as colunas a serem incluídos ou excluídos como parte da operação. No entanto, esses argumentos não há suporte para fontes de dados do SQL Server.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Suporte limitado para tipos de dados SQL em`sp_execute_external_script`

Nem todos os tipos de dados com suporte no SQL podem ser usados no R. Como alternativa, considere a conversão do tipo de dados sem suporte para um tipo de dados com suporte antes de passar os dados para sp_execute_external_script.

Para obter mais informações, consulte [tipos de dados e bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="possible-string-corruption"></a>Cadeia de caracteres possivelmente corrompida

Qualquer processamento de dados de cadeia de caracteres de [!INCLUDE[tsql](../includes/tsql-md.md)] para R e, em seguida, [!INCLUDE[tsql](../includes/tsql-md.md)] novamente pode resultar na corrupção. Isso ocorre devido a diferentes codificações usadas em R e em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], bem como os vários agrupamentos e linguagens com suporte em R e [!INCLUDE[tsql](../includes/tsql-md.md)]. As cadeias de caracteres em codificação não-ASCII podem ser possivelmente tratadas de forma incorreta.

Ao enviar dados de cadeia de caracteres para R, converta-o em uma representação de ASCII, se possível.

Essa limitação aplica-se a dados transmitidos entre o SQL Server e Python também. Caracteres multibyte devem ser passados como UTF-8 e armazenados como Unicode.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>Apenas um valor do tipo `raw` pode ser retornado de`sp_execute_external_script`

Quando um tipo de dados binários (R **bruto** tipo de dados) é retornado de R, o valor deve ser enviado no quadro de dados de saída.

Dados de tipos diferentes de **bruto**, você pode retornar valores de parâmetro junto com os resultados do procedimento armazenado, adicionando a palavra-chave OUTPUT. Para obter mais informações, consulte [parâmetros](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Se você quiser usar vários conjuntos de saída que incluem valores do tipo **bruto**, uma solução alternativa é fazer várias chamadas do procedimento armazenado ou para enviar o resultado reverte [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando ODBC.

### <a name="loss-of-precision"></a>Perda de precisão

Porque [!INCLUDE[tsql](../includes/tsql-md.md)] e R oferece suporte a vários tipos de dados, tipos de dados numéricos podem sofrer perda de precisão durante a conversão.

Para obter mais informações sobre a conversão implícita de tipo de dados, consulte [tipos de dados e bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter-the-sample-data-set-for-the-analysis-has-no-variables"></a>Variável de erro de escopo quando você usa o parâmetro transformFunc: *o conjunto de dados de exemplo para a análise não tem variáveis*

Para transformar dados enquanto você estiver modelando, você pode passar um *transformFunc* argumento em uma função, como `rxLinmod` ou `rxLogit`. No entanto, chamadas de função aninhadas podem gerar erros de escopo no contexto de computação do SQL Server, mesmo que as chamadas funcionem corretamente no contexto de computação local.

Por exemplo, suponha que você define duas funções, `f` e `g`, em seu ambiente global local e `g` chamadas `f`. Nas chamadas distribuídas ou remotas envolvendo `g`, a chamada para `g` pode falhar porque `f` não pode ser encontrado, mesmo se você passar `f` e `g` para a chamada remota.

Para contornar esse problema, caso o encontre, incorpore a definição de `f` em qualquer local dentro da sua definição de `g`, antes que `g` possa chamar `f`normalmente.

Por exemplo:

```r
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

Para evitar o erro, reescreva a definição da seguinte maneira:

```r
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="data-import-and-manipulation-using-revoscaler"></a>Importação e manipulação de dados usando o RevoScaleR

Quando **varchar** colunas são lidos de um banco de dados, o espaço em branco é cortado. Para evitar isso, coloque as cadeias de caracteres entre caracteres de espaço não em branco.

Quando funções como `rxDataStep` são usados para criar tabelas de banco de dados que têm **varchar** colunas, a largura da coluna é calculada com base em uma amostra dos dados. Se a largura pode variar, pode ser necessário preencher todas as cadeias de caracteres com um comprimento comum.

O uso de uma transformação para alterar o tipo de dados de uma variável não terá suporte quando chamadas repetidas para `rxImport` ou `rxTextToXdf` sejam usadas para importar e anexar linhas, combinando vários arquivos de entrada em um único arquivo .xdf.

### <a name="limited-support-for-rxexec"></a>Suporte limitado para rxExec

No SQL Server 2016, o `rxExec` função que é fornecido com o RevoScaleR pacote pode ser usado apenas no modo de thread único.

Paralelismo de `rxExec` entre vários processos está planejado para uma versão futura.

### <a name="increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>Aumentar o tamanho máximo do parâmetro para dar suporte à função rxGetVarInfo

Se você usar conjuntos de dados com quantidades extremamente grandes de variáveis (por exemplo, mais de 40.000), defina o `max-ppsize` sinalizador quando iniciar R para usar funções como `rxGetVarInfo`. O sinalizador `max-ppsize` especifica o tamanho máximo da pilha de proteção do ponteiro.

Se você estiver usando o console de R (por exemplo, RGui.exe ou RTerm.exe), você pode definir o valor de _max-ppsize_ em 500000 digitando:

```R
R --max-ppsize=500000
```

### <a name="issues-with-the-rxdtree-function"></a>Problemas com a função rxDTree

Atualmente, a função `rxDTree` não tem suporte para transformações dentro da fórmula. Não temos suporte para o uso da sintaxe `F()` , em especial, para a criação de fatores dinâmicos. No entanto, os dados numéricos são automaticamente guardados.

Os fatores ordenados são tratados da mesma forma que os fatores de todas as funções de análise RevoScaleR, exceto o `rxDTree`.

## <a name="python-code-execution-or-python-package-issues"></a>A execução de código Python ou problemas de pacotes do Python

Esta seção contém os problemas conhecidos que são específicos para em execução Python no SQL Server, bem como problemas relacionados aos pacotes Python publicados pela Microsoft, incluindo [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>Chamada para o modelo pré-treinado falha se o caminho para o modelo é muito longo

Se você instalou os modelos pré-treinado em uma versão anterior do SQL Server 2017, o caminho completo para o arquivo de modelo treinado pode ser muito longo para Python para leitura. Essa limitação é fixo em uma versão posterior do serviço.

Há várias possíveis soluções alternativas: 

+ Quando você instala os modelos pré-treinado, escolha um local personalizado.
+ Se possível, instale a instância do SQL Server em um caminho de instalação personalizada com um caminho mais curto, como C:\SQL\MSSQL14. MSSQLSERVER.
+ Use o utilitário Windows [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) para criar um vínculo físico que mapeia o arquivo de modelo para um caminho mais curto. 
+ Atualize para a versão mais recente do serviço.

### <a name="failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>Falha ao inicializar uma variável varbinary causa um erro no BxlServer

Se você executar o código Python no SQL Server usando `sp_execute_external_script`e o código de saída variáveis do tipo varbinary (max), varchar (max) ou tipos semelhantes, a variável deve ser inicializada ou definida como parte do script. Caso contrário, o componente de troca de dados, BxlServer, gera um erro e parar de funcionar.

Essa limitação será corrigida em uma versão futura do serviço. Como alternativa, certifique-se de que a variável é inicializada dentro do script de Python. Qualquer valor válido pode ser usado, como nos exemplos a seguir:

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N'b = 0x0'
  , @params = N'@b varbinary(max) OUTPUT'
  , @b = @b OUTPUT;
go
```

```sql
declare @b varchar(30);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N' b = ""  '
  , @params = N'@b varchar(30) OUTPUT'
  , @b = @b OUTPUT;
go
```

### <a name="telemetry-warning-on-successful-execution-of-python-code"></a>Aviso de telemetria em execução bem-sucedida do código Python

A partir do SQL Server de 2017 CU2, a seguinte mensagem pode aparecer mesmo se o código Python caso contrário é executado com êxito:

```text
STDERR message(s) from external script:  ~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger
SyntaxWarning: telemetry_state is used prior to global declaration
```

Esse problema foi corrigido no SQL Server de 2017 atualização cumulativa 3 (CU3). 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open

Esta seção lista os problemas específicos para conectividade de R, desenvolvimento e ferramentas de desempenho que são fornecidas pela Revolution Analytics. Essas ferramentas foram fornecidas nas versões de pré-lançamento anteriores do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

Em geral, é recomendável que você desinstale essas versões anteriores e instala a versão mais recente do SQL Server ou Microsoft R Server.

### <a name="revolution-r-enterprise-is-not-supported"></a>Não há suporte para Revolution R Enterprise

Instalar o Revolution R Enterprise lado a lado com qualquer versão do [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] não tem suporte.

Se você tiver uma licença existente para Revolution R Enterprise, você deve colocá-lo em um computador separado de ambas as [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instância e estação de trabalho que você deseja usar para se conectar à [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instância.

Algumas versões de pré-lançamento do [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluído um ambiente de desenvolvimento R para Windows criado pela Revolution Analytics. Essa ferramenta não é mais fornecida e não tem suporte.

Para compatibilidade com [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], recomendamos que você instale o cliente do Microsoft R. [Ferramentas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) e [código do Visual Studio](https://code.visualstudio.com/) também dá suporte a soluções de R da Microsoft.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Problemas de compatibilidade com o driver ODBC do SQLite e o RevoScaleR

Revisão 0.92 do driver ODBC do SQLite é incompatível com o RevoScaleR. Revisões de 0.88 a 0.91 e 0.93 e posteriores são compatíveis.

## <a name="see-also"></a>Consulte também

[Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Solucionando problemas de aprendizado de máquina no SQL Server](machine-learning-troubleshooting-faq.md)
