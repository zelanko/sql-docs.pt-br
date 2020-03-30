---
title: Problemas conhecidos do Python e do R
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: da725efe691aae60bf9776bbe73f80227067d2e2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74200392"
---
# <a name="known-issues-in-sql-server-machine-learning-services"></a>Problemas conhecidos nos Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve problemas ou limitações conhecidos com os componentes de aprendizado de máquina que são fornecidos como uma opção em [Serviços de Machine Learning do SQL Server](what-is-sql-server-machine-learning.md) e [SQL Server 2016 R Services](r/sql-server-r-services.md).

## <a name="setup-and-configuration-issues"></a>Problemas de instalação e de configuração

Para obter uma descrição dos processos e ver as perguntas comuns relacionadas à instalação inicial e à configuração, confira [Perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md). Ali estão contidas informações sobre atualizações, instalação lado a lado e instalação de novos componentes de R ou Python.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. Resultados inconsistentes em computações do MKL devido a uma variável de ambiente ausente

**Aplica-se a:** Binários do R_SERVER 9.0, 9.1, 9.2 ou 9.3.

O R_SERVER usa a Intel MKL (Math Kernel Library). Em cálculos que envolvam a MKL, resultados inconsistentes poderão ocorrer caso o sistema não tenha uma variável de ambiente. 

Defina a variável de ambiente `'MKL_CBWR'=AUTO` para garantir a reprodutibilidade numérica condicional no R_SERVER. Para obter mais informações, confira [Introdução à CNR (Reprodutibilidade Numérica Condicional)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr).

**Solução alternativa**

1. No Painel de Controle, clique em **Sistema e Segurança** > **Sistema** > **Configurações Avançadas do Sistema** > **Variáveis de Ambiente**.

2. Crie uma variável de usuário ou do sistema. 

   + Defina o nome da variável como 'MKL_CBWR'.
   + Defina o 'Valor da variável' para 'AUTO'.

3. Reinicie o R_SERVER. No SQL Server, você pode reiniciar o serviço SQL Server Launchpad.

> [!NOTE]
> Caso você esteja executando o SQL Server 2019 no Linux, edite ou crie o *.bash_profile* no diretório base do usuário adicionando a linha `export MKL_CBWR="AUTO"`. Execute esse arquivo digitando `source .bash_profile` em um prompt de comando de Bash. Reinicie o R_SERVER digitando `Sys.getenv()` no prompt de comando do R.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. Erro de runtime de script R (regressão CU5-CU7 do SQL Server 2017)

Para o SQL Server 2017, nas atualizações cumulativas de 5 a 7, há uma regressão no arquivo **rlauncher.config** em que o caminho do arquivo do diretório temporário inclui um espaço. Essa regressão é corrigida em CU8.

O erro que você verá ao executar o script R incluirá as seguintes mensagens:

> *Não é possível se comunicar com o runtime do script 'R'. Verifique os requisitos do runtime do 'R'.*
>
> Mensagens STDERR do script externo: 
>
> *Erro fatal: não é possível criar 'R_TempDir'*

**Solução alternativa**

Aplique CU8 quando ele ficar disponível. Como alternativa, você pode recriar **rlauncher.config** executando **registerrext** com desinstalar/instalar em um prompt de comandos com privilégios elevados. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

O exemplo a seguir mostra os comandos com a instância padrão "MSSQL14.MSSQLSERVER" instalada em "C:\Program Files\Microsoft SQL Server\":

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. Não é possível instalar recursos de aprendizado de máquina do SQL Server em um controlador de domínio

Se você tentar instalar o SQL Server 2016 R Services ou Serviços de Machine Learning do SQL Server em um controlador de domínio, a instalação falhará com estes erros:

> *Erro durante o processo de instalação do recurso*
>
> *Não é possível localizar o grupo com a identidade*
>
> *Código de erro do componente: 0x80131509*

A falha ocorre porque, em um controlador de domínio, o serviço não pode criar as 20 contas locais necessárias para executar o aprendizado de máquina. Em geral, não recomendamos a instalação do SQL Server em um controlador de domínio. Para obter mais informações, confira [Boletim de suporte 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Instalar a versão mais recente do serviço para garantir a compatibilidade com o Microsoft R Client

Se você instalar a última versão do Microsoft R Client e usá-la para executar o R no SQL Server em um contexto de computação remota, poderá receber um erro como o seguinte:

> *Você está executando a versão 9.x.x do Microsoft R Client em seu computador, que é incompatível com o Microsoft R Server versão 8.x.x. Baixe e instale uma versão compatível.*

O SQL Server 2016 requer que as bibliotecas do R no cliente correspondam exatamente às bibliotecas do R no servidor. A restrição foi removida para versões posteriores ao R Server 9.0.1. No entanto, se você encontrar esse erro, verifique a versão das bibliotecas do R que é usada pelo cliente e o servidor e, se necessário, atualize o cliente para corresponder à versão do servidor.

Normalmente, a versão do R instalada com o SQL Server R Services é atualizada sempre que uma versão do serviço SQL Server é instalada. Para garantir que você sempre tenha as versões mais atualizadas dos componentes do R, instale todos os service packs.

Para assegurar a compatibilidade com o Microsoft R Client 9.0.0, é necessário instalar as atualizações descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).

Para evitar problemas com pacotes do R, você também pode atualizar a versão das bibliotecas do R que estão instaladas no servidor, alterando seu contrato de manutenção para usar a política de suporte do ciclo de vida moderno, conforme descrito na [próxima seção](#bkmk_sqlbindr). Quando você faz isso, a versão do R instalada com o SQL Server é atualizada segundo o mesmo cronograma usado para atualizações do servidor do Machine Learning (anteriormente Microsoft R Server).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="5-r-components-missing-from-cu3-setup"></a>5. Componentes do R ausentes da configuração da CU3

Um número limitado de máquinas virtuais do Azure foram provisionadas sem os arquivos de instalação do R que devem ser incluídos com SQL Server. O problema se aplica às máquinas virtuais provisionadas no período de 05/01/2018 a 23/01/2018. Esse problema também pode afetar as instalações locais, se você aplicou a atualização CU3 ao SQL Server 2017 durante o período de 05/01/2018 a 23/01/2018.

Foi fornecida uma versão de serviço que inclui a versão correta dos arquivos de instalação do R.

+ [Pacote de Atualização Cumulativa 3 para o SQL Server 2017 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

Para instalar os componentes e reparar SQL Server 2017 CU3, você deve desinstalar a CU3 e reinstalar a versão atualizada:

1. Baixe o arquivo de instalação atualizado da CU3, que inclui os instaladores do R.
2. Desinstale a CU3. No painel de controle, procure **Desinstalar uma atualização** e, em seguida, selecione "Hotfix 3015 para SQL Server 2017 (KB4052987) (64 bits)". Prossiga com as etapas de desinstalação.
3. Reinstale a atualização CU3 clicando duas vezes na atualização para KB4052987 que você acabou de baixar: `SQLServer2017-KB4052987-x64.exe`. Siga as instruções de instalação.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. Não é possível instalar os componentes do Python em instalações offline do SQL Server 2017 CTP 2.0 ou posterior

Se você instalar uma versão de pré-lançamento do SQL Server 2017 em um computador sem acesso à Internet, o instalador poderá falhar ao exibir a página que solicita a localização dos componentes do Python baixados. Nessa instância, você pode instalar o recurso Serviços de Machine Learning, mas não os componentes do Python.

Esse problema é corrigido na próxima versão do SSMS. Além disso, essa limitação não se aplica aos componentes do R.

**Aplica-se a:** SQL Server 2017 com Python

### <a name="warning-of-incompatible-version-when-you-connect-to-an-older-version-of-sql-server-r-services-from-a-client-by-using-sssqlv14_md"></a><a name="bkmk_sqlbindr"></a> Aviso de versão incompatível ao se conectar à versão anterior do SQL Server R Services por meio de um cliente usando o [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Ao executar código R em um contexto de computação do SQL Server 2016, você poderá ver o seguinte erro:

> *Você está executando a versão 9.0.0 do Cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

Esta mensagem será exibida se uma das duas afirmações a seguir for verdadeira:

+ Você instalou o R Server (autônomo) em um computador cliente usando o assistente de instalação do para [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
+ Você instalou o Microsoft R Server usando o [Windows Installer separado](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para garantir que o servidor e o cliente usem a mesma versão, talvez seja necessário usar _associação_, compatível com o Microsoft R Server 9.0 e versões posteriores, para atualizar os componentes do R em instâncias do SQL Server 2016. Para determinar se há suporte para atualizações disponível para sua versão do R Services, confira [Atualizar uma instância do R Services usando o SqlBindR.exe](install/upgrade-r-and-python.md).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. A instalação de versões de serviço do SQL Server 2016 poderá falhar ao instalar versões mais novas dos componentes do R

Quando você instala uma atualização cumulativa ou um service pack para o SQL Server 2016 em um computador que não está conectado à Internet, o assistente de instalação poderá falhar ao exibir o aviso que permite atualizar os componentes do R usando os arquivos CAB baixados. Essa falha normalmente ocorre quando vários componentes foram instalados juntos com o mecanismo de banco de dados.

Como alternativa, você pode instalar a versão de serviço usando a linha de comando e especificando o argumento `MRCACHEDIRECTORY`, conforme mostrado neste exemplo que instala atualizações CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obter os instaladores mais recentes, confira [Instalar componentes de aprendizado de máquina sem acesso à Internet](install/sql-ml-component-install-without-internet-access.md).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. Os serviços do Launchpad falham ao iniciar se a versão é diferente da versão do R

Se você instalar SQL Server R Services separadamente do mecanismo de banco de dados e as versões de build forem diferentes, você poderá ver o seguinte erro no log de eventos do sistema:

> *O serviço do SQL Server Launchpad falhou ao iniciar devido ao seguinte erro: O serviço não respondeu à solicitação de início ou de controle em um tempo oportuno.*

Por exemplo, esse erro poderá ocorrer se você instalar o mecanismo de banco de dados usando a versão de lançamento, aplicar um patch para atualizar o mecanismo de banco de dados e, em seguida, adicionar o recurso R Services usando a versão de lançamento.

Para evitar esse problema, use um utilitário como o Gerenciador de Arquivos para comparar as versões do Launchpad.exe com a versão de binários do SQL, tais como o sqldk.dll. Todos os componentes devem ter o mesmo número de versão. Se você atualizar um componente, lembre-se de aplicar a mesma atualização a todos os outros componentes instalados.

Procure o Launchpad na pasta `Binn` da instância. Por exemplo, em uma instalação padrão do SQL Server 2016, o caminho pode ser `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. Contextos de computação remota bloqueados por um firewall nas instâncias do SQL Server em execução em Máquinas Virtuais do Azure

Se você tiver instalado o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] em uma máquina virtual do Azure, não será possível usar contextos de computação que exijam o uso do workspace da máquina virtual. O motivo é que, por padrão, o firewall nas máquinas virtuais do Azure inclui uma regra que bloqueia o acesso de rede para contas de usuários locais de R.

Como alternativa, na VM do Azure, abra o **Firewall do Windows com Segurança Avançada**, selecione as **Regras de Saída** e desabilite a regra a seguir: **Bloquear o acesso à rede para contas de usuário local do R na instância MSSQLSERVER do SQL Server**. Você também pode deixar a regra habilitada, mas alterar a propriedade de segurança para **Permitir caso seja seguro**.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. Autenticação implícita em SQLEXPRESS

Quando você executar trabalhos do R em uma estação de trabalho de ciência de dados remota usando a Autenticação Integrada do Windows, o SQL Server usará a *autenticação implícita* para gerar as chamadas ODBC locais que poderão ser exigidas pelo script. No entanto, esse recurso não funcionou no build RTM do SQL Server Express Edition.

Para corrigir o problema, recomendamos atualizar para uma versão de serviço posterior.

Se não for possível atualizá-la, como alternativa, use um logon SQL para executar trabalhos remotos do R que podem exigir chamadas ODBC inseridas.

**Aplica-se a:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. Limites de desempenho quando as bibliotecas usadas pelo SQL Server são chamadas de outras ferramentas

É possível chamar as bibliotecas de aprendizado de máquina instaladas para o SQL Server de um aplicativo externo, tal como o RGui. Fazer isso pode ser a melhor maneira de realizar determinadas tarefas, assim como instalar novos pacotes ou executar testes ad hoc em amostras de código muito curtas. No entanto, fora do SQL Server, o desempenho pode ser limitado.

Por exemplo, mesmo se você estiver usando a Edição Enterprise do SQL Server, o R será executado no modo single-threaded, caso você execute o código R usando ferramentas externas. Para obter os benefícios de desempenho no SQL Server, inicie uma conexão SQL Server e use [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para chamar o runtime de script externo.

Em geral, evite chamar as bibliotecas de aprendizado de máquina que são usadas pelo SQL Server por meio de ferramentas externas. Se você precisar depurar o código R ou Python, normalmente será mais fácil fazer isso fora do SQL Server. Para obter as mesmas bibliotecas que estão no SQL Server, você pode instalar o Microsoft R Client, o [SQL Server 2017 Machine Learning Server (Autônomo)](install/sql-machine-learning-standalone-windows-install.md) ou o [SQL Server 2016 R (Autônomo)](install/sql-r-standalone-windows-install.md).

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. O SQL Server Data Tools não oferece suporte a permissões exigidas por scripts externos

Quando você usar o Visual Studio ou SQL Server Data Tools para publicar um projeto de banco de dados, se qualquer entidade tiver permissões específicas para a execução de script externo, você poderá receber um erro como este:

> *Modelo TSQL: erro detectado ao fazer engenharia reversa do banco de dados. A permissão não foi reconhecida e não foi importada.*

Atualmente, o modelo DACPAC não oferece suporte às permissões usadas pelo R Services ou Serviços de Machine Learning, tais como GRANT ANY EXTERNAL SCRIPT ou EXECUTE ANY EXTERNAL SCRIPT. Esse problema será corrigido em uma versão posterior.

Como alternativa, execute as instruções GRANT adicionais em um script pós-implantação.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. A execução de script externo é limitada devido aos valores padrão de governança de recursos

No Enterprise Edition, você pode usar pools de recursos para gerenciar processos de script externo. Em alguns builds de versões anteriores, a memória máxima que podia ser alocada para os processos do R era de 20%. Portanto, se o servidor tivesse 32 GB de RAM, os executáveis do R (RTerm.exe e BxlServer.exe) poderiam usar um máximo de 6,4 GB em uma única solicitação.

Se você encontrar limitações de recursos, verifique o padrão atual. Caso 20% não seja suficiente, confira a documentação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sobre como alterar esse valor.

**Aplica-se a:** SQL Server 2016 R Services, Edição Enterprise


### <a name="14-error-when-using-sp_execute_external_script-without-libcso-on-linux"></a>14. Erro ao usar `sp_execute_external_script` sem `libc++.so` no Linux

Em um computador Linux limpo que não tem o `libc++.so` instalado, a execução de uma consulta `sp_execute_external_script` (SPEES) com Java ou um idioma externo falha porque `commonlauncher.so` falha ao carregar `libc++.so`.

Por exemplo:

```sql
EXECUTE sp_execute_external_script @language = N'Java'
    , @script = N'JavaTestPackage.PassThrough'
    , @parallel = 0
    , @input_data_1 = N'select 1'
WITH RESULT SETS((col1 INT NOT NULL))
GO
```

Isso falha com uma mensagem semelhante à seguinte:

```text
Msg 39012, Level 16, State 14, Line 0

Unable to communicate with the runtime for 'Java' script for request id: 94257840-1704-45E8-83D2-2F74AEB46CF7. Please check the requirements of 'Java' runtime.
```

Os logs de `mssql-launchpadd` mostrarão uma mensagem de erro semelhante à seguinte:

```text
Oct 18 14:03:21 sqlextmls launchpadd[57471]: [launchpad] 2019/10/18 14:03:21 WARNING: PopulateLauncher failed: Library /opt/mssql-extensibility/lib/commonlauncher.so not loaded. Error: libc++.so.1: cannot open shared object file: No such file or directory
```

**Solução alternativa**

Você pode usar uma das soluções alternativas a seguir:

1. Copie `libc++*` de `/opt/mssql/lib` para o caminho do sistema padrão `/lib64`

1. Adicione as entradas a seguir para `/var/opt/mssql/mssql.conf` a fim de expor o caminho:

   ```text
   [extensibility]
   readabledirectories = /opt/mssql
   ```

**Aplica-se a:** SQL Server 2019 no Linux

## <a name="r-script-execution-issues"></a>Problemas de execução do script R

Esta seção contém problemas conhecidos que são específicos da execução do R no SQL Server, bem como alguns problemas relacionados às bibliotecas e ferramentas do R publicadas pela Microsoft, incluindo o RevoScaleR.

Para problemas conhecidos adicionais que podem afetar as soluções de R, confira o site do [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues).

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. Aviso de acesso negado ao executar scripts R no SQL Server em uma localização não padrão

Se a instância do SQL Server tiver sido instalada em uma localização não padrão, por exemplo, fora da pasta `Program Files`, o aviso ACCESS_DENIED será gerado quando você tentar executar scripts que instalam um pacote. Por exemplo:

> *Em `normalizePath(path.expand(path), winslash, mustWork)`: path[2]="~ExternalLibraries/R/8/1": Acesso negado*

O motivo é que uma função do R tenta ler o caminho e falha caso o grupo de usuários interno **SQLRUserGroup** não tenha acesso de leitura. O aviso gerado não bloqueia a execução do script R atual, mas o aviso pode ocorrer repetidamente sempre que o usuário executar qualquer outro script R.

Se você tiver instalado SQL Server na localização padrão, esse erro não ocorrerá, pois todos os usuários do Windows têm permissões de leitura na pasta `Program Files`.

Esse problema será resolvido em uma versão futura do serviço. Como alternativa, forneça acesso de leitura para todas as pastas pai de `ExternalLibraries` ao grupo **SQLRUserGroup**.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. Erro de serialização entre as versões antiga e nova do RevoScaleR

Ao passar um modelo usando um formato serializado para uma instância remota do SQL Server, você pode receber o erro: 

> *Erro em memDecompress(data, type = decompress) erro interno -3 em memDecompress(2).*

Esse erro é gerado se você salvou o modelo usando uma versão recente da função de serialização, [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), mas a instância SQL Server em que você desserializa o modelo tem uma versão mais antiga das APIs do RevoScaleR, do SQL Server 2017 CU2 ou anterior.

Como alternativa, você pode atualizar a instância do SQL Server 2017 para CU3 ou posterior.

O erro não será exibido se a versão da API for a mesma ou se você estiver movendo um modelo salvo com uma função de serialização mais antiga para um servidor que use uma versão mais recente da API de serialização.

Em outras palavras, use a mesma versão do RevoScaleR para operações de serialização e desserialização.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-_learningrate_-parameter-in-tree-and-forest-models"></a>3. A pontuação em tempo real não manipula corretamente o parâmetro _learningRate_ em modelos de árvore e floresta

Se criar um modelo usando uma árvore de decisão ou um método de floresta de decisão e especificar a taxa de aprendizado, você poderá ver resultados inconsistentes ao usar `sp_rxpredict` ou a função SQL `PREDICT`, em comparação com o uso de `rxPredict`.

A causa é um erro na API que processa modelos serializados e é limitada ao parâmetro `learningRate`: por exemplo, em [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) ou

Esse problema será resolvido em uma versão futura do serviço.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. Limitações na afinidade do processador para trabalhos do R

No build da versão inicial do SQL Server 2016, você podia definir a afinidade do processador somente para CPUs no primeiro grupo k. Por exemplo, se o servidor for um computador de dois soquetes com dois grupos k, apenas os processadores do primeiro grupo k serão usados para os processos do R. A mesma limitação se aplica ao configurar a governança de recursos para trabalhos de script do R.

Esse problema é corrigido no SQL Server 2016 Service Pack 1. Recomendamos atualizar para uma versão posterior do serviço.

**Aplica-se a:** SQL Server 2016 R Services versão RTM

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5. Não é possível fazer alterações nos tipos de coluna durante a leitura de dados em um contexto de computação do SQL Server

Se o contexto de computação estiver definido como a instância do SQL Server, não será possível usar o argumento _colClasses_ (ou outros argumentos semelhante) para alterar o tipo de dados das colunas no código R.

Por exemplo, a seguinte instrução resultará em um erro se a coluna CRSDepTimeStr ainda não for um inteiro:

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

Como alternativa, você pode reescrever a consulta SQL para usar CAST ou CONVERT e apresentar os dados ao R usando o tipo de dados correto. Em geral, o desempenho é melhor ao trabalhar com os dados usando o SQL em vez de alterar dados no código R.

**Aplica-se a:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. Limites no tamanho de modelos serializados

Quando salva um modelo em uma tabela do SQL Server, você deve serializar o modelo e salvá-lo em um formato binário. Teoricamente, o tamanho máximo de um modelo que pode ser armazenado com esse método é 2 GB, que é o tamanho máximo das colunas varbinary no SQL Server.

Se você precisar usar modelos maiores, as seguintes soluções alternativas estarão disponíveis:

+ Tome medidas para reduzir o tamanho do seu modelo. Alguns pacotes R de software livre incluem uma grande quantidade de informações no objeto de modelo e muitas dessas informações podem ser removidas para implantação. 
+ Use a seleção de recursos para remover as colunas desnecessárias.
+ Se você estiver usando um algoritmo de software livre, considere uma implementação semelhante usando o algoritmo correspondente em MicrosoftML ou RevoScaleR. Esses pacotes foram otimizados para cenários de implantação.
+ Depois que o modelo tiver sido racionalizado e o tamanho reduzido usando as etapas anteriores, veja se a função [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) no R base pode ser usada para reduzir o tamanho do modelo antes de passá-lo para o SQL Server. Essa opção é melhor quando o modelo está perto do limite de 2 GB.
+ Para modelos maiores, você pode usar o recurso [FileTable](../relational-databases/blob/filetables-sql-server.md) do SQL Server para armazenar os modelos, em vez de usar uma coluna varbinary.

    Para usar FileTables, você deve adicionar uma exceção de firewall, pois os dados armazenados em FileTables são gerenciados pelo driver de sistema de arquivos do fluxo de arquivos no SQL Server e as regras de firewall padrão bloqueiam o acesso ao arquivo de rede. Para obter mais informações, confira [Habilitar pré-requisitos para FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md).

    Depois de habilitar o FileTable, para gravar o modelo, você obtém um caminho do SQL usando a API do FileTable e, em seguida, grava o modelo nessa localização por meio do seu código. Quando precisar ler o modelo, você obterá o caminho do SQL e, em seguida, chamará o modelo usando o caminho por meio do seu script. Para obter mais informações, confira [Acessar FileTables com APIs de entrada e saída de arquivo](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-ssnoversion-compute-context"></a>7. Evitar a limpeza dos workspaces ao executar o código R em um contexto de computação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Se você usar um comando do R para limpar o workspace de objetos durante a execução de código R em um contexto de computação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou se limpar o workspace como parte de um script do R chamado pelo uso de [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), você poderá receber este erro: *objeto do workspace revoScriptConnection não encontrado*

O`revoScriptConnection` é um objeto no workspace do R que contém informações sobre uma sessão do R chamada por meio de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, se o código R incluir um comando para limpar o workspace (como `rm(list=ls()))`), todas as informações sobre a sessão e outros objetos no workspace do R também serão limpos.

Como alternativa, evite a limpeza indiscriminada de variáveis e outros objetos ao executar o R no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Embora a limpeza do workspace seja comum ao trabalhar no console do R, ela poderá trazer consequências indesejadas.

+ Para excluir variáveis específicas, use a função `remove` do R: por exemplo, `remove('name1', 'name2', ...)`
+ Se houver várias variáveis a serem excluídas, salve os nomes das variáveis temporárias em uma lista e execute a coleta de lixo periódica.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. Restrições sobre dados que podem ser fornecidos como entrada para um script R

O sistema não permite usar os seguintes tipos de resultados de consulta em um script R:

- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência às colunas AlwaysEncrypted.
  
- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência à colunas mascaradas.
  
     Se precisar usar dados mascarados em um script R, uma solução alternativa é copiar os dados em uma tabela temporária e usar esses dados.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. O uso de cadeias de caracteres como fatores pode levar à degradação do desempenho

Usar variáveis de tipo de cadeia de caracteres como fatores pode aumentar muito a quantidade de memória usada para operações de R. Esse é um problema conhecido com o R em geral e há muitos artigos sobre o assunto. Por exemplo, confira [Factors are not first-class citizens in R (Fatores não são cidadãos de primeira classe no R), por John Mount, em R-bloggers](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) ou [stringsAsFactors: An unauthorized biography (Uma biografia não autorizada), por Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Embora o problema não seja específico do SQL Server, ele pode afetar muito o desempenho da execução de código R no SQL Server. Em geral, as cadeias de caracteres são armazenadas como varchar ou nvarchar e, se uma coluna de dados de cadeia tem muitos valores exclusivos, o processo de convertê-las internamente para inteiros e voltar para cadeias por R pode até mesmo levar a erros de alocação de memória.

Se você realmente não precisa de um tipo de dados String para outras operações, o mapeamento dos valores de cadeia de caracteres para um tipo de dados numérico (inteiro) como parte da preparação de dados é benéfico para o desempenho e para escalonamento.

Para obter uma discussão sobre esse problema e outras dicas, confira [Desempenho para R Services – otimização de dados](r/r-and-data-optimization-r-services.md).

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. Os argumentos *varsToKeep* e *varsToDrop* não são compatíveis com fontes de dados do SQL Server

Quando você usa a função rxDataStep para gravar resultados em uma tabela, usar *varsToKeep* e *varsToDrop* é uma maneira útil de especificar as colunas a serem incluídas ou excluídas como parte da operação. No entanto, esses argumentos não são compatíveis com fontes de dados do SQL Server.

### <a name="11-limited-support-for-sql-data-types-in-sp_execute_external_script"></a>11. Suporte limitado para tipos de dados SQL em sp\_execute\_external\_script

Nem todos os tipos de dados compatíveis com o SQL podem ser usados no R. Como alternativa, considere a conversão do tipo de dados incompatível para um tipo de dados compatível antes de passar os dados para sp\_execute\_external\_script.

Para obter mais informações, confira [Tipos de dados e bibliotecas do R](r/r-libraries-and-data-types.md).

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Possível corrupção de cadeia de caracteres usando cadeias de caracteres Unicode em colunas varchar

A passagem de dados Unicode em colunas varchar de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para R/Python pode resultar em corrupção de cadeia de caracteres. Isso ocorre porque a codificação para essa cadeia de caracteres Unicode em agrupamentos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode não corresponder à codificação UTF-8 padrão usada em R/Python. 

Para enviar dados de cadeia de caracteres não ASCII do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para R/Python, use a codificação UTF-8 (disponível no [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) ou use o tipo nvarchar para eles.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-sp_execute_external_script"></a>13. Somente um valor do tipo `raw` pode ser retornado de `sp_execute_external_script`

Quando um tipo de dados binário é retornado de R (o tipo de dados **brutos** de R), o valor precisa ser enviado no quadro de dados de saída.

Com tipos de dados diferentes de **bruto**, é possível retornar valores de parâmetro junto com os resultados do procedimento armazenado apenas adicionando a palavra-chave OUTPUT. Para obter mais informações, confira [Parâmetros](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Caso pretenda usar vários conjuntos de saída que incluam valores do tipo **bruto**, uma possível solução alternativa é fazer várias chamadas do procedimento armazenado e enviar os conjuntos de resultados de volta para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando o ODBC.

### <a name="14-loss-of-precision"></a>14. Perda de precisão

Já que o [!INCLUDE[tsql](../includes/tsql-md.md)] e o R dão suporte a diferentes tipos de dados, os tipos de dados numéricos podem sofrer perda de precisão durante a conversão.

Para obter mais informações sobre a conversão implícita de tipos de dados, confira [Tipos de dados e bibliotecas do R](r/r-libraries-and-data-types.md).

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. Erro de escopo de variável ao usar o parâmetro transformFunc

Para transformar os dados ao modelar, você pode passar um argumento *transformFunc* em uma função como `rxLinmod` ou `rxLogit`. No entanto, as chamadas de função aninhadas podem gerar erros de escopo no contexto de computação do SQL Server, mesmo que as chamadas funcionem corretamente no contexto de computação local.

> *O conjunto de dados de exemplo para a análise não tem nenhuma variável*

Por exemplo, digamos que você tenha definido duas funções `f` e `g` no ambiente global local e então `g` chama `f`. Nas chamadas distribuídas ou remotas envolvendo `g`, a chamada para `g` pode falhar com esse erro porque `f` não pode ser encontrado, mesmo caso você passe `f` e `g` para a chamada remota.

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

Durante a leitura de colunas **varchar** de um banco de dados, o sistema retira os espaços em branco. Para evitar isso, coloque as cadeias de caracteres entre caracteres de espaço não em branco.

Quando funções como `rxDataStep` são usadas para criar tabelas de bancos de dados que contêm colunas **varchar**, a largura da coluna é calculada com base em uma amostra dos dados. Se a largura for variável, talvez seja necessário preencher todas as cadeias de caracteres com um comprimento comum.

O uso de uma transformação para alterar o tipo de dados de uma variável não terá suporte quando chamadas repetidas para `rxImport` ou `rxTextToXdf` sejam usadas para importar e anexar linhas, combinando vários arquivos de entrada em um único arquivo .xdf.

### <a name="17-limited-support-for-rxexec"></a>17. Suporte limitado para rxExec

No SQL Server 2016, a função `rxExec` fornecida pelo pacote RevoScaleR pode ser usada somente no modo de thread único.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. Aumentar o tamanho máximo do parâmetro para dar suporte à função rxGetVarInfo

Se usar conjuntos de dados com um número muito grande de variáveis (por exemplo, mais de 40.000), defina o sinalizador `max-ppsize` quando iniciar o R para usar funções como `rxGetVarInfo`. O sinalizador `max-ppsize` especifica o tamanho máximo da pilha de proteção do ponteiro.

Se estiver usando o console de R (por exemplo, em RGui.exe ou em RTerm.exe), defina o valor máximo de _max-ppsize_ para 500000 digitando:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. Problemas com a função rxDTree

Atualmente, a função `rxDTree` não tem suporte para transformações dentro da fórmula. Não temos suporte para o uso da sintaxe `F()` , em especial, para a criação de fatores dinâmicos. No entanto, os dados numéricos são compartimentalizados automaticamente.

Os fatores ordenados são tratados da mesma forma que os fatores de todas as funções de análise RevoScaleR, exceto o `rxDTree`.

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20. Data.table como um OutputDataSet em R

O uso de `data.table` como um `OutputDataSet` em R não é compatível com o SQL Server 2017 CU13 (Atualização Cumulativa 13) e anteriores. A seguinte mensagem pode aparecer:

``` text
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

`data.table` como um `OutputDataSet` em R não é compatível com o SQL Server 2017 CU14 (Atualização Cumulativa 14) e posteriores.

### <a name="21-running-a-long-script-fails-while-installing-a-library"></a>21. A execução de um script longo falha durante a instalação de uma biblioteca

Executar uma sessão de script externo de execução prolongada e fazer paralelamente com que o dbo tente instalar uma biblioteca em um banco de dados diferente pode encerrar o script.

Por exemplo, executar esse script externo em relação ao mestre:

```sql
USE MASTER
DECLARE @language nvarchar(1) = N'R'
DECLARE @script nvarchar(max) = N'Sys.sleep(100)'
DECLARE @input_data_1 nvarchar(max) = N'select 1'
EXEC sp_execute_external_script @language = @language, @script = @script, @input_data_1 = @input_data_1 with result sets none
go
```

Enquanto o dbo instala paralelamente uma biblioteca em LibraryManagementFunctional:

```sql
USE [LibraryManagementFunctional]
go

CREATE EXTERNAL LIBRARY [RODBC] FROM (CONTENT = N'/home/ani/var/opt/mssql/data/RODBC_1.3-16.tar.gz') WITH (LANGUAGE = 'R')
go

DECLARE @language nvarchar(1) = N'R'
DECLARE @script nvarchar(14) = N'library(RODBC)'
DECLARE @input_data_1 nvarchar(8) = N'select 1'
EXEC sp_execute_external_script @language = @language, @script = @script, @input_data_1 = @input_data_1
go
```

O script externo de execução prolongada anterior em relação ao Mestre será encerrado com a seguinte mensagem de erro:

> *Um erro de script 'R' ocorreu durante a execução de 'sp_execute_external_script' com HRESULT 0x800704d4.*

**Solução alternativa**

Não execute a instalação da biblioteca em paralelo à consulta de execução prolongada. Ou execute novamente a consulta de execução prolongada após a conclusão da instalação.

**Aplica-se a:** somente o SQL Server 2019 no Linux e os Clusters de Big Data.

## <a name="python-script-execution-issues"></a>Problemas de execução de script Python

Esta seção contém problemas conhecidos que são específicos da execução do Python no SQL Server, bem como problemas relacionados aos pacotes do Python publicados pela Microsoft, incluindo [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. A chamada para o modelo previamente treinado falhará se o caminho para o modelo for muito longo

Se você tiver instalado os modelos pré-treinados em uma versão inicial do SQL Server 2017, o caminho completo para o arquivo de modelo treinado poderá ser muito longo para que o Python os leia. Essa limitação é corrigida em uma versão posterior do serviço.

Há várias soluções alternativas possíveis:

+ Ao instalar os modelos pré-treinados, escolha uma localização personalizado.
+ Se possível, instale a instância de SQL Server em um caminho de instalação personalizado com um caminho mais curto, tal como C:\SQL\MSSQL14.MSSQLSERVER.
+ Use o utilitário [fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) do Windows para criar um link físico que mapeia o arquivo de modelo para um caminho mais curto.
+ Atualize para a versão mais recente do serviço.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. Erro ao salvar o modelo serializado para o SQL Server

Quando você passa um modelo para uma instância remota do SQL Server e tenta ler o modelo binário usando a função `rx_unserialize` em [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), você pode receber o erro: 

> *NameError: o nome 'rx_unserialize_model' não está definido*

Esse erro é gerado se você salvou o modelo usando uma versão recente da função de serialização, mas a instância do SQL Server em que você desserializa o modelo não reconhece a API de serialização.

Para solucionar o problema, é possível atualizar a instância do SQL Server 2017 para CU3 ou posterior.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. A falha ao inicializar uma variável varbinary causa um erro em BxlServer

Se você executar o código Python no SQL Server usando `sp_execute_external_script` e o código tiver variáveis de saída do tipo varbinary(max), varchar(max) ou tipos semelhantes, a variável deverá ser inicializada ou definida como parte do seu script. Caso contrário, o componente de troca de dados, BxlServer, gerará um erro e deixará de funcionar.

Essa limitação será corrigida em uma versão de serviço futura. Como alternativa, verifique se a variável é inicializada dentro do script Python. Qualquer valor válido pode ser usado, assim como nos exemplos a seguir:

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

Do SQL Server 2017 CU2 em diante, a seguinte mensagem pode aparecer mesmo que o código Python seja executado com êxito:

> *Mensagens STDERR do script externo:* 
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state é usado antes da declaração global*

Esse problema foi corrigido no SQL Server 2017 CU3 (Atualização Cumulativa 3). 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5. Os tipos de dados numérico, decimal e money não são compatíveis

Do SQL Server 2017 CU12 (Atualização Cumulativa 12) em diante, os tipos de dados numérico, decimal e money em WITH RESULT SETS não são compatíveis ao usar o Python com `sp_execute_external_script`. As seguintes mensagens podem aparecer:

> *[Código: 39004, estado do SQL: S1000] Um erro de script 'Python' ocorreu durante a execução de 'sp_execute_external_script' com HRESULT 0x80004004.*
>
> *[Código: 39019, estado do SQL: S1000] Ocorreu um erro de script externo:*
>
> *Erro de SqlSatelliteCall: Tipo incompatível no esquema de saída. Tipos compatíveis: bit, smallint, int, DateTime, SmallMoney, real e float; char e varchar são parcialmente compatíveis.*

Isso foi corrigido no SQL Server 2017 CU14 (Atualização Cumulativa 14).

### <a name="6-bad-interpreter-error-when-installing-python-packages-with-pip-on-linux"></a>6. Erro de interpretador incorreto ao instalar pacotes do Python com pip no Linux 

No SQL Server 2019, se você tentar usar o **pip**. Por exemplo:

```bash
/opt/mssql/mlservices/runtime/python/bin/pip -h
```

Você receberá então este erro:

> *bash: /opt/mssql/mlservices/runtime/python/bin/pip: /opt/microsoft/mlserver/9.4.7/bin/python/python: bad interpreter: Esse arquivo ou diretório não existe*

**Solução alternativa**

Instale o **pip** da [PyPA (autoridade de pacote do Python)](https://www.pypa.io):

```bash
wget 'https://bootstrap.pypa.io/get-pip.py' 
/opt/mssql/mlservices/bin/python/python ./get-pip.py 
```

**Recomendação**

Confira [Instalar pacotes Python com o sqlmlutils](package-management/install-additional-python-packages-on-sql-server.md).

**Aplica-se a:** SQL Server 2019 no Linux

### <a name="7-unable-to-install-python-packages-using-pip-after-installing-sql-server-2019-on-windows"></a>7. Não é possível instalar os pacotes do Python usando o pip após a instalação do SQL Server 2019 no Windows

Depois de instalar o SQL Server 2019 no Windows, a tentativa de instalar um pacote do Python via **pip** por meio de uma linha de comando do DOS falhará. Por exemplo:

```bash
pip install quantfolio
```

Isso retornará o erro a seguir:

> *O pip é configurado com locais que exigem TLS/SSL, no entanto, o módulo SSL no Python não está disponível.*

Esse é um problema específico do pacote Anaconda. Ele será corrigido em uma versão futura do serviço.

**Solução alternativa**

Copie os seguintes arquivos:

+ `libssl-1_1-x64.dll`
+ `libcrypto-1_1-x64.dll`

da pasta <br>
`C:\Program Files\Microsoft SQL Server\MSSSQL15.MSSQLSERVER\PYTHON_SERVICES\Library\bin`

para a pasta <br>
`C:\Program Files\Microsoft SQL Server\MSSSQL15.MSSQLSERVER\PYTHON_SERVICES\DLLs`

Em seguida, abra um novo prompt do shell de comando do DOS.

**Aplica-se a:** SQL Server 2019 no Windows

### <a name="8-error-when-using-sp_execute_external_script-without-libcaboso-on-linux"></a>8. Erro ao usar `sp_execute_external_script` sem `libc++abo.so` no Linux

Em um computador Linux limpo que não tem o `libc++abi.so` instalado, a execução de uma consulta `sp_execute_external_script` (SPEES) falha com um erro "Esse arquivo ou diretório não existe".

Por exemplo:

```text
EXEC sp_execute_external_script
    @language = N'Python'
    , @script = N'
OutputDataSet = InputDataSet'
    , @input_data_1 = N'select 1'
    , @input_data_1_name = N'InputDataSet'
    , @output_data_1_name = N'OutputDataSet'
    WITH RESULT SETS (([output] int not null));
Msg 39012, Level 16, State 14, Line 0
Unable to communicate with the runtime for 'Python' script for request id: 94257840-1704-45E8-83D2-2F74AEB46CF7. Please check the requirements of 'Python' runtime.
STDERR message(s) from external script:

Failed to load library /opt/mssql-extensibility/lib/sqlsatellite.so with error libc++abi.so.1: cannot open shared object file: No such file or directory.

SqlSatelliteCall error: Failed to load library /opt/mssql-extensibility/lib/sqlsatellite.so with error libc++abi.so.1: cannot open shared object file: No such file or directory.
STDOUT message(s) from external script:
SqlSatelliteCall function failed. Please see the console output for more information.
Traceback (most recent call last):
  File "/opt/mssql/mlservices/libraries/PythonServer/revoscalepy/computecontext/RxInSqlServer.py", line 605, in rx_sql_satellite_call
    rx_native_call("SqlSatelliteCall", params)
  File "/opt/mssql/mlservices/libraries/PythonServer/revoscalepy/RxSerializable.py", line 375, in rx_native_call
    ret = px_call(functionname, params)
RuntimeError: revoscalepy function failed.
Total execution time: 00:01:00.387
```

**Solução alternativa**

Execute o comando a seguir:

```bash
sudo cp /opt/mssql/lib/libc++abi.so.1 /opt/mssql-extensibility/lib/
```

**Aplica-se a:** SQL Server 2019 no Linux

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open

Esta seção lista problemas específicos à conectividade, ao desenvolvimento e às ferramentas de desempenho do R fornecidas pela Revolution Analytics. Essas ferramentas foram fornecidas em versões de pré-lançamento anteriores do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

Em geral, recomendamos a desinstalação dessas versões anteriores e a instalação da última versão do SQL Server ou do Microsoft R Server.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. O Revolution R Enterprise não é compatível

A instalação do Revolution R Enterprise lado a lado com uma versão do [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] não é compatível.

Se tiver uma licença existente do Revolution R Enterprise, coloque-a em um computador separado, na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e na estação de trabalho que pretende usar para se conectar à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Algumas versões de pré-lançamento do [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluíram um ambiente de desenvolvimento do R para o Windows criado pela Revolution Analytics. Essa ferramenta não é mais fornecida e não é compatível.

Para obter compatibilidade com o [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], recomendamos que você instale o Microsoft R Client em seu lugar. As [Ferramentas do R para Visual Studio](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019) e o [Visual Studio Code](https://code.visualstudio.com/) também dão suporte a soluções do Microsoft R.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. Problemas de compatibilidade com o driver ODBC do SQLite e o RevoScaleR

A revisão 0.92 do driver ODBC do SQLite é incompatível com o RevoScaleR. As revisões 0.88-0.91, a 0.93 e as demais posteriores são tidas como compatíveis.

## <a name="next-steps"></a>Próximas etapas

[Como solucionar problemas de aprendizado de máquina no SQL Server](machine-learning-troubleshooting-faq.md)
