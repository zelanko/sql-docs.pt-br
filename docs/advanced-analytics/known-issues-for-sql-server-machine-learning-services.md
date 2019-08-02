---
title: Problemas conhecidos de integração do Python e da linguagem R
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 93b2871fa60d6a7c7a41fae202e960440b53c11e
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715190"
---
# <a name="known-issues-in-machine-learning-services"></a>Problemas conhecidos no Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve problemas ou limitações conhecidos com componentes do Machine Learning que são fornecidos como uma opção em [2016 SQL Server r Services](r/sql-server-r-services.md) e [SQL Server serviços de Machine Learning com r e Python](what-is-sql-server-machine-learning.md).

## <a name="setup-and-configuration-issues"></a>Problemas de instalação e configuração

Para obter uma descrição dos processos e perguntas comuns relacionadas à instalação inicial e à configuração, consulte [perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md). Ele contém informações sobre atualizações, instalação lado a lado e instalação de novos componentes de R ou Python.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. Resultados inconsistentes em computações do MKL devido à falta de variável de ambiente

**Aplica-se a:** R_SERVER binários 9,0, 9,1, 9,2 ou 9,3.

O R_SERVER usa a Intel Math Kernel Library (MKL). Para cálculos que envolvam MKL, resultados inconsistentes poderão ocorrer se o sistema não tiver uma variável de ambiente. 

Defina a variável `'MKL_CBWR'=AUTO` de ambiente para garantir o reprodução numérico condicional em R_SERVER. Para obter mais informações, consulte [introdução ao CNR (numerical reprodução)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr).

**Solução alternativa**

1. No painel de controle, clique em sistema e**sistema** >  **de segurança** > **configurações** > avançadas do sistema**variáveis de ambiente**.

2. Crie uma nova variável de usuário ou de sistema. 

  + Defina o nome da variável como ' MKL_CBWR '.
  + Defina o ' valor da variável ' como ' AUTO '.

3. Reinicie o R_SERVER. Em SQL Server, você pode reiniciar SQL Server Launchpad serviço.

> [!NOTE]
> Se você estiver executando a versão prévia do SQL Server 2019 no Linux, edite ou crie *. bash_profile* no diretório base do usuário, `export MKL_CBWR="AUTO"`adicionando a linha. Execute esse arquivo digitando `source .bash_profile` em um prompt de comando bash. Reinicie o R_SERVER `Sys.getenv()` digitando no prompt de comando do R.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. Erro de tempo de execução de script R (SQL Server 2017 CU5-CU7 regressão)

Para SQL Server 2017, em atualizações cumulativas de 5 a 7, há uma regressão no arquivo **rlauncher. config** em que o caminho do arquivo do diretório Temp inclui um espaço. Essa regressão é corrigida em CU8.

O erro que você verá ao executar o script R incluirá as seguintes mensagens:

> *Não é possível se comunicar com o tempo de execução do script ' R '. Verifique os requisitos do tempo de execução ' R '.*
>
> Mensagem (ns) STDERR do script externo: 
>
> *Erro fatal: não é possível criar ' R_TempDir '*

**Solução alternativa**

Aplique CU8 quando ela ficar disponível. Como alternativa, você pode recriar **rlauncher. config** executando **registerrext** com desinstalar/instalar em um prompt de comandos com privilégios elevados. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

O exemplo a seguir mostra os comandos com a instância padrão "MSSQL14. MSSQLSERVER "instalado em" C:\Arquivos de Programas\microsoft\"SQL Server:

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. Não é possível instalar SQL Server recursos de Machine Learning em um controlador de domínio

Se você tentar instalar SQL Server 2016 R Services ou SQL Server Serviços de Machine Learning em um controlador de domínio, a instalação falhará, com estes erros:

> *Ocorreu um erro durante o processo de instalação do recurso*
> 
> *Não é possível localizar o grupo com identidade*
> 
> *Código de erro do componente: 0x80131509*

A falha ocorre porque, em um controlador de domínio, o serviço não pode criar as 20 contas locais necessárias para executar o aprendizado de máquina. Em geral, não recomendamos a instalação de SQL Server em um controlador de domínio. Para obter mais informações, consulte o [Boletim de suporte 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Instale a versão mais recente do serviço para garantir a compatibilidade com Microsoft R Client

Se você instalar a versão mais recente do Microsoft R Client e usá-la para executar o R em SQL Server em um contexto de computação remota, você poderá receber um erro semelhante ao seguinte:

> *Você está executando a versão 9. x. x de Microsoft R Client em seu computador, que é incompatível com Microsoft R Server versão 8. x.x. Baixe e instale uma versão compatível.*

SQL Server 2016 requer que as bibliotecas do R no cliente correspondam exatamente às bibliotecas do R no servidor. A restrição foi removida para versões posteriores ao 9.0.1 do R Server. No entanto, se você encontrar esse erro, verifique a versão das bibliotecas do R que é usada pelo cliente e o servidor e, se necessário, atualize o cliente para corresponder à versão do servidor.

A versão do R instalada com o SQL Server R Services é atualizada sempre que uma versão do serviço SQL Server é instalada. Para garantir que você sempre tenha as versões mais atualizadas dos componentes do R, certifique-se de instalar todos os Service Packs.

Para garantir a compatibilidade com Microsoft R Client 9.0.0, instale as atualizações descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).

Para evitar problemas com pacotes do R, você também pode atualizar a versão das bibliotecas do R que estão instaladas no servidor, alterando seu contrato de manutenção para usar a política de suporte do ciclo de vida moderno, conforme descrito na [próxima seção](#bkmk_sqlbindr). Quando você faz isso, a versão do R instalada com o SQL Server é atualizada na mesma agenda usada para atualizações do servidor do Machine Learning (anteriormente Microsoft R Server).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="5-r-components-missing-from-cu3-setup"></a>5. Componentes do R ausentes da configuração do CU3

Um número limitado de máquinas virtuais do Azure foi provisionado sem os arquivos de instalação do R que devem ser incluídos com SQL Server. O problema se aplica às máquinas virtuais provisionadas no período de 2018-01-05 a 2018-01-23. Esse problema também pode afetar as instalações locais, se você aplicou a atualização CU3 para SQL Server 2017 durante o período de 2018-01-05 a 2018-01-23.

Foi fornecida uma versão de serviço que inclui a versão correta dos arquivos de instalação do R.

+ [Pacote de atualização cumulativa 3 para SQL Server 2017 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

Para instalar os componentes e reparar SQL Server 2017 CU3, você deve desinstalar o CU3 e reinstalar a versão atualizada:

1. Baixe o arquivo de instalação do CU3 atualizado, que inclui os instaladores do R.
2. Desinstale o CU3. No painel de controle, procure **desinstalar uma atualização**e, em seguida, selecione "hotfix 3015 para SQL Server 2017 (KB4052987) (64-bit)". Prossiga com as etapas de desinstalação.
3. Reinstale a atualização do CU3 clicando duas vezes na atualização de KB4052987 que você acabou de baixar: `SQLServer2017-KB4052987-x64.exe`. Siga as instruções de instalação.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. Não é possível instalar os componentes do Python em instalações offline do SQL Server 2017 CTP 2,0 ou posterior

Se você instalar uma versão de pré-lançamento do SQL Server 2017 em um computador sem acesso à Internet, o instalador poderá falhar ao exibir a página que solicita o local dos componentes do Python baixados. Nessa instância, você pode instalar o recurso Serviços de Machine Learning, mas não os componentes do Python.

Esse problema é corrigido na versão de lançamento. Além disso, essa limitação não se aplica aos componentes do R.

**Aplica-se a:** SQL Server 2017 com Python

### <a name="bkmk_sqlbindr"></a>Aviso de versão incompatível quando você se conecta a uma versão mais antiga do SQL Server R Services de um cliente usando o[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Ao executar o código R em um SQL Server contexto de computação 2016, você poderá ver o seguinte erro:

> *Você está executando a versão 9.0.0 do Cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

Essa mensagem será exibida se uma das duas instruções a seguir for verdadeira,

+ Você instalou o R Server (autônomo) em um computador cliente usando o assistente para instalação [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]do.
+ Você instalou Microsoft R Server usando o [Windows Installer separado](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para garantir que o servidor e o cliente usem a mesma versão, talvez seja necessário usar a _Associação_, com suporte para Microsoft R Server 9,0 e versões posteriores, para atualizar os componentes do R em SQL Server instâncias 2016. Para determinar se o suporte para atualizações está disponível para sua versão do R Services, consulte [atualizar uma instância do r Services usando Sqlbindr. exe](install/upgrade-r-and-python.md).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. A instalação de versões de serviço do SQL Server 2016 poderá falhar ao instalar versões mais novas dos componentes do R

Quando você instala uma atualização cumulativa ou instala um service pack para SQL Server 2016 em um computador que não está conectado à Internet, o assistente de instalação pode falhar ao exibir o prompt que permite atualizar os componentes do R usando arquivos CAB baixados. Essa falha normalmente ocorre quando vários componentes foram instalados junto com o mecanismo de banco de dados.

Como alternativa, você pode instalar a versão do serviço usando a linha de comando e especificando o `MRCACHEDIRECTORY` argumento, conforme mostrado neste exemplo, que instala as atualizações do Cu1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obter os instaladores mais recentes, consulte [instalar componentes do Machine Learning sem acesso à Internet](install/sql-ml-component-install-without-internet-access.md).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. Os serviços do Launchpad não serão iniciados se a versão for diferente da versão do R

Se você instalar SQL Server R Services separadamente do mecanismo de banco de dados e as versões de compilação forem diferentes, você poderá ver o seguinte erro no log de eventos do sistema:

> *Falha ao iniciar o serviço de SQL Server Launchpad devido ao seguinte erro: O serviço não respondeu à solicitação de início ou de controle em tempo hábil.*

Por exemplo, esse erro pode ocorrer se você instalar o mecanismo de banco de dados usando a versão de lançamento, aplicar um patch para atualizar o mecanismo de banco de dados e, em seguida, adicionar o recurso R Services usando a versão de lançamento.

Para evitar esse problema, use um utilitário como o Gerenciador de arquivos para comparar as versões do Launchpad. exe com a versão de binários do SQL, como sqldk. dll. Todos os componentes devem ter o mesmo número de versão. Se você atualizar um componente, lembre-se de aplicar a mesma atualização a todos os outros componentes instalados.

Procure a barra inicial na `Binn` pasta da instância. Por exemplo, em uma instalação padrão do SQL Server 2016, o caminho pode ser `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. Contextos de computação remota são bloqueados por um firewall em SQL Server instâncias que estão em execução em máquinas virtuais do Azure

Se você tiver instalado [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] o em uma máquina virtual do Windows Azure, talvez não seja possível usar contextos de computação que exijam o uso do espaço de trabalho da máquina virtual. O motivo é que, por padrão, o firewall em máquinas virtuais do Azure inclui uma regra que bloqueia o acesso à rede para contas de usuário locais do R.

Como solução alternativa, na VM do Azure, abra **Firewall do Windows com segurança avançada**, selecione **regras de saída**e desabilite a seguinte regra: **Bloquear o acesso à rede para contas de usuário local do R na instância SQL Server MSSQLSERVER**. Você também pode deixar a regra habilitada, mas alterar a propriedade de segurança para **permitir se seguro**.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. Autenticação implícita em SQLEXPRESS

Quando você executa trabalhos do R de uma estação de trabalho de ciência de dados remota usando a autenticação integrada do Windows, o SQL Server usa a *autenticação implícita* para gerar qualquer chamada ODBC local que possa ser exigida pelo script. No entanto, esse recurso não funcionou no build RTM do SQL Server Express Edition.

Para corrigir o problema, recomendamos atualizar para uma versão de serviço posterior.

Se a atualização não for viável, como alternativa, use um logon do SQL para executar trabalhos de R remotos que podem exigir chamadas ODBC inseridas.

**Aplica-se a:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. Limites de desempenho quando as bibliotecas usadas por SQL Server são chamadas de outras ferramentas

É possível chamar as bibliotecas de aprendizado de máquina que estão instaladas para SQL Server de um aplicativo externo, como RGui. Fazer isso pode ser a maneira mais conveniente para realizar determinadas tarefas, como instalar novos pacotes ou executar testes ad hoc em exemplos de código muito curtos. No entanto, fora do SQL Server, o desempenho pode ser limitado. 

Por exemplo, mesmo se você estiver usando a Enterprise Edition do SQL Server, o R será executado no modo de thread único quando você executar o código R usando ferramentas externas. Para obter os benefícios do desempenho no SQL Server, inicie uma conexão SQL Server e use [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para chamar o tempo de execução de script externo.

Em geral, evite chamar as bibliotecas de aprendizado de máquina que são usadas pelo SQL Server de ferramentas externas. Se você precisar depurar o código R ou Python, normalmente será mais fácil fazer isso fora do SQL Server. Para obter as mesmas bibliotecas que estão no SQL Server, você pode instalar o Microsoft R Client, [SQL Server 2017 Machine Learning Server (autônomo)](install/sql-machine-learning-standalone-windows-install.md)ou o [SQL Server 2016 R Server (autônomo)](install/sql-r-standalone-windows-install.md).

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools não dá suporte a permissões exigidas por scripts externos

Quando você usa o Visual Studio ou SQL Server Data Tools para publicar um projeto de banco de dados, se qualquer entidade tiver permissões específicas para a execução de script externo, você poderá receber um erro como este:

> *Modelo TSQL: Erro detectado ao fazer engenharia reversa do banco de dados. A permissão não foi reconhecida e não foi importada.*

Atualmente, o modelo DACPAC não oferece suporte às permissões usadas pelo R Services ou Serviços de Machine Learning, como conceder qualquer SCRIPT externo ou executar qualquer SCRIPT externo. Esse problema será corrigido em uma versão posterior.

Como alternativa, execute as instruções GRANT adicionais em um script pós-implantação.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. A execução de script externo é limitada devido aos valores padrão de governança de recursos

No Enterprise Edition, você pode usar pools de recursos para gerenciar processos de script externo. Em algumas compilações de versões anteriores, a memória máxima que poderia ser alocada para os processos de R foi de 20%. Portanto, se o servidor tiver 32 GB de RAM, os executáveis R (RTerm. exe e BxlServer. exe) poderiam usar um máximo de 6,4 GB em uma única solicitação.

Se você encontrar limitações de recursos, verifique o padrão atual. Se 20 por cento não for suficiente, consulte a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] documentação sobre como alterar esse valor.

**Aplica-se a:** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>Problemas de execução de script R

Esta seção contém problemas conhecidos que são específicos para executar o R em SQL Server, bem como alguns problemas relacionados às bibliotecas e ferramentas do R publicadas pela Microsoft, incluindo RevoScaleR.

Para problemas conhecidos adicionais que podem afetar as soluções de R, consulte o site [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) .

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. Aviso de acesso negado ao executar scripts R em SQL Server em um local não padrão

Se a instância do SQL Server tiver sido instalada em um local não padrão, como fora da `Program Files` pasta, o aviso ACCESS_DENIED será gerado quando você tentar executar scripts que instalam um pacote. Por exemplo:

> *Em `normalizePath(path.expand(path), winslash, mustWork)` : caminho [2] = "~ ExternalLibraries/R/8/1": Acesso negado*

O motivo é que uma função do R tenta ler o caminho e falha se o grupo interno de usuários **SQLRUserGroup**, não tem acesso de leitura. O aviso gerado não bloqueia a execução do script do R atual, mas o aviso pode ocorrer repetidamente sempre que o usuário executar qualquer outro script do R.

Se você tiver instalado SQL Server no local padrão, esse erro não ocorrerá, pois todos os usuários do Windows têm permissões de leitura `Program Files` na pasta.

Esse problema ia foi resolvido em uma versão futura do serviço. Como alternativa, forneça o grupo, **SQLRUserGroup**, com acesso de leitura para todas as pastas pai `ExternalLibraries`do.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. Erro de serialização entre as versões antiga e nova do RevoScaleR

Ao passar um modelo usando um formato serializado para uma instância de SQL Server remota, você pode receber o erro: 

> *Erro em memDecompress (dados, tipo = descompactar) erro interno-3 em memDecompress (2).*

Esse erro será gerado se você salvou o modelo usando uma versão recente da função de serialização, [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), mas a instância de SQL Server em que você desserializar o modelo tiver uma versão mais antiga das APIs do RevoScaleR, de SQL Server 2017 Cu2 ou anterior.

Como alternativa, você pode atualizar a instância do SQL Server 2017 para CU3 ou posterior.

O erro não será exibido se a versão da API for a mesma, ou se você estiver movendo um modelo salvo com uma função de serialização mais antiga para um servidor que usa uma versão mais recente da API de serialização.

Em outras palavras, use a mesma versão do RevoScaleR para operações de serialização e desserialização.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>3. A pontuação em tempo real não manipula corretamente o parâmetro _learningRate_ em modelos de árvore e floresta

Se você criar um modelo usando uma árvore de decisão ou um método de floresta de decisão e especificar a taxa de aprendizagem, você poderá ver `sp_rxpredict` resultados inconsistentes ao usar o ou a `rxPredict`função SQL `PREDICT` , em comparação com o uso de.

A causa é um erro na API que processa modelos serializados e é limitada ao `learningRate` parâmetro: por exemplo, em [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees), ou

Esse problema é resolvido em uma versão de serviço futura.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. Limitações na afinidade do processador para trabalhos do R

Na versão inicial do Build do SQL Server 2016, você pode definir a afinidade do processador somente para CPUs no primeiro grupo k. Por exemplo, se o servidor for um computador de 2 soquetes com dois grupos k, somente os processadores do primeiro grupo k serão usados para os processos do R. A mesma limitação se aplica quando você configura a governança de recursos para trabalhos de script do R.

Esse problema é corrigido no SQL Server 2016 Service Pack 1. Recomendamos que você atualize para a versão mais recente do serviço.

**Aplica-se a:** Versão RTM do SQL Server R Services 2016

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5. Não é possível fazer alterações nos tipos de coluna durante a leitura de dados em um contexto de computação do SQL Server

Se o contexto de computação estiver definido como a instância do SQL Server, não será possível usar o argumento _colClasses_ (ou outros argumentos semelhante) para alterar o tipo de dados das colunas no código R.

Por exemplo, a seguinte instrução resultará em um erro se a coluna CRSDepTimeStr ainda não for um inteiro:

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

Como alternativa, você pode reescrever a consulta SQL para usar CAST ou CONVERT e apresentar os dados para R usando o tipo de dados correto. Em geral, o desempenho é melhor quando você trabalha com dados usando SQL em vez de alterar dados no código R.

**Aplica-se a:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. Limites no tamanho dos modelos serializados

Quando você salva um modelo em uma tabela SQL Server, você deve serializar o modelo e salvá-lo em um formato binário. Teoricamente, o tamanho máximo de um modelo que pode ser armazenado com esse método é 2 GB, que é o tamanho máximo das colunas varbinary no SQL Server.

Se você precisar usar modelos maiores, as seguintes soluções alternativas estarão disponíveis:

+ Tome medidas para reduzir o tamanho do seu modelo. Alguns pacotes R de software livre incluem uma grande quantidade de informações no objeto de modelo, e muitas dessas informações podem ser removidas para implantação. 
+ Use a seleção de recursos para remover colunas desnecessárias.
+ Se você estiver usando um algoritmo de software livre, considere uma implementação semelhante usando o algoritmo correspondente em MicrosoftML ou RevoScaleR. Esses pacotes foram otimizados para cenários de implantação.
+ Depois que o modelo foi racionalizado e o tamanho reduzido usando as etapas anteriores, veja se a função [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) no R de base pode ser usada para reduzir o tamanho do modelo antes de passá-lo para SQL Server. Essa opção é melhor quando o modelo está perto do limite de 2 GB.
+ Para modelos maiores, você pode usar o SQL Server recurso [filetable](../relational-databases/blob/filetables-sql-server.md) para armazenar os modelos, em vez de usar uma coluna varbinary.

    Para usar filetables, você deve adicionar uma exceção de firewall, pois os dados armazenados em filetables são gerenciados pelo driver de sistema de arquivos FILESTREAM no SQL Server e as regras de firewall padrão bloqueiam o acesso ao arquivo de rede. Para obter mais informações, consulte [Enable Prerequisites for filetable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md).

    Depois de habilitar a Filetable, para gravar o modelo, você obtém um caminho do SQL usando a API Filetable e, em seguida, grava o modelo nesse local por meio do seu código. Quando precisar ler o modelo, você obtém o caminho do SQL e, em seguida, chama o modelo usando o caminho do seu script. Para obter mais informações, consulte [acessar Filetables com APIs de entrada/saída de arquivo](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7. Evite limpar os espaços de trabalho ao executar o código R [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um contexto de computação

Se você usar um comando do r para limpar o espaço de trabalho de objetos ao executar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] código r em um contexto de computação, ou se limpar o espaço de trabalho como parte de um script R chamado usando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), você poderá receber esse erro: *espaço de trabalho revoScriptConnection de objeto não encontrado*

O`revoScriptConnection` é um objeto no workspace do R que contém informações sobre uma sessão do R chamada por meio de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, se o código R incluir um comando para limpar o workspace (como `rm(list=ls()))`), todas as informações sobre a sessão e outros objetos no workspace do R também serão limpos.

Como alternativa, evite a limpeza indiscriminado de variáveis e outros objetos enquanto você estiver executando o R [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]no. Embora a limpeza do espaço de trabalho seja comum ao trabalhar no console do R, ela pode ter consequências indesejadas.

* Para excluir variáveis específicas, use a função `remove` R: por exemplo,`remove('name1', 'name2', ...)`
* Se houver várias variáveis a serem excluídas, salve os nomes das variáveis temporárias em uma lista e execute a coleta de lixo periódica.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. Restrições sobre dados que podem ser fornecidos como entrada para um script R

O sistema não permite usar os seguintes tipos de resultados de consulta em um script R:

- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência às colunas AlwaysEncrypted.
  
- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência à colunas mascaradas.
  
     Se precisar usar dados mascarados em um script R, uma solução alternativa é copiar os dados em uma tabela temporária e usar esses dados.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. O uso de cadeias de caracteres como fatores pode levar à degradação do desempenho

Usar variáveis de tipo de cadeia de caracteres como fatores pode aumentar muito a quantidade de memória usada para operações de R. Esse é um problema conhecido com R em geral, e há muitos artigos sobre o assunto. Por exemplo, veja [fatores que não são cidadãos de primeira classe em r, por John Mount, em r-bloggers)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) ou [stringsAsFactors: Uma biografia não autorizada, por Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Embora o problema não seja específico para SQL Server, ele pode afetar muito o desempenho da execução do código R no SQl Server. Em geral, as cadeias de caracteres são armazenadas como varchar ou nvarchar e, se uma coluna de dados de cadeia tiver muitos valores exclusivos, o processo de convertê-las internamente para inteiros e voltar para cadeias por R poderá até mesmo levar a erros de alocação de memória.

Se você não precisar absolutamente de um tipo de dados de cadeia de caracteres para outras operações, o mapeamento dos valores de cadeia de caracteres para um tipo de dados numérico (inteiro) como parte da preparação dos dados seria benéfico em relação à perspectiva de desempenho e escala.

Para obter uma discussão sobre esse problema e outras dicas, consulte [performance for R Services-otimização de dados](r/r-and-data-optimization-r-services.md).

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. Os argumentos *varsToKeep* e *varsToDrop* não têm suporte para fontes de dados SQL Server

Quando você usa a função rxDataStep para gravar resultados em uma tabela, o uso de *varsToKeep* e *varsToDrop* é uma maneira útil de especificar as colunas a serem incluídas ou excluídas como parte da operação. No entanto, esses argumentos não têm suporte para SQL Server fontes de dados.

### <a name="11-limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>11. Suporte limitado para tipos de dados SQL no\_SP\_executar\_script externo

Nem todos os tipos de dados com suporte no SQL podem ser usados em R. Como alternativa, considere converter o tipo de dados sem suporte para um tipo de dados com suporte antes de passar os dados\_para\_SP\_executar script externo.

Para obter mais informações, consulte [bibliotecas e tipos de dados do R](r/r-libraries-and-data-types.md).

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Possível corrupção de cadeia de caracteres usando cadeias Unicode em colunas varchar

A passagem de dados Unicode em colunas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] varchar de para R/Python pode resultar em corrupção de cadeia de caracteres. Isso ocorre devido à codificação para essa cadeia de caracteres Unicode [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em agrupamentos pode não corresponder com a codificação UTF-8 padrão usada em R/Python. 

Para enviar dados de cadeia de caracteres não ASCII [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de para R/Python, use a codificação UTF-8 ( [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]disponível em) ou use o tipo nvarchar para o mesmo.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>13. Somente um valor do tipo `raw` pode ser retornado de`sp_execute_external_script`

Quando um tipo de dados binary (o tipo de dados **bruto** do r) é retornado de R, o valor deve ser enviado no quadro de dados de saída.

Com tipos de dados diferentes de **RAW**, você pode retornar valores de parâmetro junto com os resultados do procedimento armazenado adicionando a palavra-chave output. Para obter mais informações, consulte [parâmetros](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Se você quiser usar vários conjuntos de saída que incluem valores do tipo **RAW**, uma solução alternativa possível é fazer várias chamadas do procedimento armazenado ou enviar os conjuntos de resultados de volta ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o ODBC.

### <a name="14-loss-of-precision"></a>14. Perda de precisão

Como [!INCLUDE[tsql](../includes/tsql-md.md)] e o R dá suporte a vários tipos de dados, os tipos de dados numéricos podem sofrer perda de precisão durante a conversão.

Para obter mais informações sobre conversão implícita de tipo de dados, consulte [bibliotecas e tipos de dados do R](r/r-libraries-and-data-types.md).

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. Erro de escopo de variável ao usar o parâmetro transformFunc

Para transformar dados enquanto você está modelando, você pode passar um argumento *transformFunc* em uma função `rxLinmod` como `rxLogit`ou. No entanto, chamadas de função aninhadas podem levar a erros de escopo no contexto de computação SQL Server, mesmo que as chamadas funcionem corretamente no contexto de computação local.

> *O conjunto de dados de exemplo para a análise não tem nenhuma variável*

Por exemplo, suponha que `f` você definiu duas funções e `g`, em seu ambiente global local, e `g` chama `f`. Em chamadas distribuídas ou remotas `g`que envolvem `g` , a chamada para pode falhar com `f` esse erro, porque não pode ser `f` encontrada, mesmo que `g` você tenha passado e para a chamada remota.

Para contornar esse problema, caso o encontre, incorpore a definição de `f` em qualquer local dentro da sua definição de `g`, antes que `g` possa chamar `f`normalmente.

Por exemplo:

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

Para evitar o erro, reescreva a definição da seguinte maneira:

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16. Importação e manipulação de dados usando o RevoScaleR

Quando colunas **varchar** são lidas de um banco de dados, o espaço em branco é cortado. Para evitar isso, coloque as cadeias de caracteres entre caracteres de espaço não em branco.

Quando funções como `rxDataStep` são usadas para criar tabelas de banco de dados que têm colunas **varchar** , a largura da coluna é estimada com base em uma amostra dos dados. Se a largura puder variar, talvez seja necessário preencher todas as cadeias de caracteres para um comprimento comum.

O uso de uma transformação para alterar o tipo de dados de uma variável não terá suporte quando chamadas repetidas para `rxImport` ou `rxTextToXdf` sejam usadas para importar e anexar linhas, combinando vários arquivos de entrada em um único arquivo .xdf.

### <a name="17-limited-support-for-rxexec"></a>17. Suporte limitado para rxExec

No SQL Server 2016, a `rxExec` função fornecida pelo pacote RevoScaleR pode ser usada somente no modo de thread único.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. Aumentar o tamanho máximo do parâmetro para dar suporte a rxGetVarInfo

Se você usar conjuntos de dados com números extremamente grandes de variáveis (por exemplo, mais de 40.000), `max-ppsize` defina o sinalizador ao iniciar o R para usar funções `rxGetVarInfo`como. O sinalizador `max-ppsize` especifica o tamanho máximo da pilha de proteção do ponteiro.

Se você estiver usando o console do R (por exemplo, RGui. exe ou RTerm. exe), poderá definir o valor de _Max-ppsize_ como 500000 digitando:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. Problemas com a função rxDTree

Atualmente, a função `rxDTree` não tem suporte para transformações dentro da fórmula. Não temos suporte para o uso da sintaxe `F()` , em especial, para a criação de fatores dinâmicos. No entanto, os dados numéricos são automaticamente compartimentalizadosdos.

Os fatores ordenados são tratados da mesma forma que os fatores de todas as funções de análise RevoScaleR, exceto o `rxDTree`.

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20. Data. Table como um OutputDataSet em R

Não `data.table` há suporte `OutputDataSet` para o uso do como em R no SQL Server 2017 atualização cumulativa 13 (CU13) e anterior. A seguinte mensagem pode aparecer:

```
Msg 39004, Level 16, State 20, Line 2
A 'R' script error occurred during execution of 
'sp_execute_external_script' with HRESULT 0x80004004.
Msg 39019, Level 16, State 2, Line 2
An external script error occurred: 
Error in alloc.col(newx) : 
  Internal error: length of names (0) is not length of dt (11)
Calls: data.frame ... as.data.frame -> as.data.frame.data.table -> copy -> alloc.col

Error in execution.  Check the output for more information.
Error in eval(expr, envir, enclos) : 
  Error in execution.  Check the output for more information.
Calls: source -> withVisible -> eval -> eval -> .Call
Execution halted
```

`data.table`como um `OutputDataSet` em R tem suporte no SQL Server 2017 atualização cumulativa 14 (CU14) e posterior.

## <a name="python-script-execution-issues"></a>Problemas de execução de script do Python

Esta seção contém problemas conhecidos que são específicos para executar o Python no SQL Server, bem como problemas relacionados aos pacotes do Python publicados pela Microsoft, incluindo [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. A chamada para o modelo pretreinado falha se o caminho para o modelo for muito longo

Se você instalou os modelos pré-treinados em uma versão inicial do SQL Server 2017, o caminho completo para o arquivo de modelo treinado pode ser muito longo para que o Python seja lido. Essa limitação é corrigida em uma versão de serviço posterior.

Há várias soluções alternativas possíveis: 

+ Ao instalar os modelos pré-treinados, escolha um local personalizado.
+ Se possível, instale a instância de SQL Server em um caminho de instalação personalizado com um caminho mais curto, como C:\SQL\MSSQL14. MSSQLSERVER.
+ Use o utilitário do Windows [fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) para criar um link físico que mapeia o arquivo de modelo para um caminho mais curto.
+ Atualize para a versão mais recente do serviço.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. Erro ao salvar o modelo serializado em SQL Server

Quando você passa um modelo para uma instância de SQL Server remota e tenta ler o modelo binário usando a `rx_unserialize` função em [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), você pode receber o erro: 

> *NameError: o nome ' rx_unserialize_model ' não está definido*

Esse erro é gerado se você salvou o modelo usando uma versão recente da função de serialização, mas a instância de SQL Server em que você desserializar o modelo não reconhece a API de serialização.

Para resolver o problema, atualize a instância do SQL Server 2017 para CU3 ou posterior.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. Falha ao inicializar uma variável varbinary causa um erro em BxlServer

Se você executar o código Python em SQL Server `sp_execute_external_script`usando, e o código tiver variáveis de saída do tipo varbinary (max), varchar (max) ou tipos semelhantes, a variável deverá ser inicializada ou definida como parte do seu script. Caso contrário, o componente de troca de dados, BxlServer, gerará um erro e deixará de funcionar.

Essa limitação será corrigida em uma versão de serviço futura. Como alternativa, certifique-se de que a variável seja inicializada dentro do script Python. Qualquer valor válido pode ser usado, como nos exemplos a seguir:

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

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. Aviso de telemetria sobre a execução bem-sucedida do código Python

A partir do SQL Server 2017 CU2, a seguinte mensagem pode aparecer mesmo que o código Python seja executado com êxito:

> *Mensagem (ns) stderr do script externo:* 
>  *~ PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state é usado antes da declaração global*

Esse problema foi corrigido no SQL Server 2017 atualização cumulativa 3 (CU3). 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5. Tipos de dados numeric, decimal e Money sem suporte

A partir do SQL Server 2017, os tipos de dados CU12 (atualização cumulativa 12), Numeric, decimal e Money no com conjuntos de resultados não têm suporte `sp_execute_external_script`ao usar o Python com o. As seguintes mensagens podem aparecer:

> *Auto-completar 39004, estado do SQL: S1000] ocorreu um erro de script "Python" durante a execução of'sp_execute_external_script "com HRESULT 0x80004004.*

> *Auto-completar 39019, estado do SQL: S1000] ocorreu um erro de script externo:*
> 
> *Erro de SqlSatelliteCall: Tipo sem suporte no esquema de saída. Tipos com suporte: bit, smallint, int, DateTime, SmallMoney, real e float. Char, varchar têm suporte parcial.*

Isso foi corrigido no SQL Server 2017 atualização cumulativa 14 (CU14).

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open

Esta seção lista problemas específicos para conectividade de R, desenvolvimento e ferramentas de desempenho que são fornecidos pela análise de revolução. Essas ferramentas foram fornecidas nas versões anteriores de pré-lançamento do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

Em geral, recomendamos que você desinstale essas versões anteriores e instale a versão mais recente do SQL Server ou Microsoft R Server.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. Não há suporte para a revolução R Enterprise

Não há suporte para a instalação da revolução R Enterprise lado [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] a lado com nenhuma versão do.

Se você tiver uma licença existente para a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] revolução R Enterprise, deverá colocá-la em um computador separado da instância do e de qualquer estação de trabalho que deseja usar para se conectar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] à instância do.

Algumas versões de pré-lançamento do [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluíam um ambiente de desenvolvimento de R para Windows que foi criado pela análise de revolução. Essa ferramenta não é mais fornecida e não tem suporte.

Para compatibilidade com [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]o, recomendamos que você instale Microsoft R Client em vez disso. [Ferramentas do R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) e [Visual Studio Code](https://code.visualstudio.com/) também dá suporte a soluções do Microsoft R.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. Problemas de compatibilidade com o driver ODBC do SQLite e o RevoScaleR

A revisão 0,92 do driver ODBC do SQLite é incompatível com RevoScaleR. As revisões 0.88-0,91 e 0,93 e posteriores são conhecidas como compatíveis.

## <a name="see-also"></a>Confira também

[Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Solucionando problemas de aprendizado de máquina no SQL Server](machine-learning-troubleshooting-faq.md)
