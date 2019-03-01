---
title: Problemas conhecidos para a linguagem R e a integração do Python - serviços do SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fd6f67e3095af0f1a53ed533ea9b763d52547e39
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018062"
---
# <a name="known-issues-in-machine-learning-services"></a>Problemas conhecidos no serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve problemas conhecidos ou limitações com componentes de aprendizado de máquina que são fornecidos como uma opção na [SQL Server 2016 R Services](install/sql-r-services-windows-install.md) e [serviços de aprendizado de máquina do SQL Server 2017 com R e Python](install/sql-machine-learning-services-windows-install.md).

## <a name="setup-and-configuration-issues"></a>Problemas de instalação e configuração

Para obter uma descrição dos processos e perguntas comuns relacionadas a instalação e configuração inicial, consulte [perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md). Ele contém informações sobre atualizações, a instalação lado a lado e a instalação de novos componentes de R ou Python.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. Resultados inconsistentes em cálculos de MKL devido à ausência da variável de ambiente

**Aplica-se a:** Binários R_SERVER 9.0, 9.1, 9.2 ou 9.3.

R_SERVER usa a Intel MKL Math Kernel Library (). Para cálculos que envolvem MKL, poderão ocorrer resultados inconsistentes se o sistema está sem uma variável de ambiente. 

Defina a variável de ambiente `'MKL_CBWR'=AUTO` para garantir reprodutibilidade numérica condicional em R_SERVER. Para obter mais informações, consulte [Introdução a capacidade de reprodução numéricos condicional (CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr).

**Solução alternativa**

1. No painel de controle, clique em **sistema e segurança** > **sistema** > **configurações avançadas do sistema**  >   **Variáveis de ambiente**.

2. Crie uma nova variável de sistema ou usuário. 

  + Defina o nome da variável à 'MKL_CBWR'.
  + Defina o 'valor da variável' como 'AUTO'.

3. Reinicie o R_SERVER. No SQL Server, você pode reiniciar o serviço Launchpad do SQL Server.

> [!NOTE]
> Se você estiver executando o SQL Server de 2019 Preview no Linux, edite ou crie *. bash_profile* em seu diretório base do usuário, adicionando a linha `export MKL_CBWR="AUTO"`. Execute esse arquivo digitando `source .bash_profile` em um prompt de comando do bash. Reiniciar R_SERVER digitando `Sys.getenv()` no prompt de comando de R.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. Erro de tempo de execução do Script R (SQL Server 2017 CU5 CU7 regressão)

Para o SQL Server 2017, em 5 a 7, as atualizações cumulativas, há uma regressão na **rlauncher** onde o caminho de arquivo do diretório temporário inclui um espaço de arquivo. Essa regressão foi corrigido no CU8.

O erro, que você verá ao executar script R inclui as seguintes mensagens:

> *Não é possível se comunicar com o tempo de execução de script 'R'. Verifique se os requisitos de tempo de execução 'R'.*
>
> Mensagens STDERR do script externo: 
>
> *Erro fatal: não é possível criar 'R_TempDir'*

**Solução alternativa**

Aplica CU8 quando ele estiver disponível. Como alternativa, você pode recriar **rlauncher** executando **registerrext** com desinstale/instale em um prompt de comando com privilégios elevados. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

O exemplo a seguir mostra os comandos com a instância padrão "MSSQL14. MSSQLSERVER"instalado em" C:\Program Files\Microsoft SQL Server\":

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. Não é possível instalar os recursos de aprendizado de máquina do SQL Server em um controlador de domínio

Se você tentar instalar o SQL Server 2016 R Services ou serviços de aprendizado de máquina do SQL Server 2017 em um controlador de domínio, a instalação falha, com esses erros:

> *Ocorreu um erro durante o processo de instalação do recurso*
> 
> *Não é possível localizar o grupo de identidade*
> 
> *Código de erro do componente: 0x80131509*

A falha ocorre porque, em um controlador de domínio, o serviço não é possível criar as 20 contas locais necessárias para executar o aprendizado de máquina. Em geral, não recomendamos a instalação do SQL Server em um controlador de domínio. Para obter mais informações, consulte [boletim suporte 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Instalar a versão mais recente do serviço para garantir a compatibilidade com o Microsoft R Client

Se você instala a versão mais recente do Microsoft R Client e usá-lo para executar o R no SQL Server em um contexto de computação remota, você poderá receber um erro semelhante ao seguinte:

> *Você está executando a versão 9.x.x do Microsoft R Client em seu computador, o que é incompatível com o Microsoft R Server versão 8.x.x. Baixe e instale uma versão compatível.*

SQL Server 2016 requer que as bibliotecas do R no cliente correspondem exatamente as bibliotecas do R no servidor. A restrição foi removida para versões mais tarde do que o R Server 9.0.1. No entanto, se você encontrar esse erro, verifique se a versão das bibliotecas do R que é usada pelo seu cliente e o servidor e, se necessário, atualize o cliente de acordo com a versão do servidor.

A versão do R que é instalado com o SQL Server R Services é atualizada sempre que uma versão de serviço do SQL Server está instalada. Para garantir que você sempre tenha as versões mais atualizadas dos componentes do R, certifique-se de instalar todos os service packs.

Para garantir a compatibilidade com o cliente do Microsoft R 9.0.0, instalar as atualizações que são descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).

Para evitar problemas com pacotes de R, você também pode atualizar a versão das bibliotecas do R são instalados no servidor, alterando seu contrato de serviço para usar a política de suporte do ciclo de vida moderno, conforme descrito em [a próxima seção](#bkmk_sqlbindr). Quando você fizer isso, a versão do R que é instalado com o SQL Server é atualizada na mesma agenda usada para atualizações de machine Learning Server (anteriormente conhecido como Microsoft R Server).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="5-r-components-missing-from-cu3-setup"></a>5. Componentes de R ausentes da configuração CU3

Um número limitado de máquinas virtuais do Azure foram provisionado sem os arquivos de instalação do R que devem ser incluídos com o SQL Server. O problema se aplica a máquinas virtuais provisionadas no período de 2018-01-05 para 2018-01-23. Esse problema também pode afetar as instalações locais, se você aplicou a atualização CU3 do SQL Server 2017 durante o período de 2018-01-05 para 2018-01-23.

Uma versão de serviço foi fornecido para que inclui a versão correta dos arquivos de instalação de R.

+ [Pacote de atualização cumulativa 3 para SQL Server 2017 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

Para instalar os componentes e reparar o SQL Server 2017 CU3, você deve desinstalar CU3 e reinstalar a versão atualizada:

1. Baixe o arquivo de instalação atualizado CU3, que inclui os instaladores do R.
2. Desinstale CU3. No painel de controle, pesquise **desinstalar uma atualização**e, em seguida, selecione "Hotfix 3015 do SQL Server 2017 (KB4052987) (64 bits)". Prossiga com as etapas de desinstalação.
3. Reinstalar a atualização de CU3, clicando duas vezes na atualização para que você acabou de baixar KB4052987: `SQLServer2017-KB4052987-x64.exe`. Siga as instruções de instalação.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. Não é possível instalar componentes do Python em instalações offline do SQL Server 2017 CTP 2.0 ou posterior

Se você instalar uma versão de pré-lançamento do SQL Server 2017 em um computador sem acesso à internet, o instalador poderá falhar ao exibir a página que solicita o local dos componentes do Python baixados. Nesse caso, você pode instalar o recurso de serviços de aprendizado de máquina, mas não os componentes do Python.

Esse problema é corrigido na versão de lançamento. Além disso, essa limitação não se aplica aos componentes do R.

**Aplica-se a:** SQL Server 2017 com o Python

### <a name="bkmk_sqlbindr"></a> Aviso de versão incompatível ao se conectar a uma versão anterior do SQL Server R Services de um cliente usando o [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Quando você executa o código R no contexto de computação de um SQL Server 2016, você poderá ver o seguinte erro:

> *Você está executando a versão 9.0.0 do Cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

Esta mensagem é exibida se uma das duas instruções a seguir for verdadeira,

+ Você instalou o R Server (autônomo) em um computador cliente usando o Assistente para instalação [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
+ Você instalou o Microsoft R Server usando o [separar o instalador do Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para garantir que o servidor e cliente usam a mesma versão que você talvez precise usar _associação_, com suporte para o Microsoft R Server 9.0 e versões posteriores atualizar os componentes de R em instâncias do SQL Server 2016. Para determinar se há suporte para atualizações disponível para sua versão do R Services, consulte [atualiza uma instância do R Services usando SqlBindR.exe](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. A instalação de versões de serviço do SQL Server 2016 poderá falhar ao instalar versões mais novas dos componentes do R

Quando você instala uma atualização cumulativa ou instala um service pack do SQL Server 2016 em um computador que não está conectado à internet, o Assistente de instalação poderá falhar ao exibir o prompt que permite que você atualize os componentes do R por meio de arquivos CAB baixados. Normalmente, essa falha ocorre quando vários componentes foram instalados junto com o mecanismo de banco de dados.

Como alternativa, você pode instalar a versão de serviço usando a linha de comando e especificando o `MRCACHEDIRECTORY` argumento conforme mostrado neste exemplo, que instala atualizações de atualização cumulativa 1 para:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obter os instaladores mais recentes, consulte [instalar componentes de aprendizado de máquina sem acesso à internet](install/sql-ml-component-install-without-internet-access.md).

**Aplica-se a:** SQL Server 2016 R Services, com o R Server versão 9.0.0 ou anterior

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. Os serviços do Launchpad não pode ser iniciado se a versão for diferente da versão do R

Se você instalar o SQL Server R Services separadamente do mecanismo de banco de dados e as versões de compilação forem diferentes, você poderá ver o seguinte erro no log de eventos do sistema:

> *O serviço Launchpad do SQL Server falhou ao iniciar devido ao seguinte erro: O serviço não respondeu à solicitação de início ou controle de forma oportuna.*

Por exemplo, esse erro pode ocorrer se você instalar o mecanismo de banco de dados usando a versão de lançamento, aplicar um patch para atualizar o mecanismo de banco de dados e, em seguida, adicione o recurso R Services usando a versão de lançamento.

Para evitar esse problema, use um utilitário como o Gerenciador de arquivo para comparar as versões do Launchpad.exe com versão dos binários do SQL, como sqldk.dll. Todos os componentes devem ter o mesmo número de versão. Se você atualizar um componente, lembre-se de aplicar a mesma atualização a todos os outros componentes instalados.

Procure a barra inicial no `Binn` pasta para a instância. Por exemplo, uma instalação padrão do SQL Server 2016, o caminho pode ser `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. Contextos de computação remota estão bloqueados por um firewall nas instâncias do SQL Server em execução em máquinas virtuais do Azure

Se você tiver instalado o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] em uma máquina virtual do Windows Azure, você talvez não consiga usar contextos de computação que exigem o uso do espaço de trabalho da máquina virtual. O motivo é que, por padrão, o firewall em máquinas virtuais do Azure inclui uma regra que bloqueia o acesso para contas de usuário locais do R de rede.

Como alternativa, na VM do Azure, abra **Firewall do Windows com segurança avançada**, selecione **regras de saída**e desabilitar a regra a seguir: **Bloquear o acesso de rede para contas de usuário local do R na instância MSSQLSERVER do SQL Server**. Você também pode deixar a regra habilitada, mas altere a propriedade de segurança para **permitir se seguro**.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. Autenticação implícita em SQLEXPRESS

Quando você executa trabalhos em R de uma estação de trabalho de ciência de dados remota usando a autenticação do Windows integrada, o SQL Server usa *autenticação implícita* para gerar as chamadas ODBC locais que podem ser exigidas pelo script. No entanto, esse recurso não funcionou no build RTM do SQL Server Express Edition.

Para corrigir o problema, recomendamos atualizar para uma versão de serviço posterior.

Se a atualização não for viável, como alternativa, use um logon do SQL para executar trabalhos R remotos que podem exigir chamadas ODBC incorporadas.

**Aplica-se a:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. Limites de desempenho quando as bibliotecas usadas pelo SQL Server são chamadas de outras ferramentas

É possível chamar as bibliotecas que são instaladas para o SQL Server de um aplicativo externo, como o RGui de aprendizado de máquina. Isso pode ser a maneira mais conveniente para realizar certas tarefas, como instalar novos pacotes, ou a execução de testes ad hoc em amostras de código muito curto. No entanto, fora do SQL Server, o desempenho pode ser limitado. 

Por exemplo, mesmo se você estiver usando o Enterprise Edition do SQL Server, R é executado no modo single-threaded, quando você executa seu código R usando ferramentas externas. Para obter os benefícios de desempenho no SQL Server, inicie uma conexão do SQL Server e usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para chamar o tempo de execução do script externo.

Em geral, evite chamar as bibliotecas que são usadas pelo SQL Server de ferramentas externas de aprendizado de máquina. Se você precisar depurar R ou o código do Python, é geralmente mais fácil de fazer isso fora do SQL Server. Para obter as mesmas bibliotecas que estão no SQL Server, você pode instalar o cliente do Microsoft R [Machine Learning Server (autônomo) do SQL Server 2017](install/sql-machine-learning-standalone-windows-install.md), ou [SQL Server 2016 R Server (autônomo)](install/sql-r-standalone-windows-install.md).

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools não oferece suporte a permissões exigidas para scripts externos

Ao usar o Visual Studio ou o SQL Server Data Tools para publicar um projeto de banco de dados, se qualquer entidade de segurança tem permissões específicas para a execução do script externo, você poderá receber um erro como este:

> *Modelo de TSQL: Erro detectado quando o banco de dados de engenharia reversa. A permissão não foi reconhecida e não foi importada.*

Atualmente, o modelo de DACPAC não oferece suporte para as permissões usadas pelo R Services ou serviços de aprendizado de máquina, como GRANT ANY EXTERNAL SCRIPT ou EXECUTE ANY EXTERNAL SCRIPT. Esse problema será corrigido em uma versão posterior.

Como alternativa, execute a concessão adicional instruções em um script de pós-implantação.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. Execução de script externo está limitada devido a valores de padrão de governança de recursos

No Enterprise Edition, você pode usar pools de recursos para gerenciar processos de script externo. Em alguns builds de lançamento inicial, a memória máxima que podia ser alocada para os processos do R era de 20 por cento. Portanto, se o servidor tinha 32 GB de RAM, os executáveis do R (RTerm.exe e BxlServer.exe) pode usar um máximo de 6,4 GB em uma única solicitação.

Se você encontrar limitações de recursos, verifique o padrão atual. Se 20 por cento não for suficiente, consulte a documentação para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sobre como alterar esse valor.

**Aplica-se a:** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>Problemas de execução do script de R

Esta seção contém problemas conhecidos que são específicos para executar o R no SQL Server, bem como alguns problemas que estão relacionados às bibliotecas de R e ferramentas publicadas pela Microsoft, incluindo o RevoScaleR.

Para mais problemas conhecidos que podem afetar a soluções de R, consulte o [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) site.

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. Acesso negado aviso durante a execução de scripts do R no SQL Server em um local não padrão

Se a instância do SQL Server foi instalada em um local não padrão, como fora de `Program Files` pasta, o aviso ACCESS_DENIED é gerado quando você tenta executar scripts que instalam um pacote. Por exemplo:

> *No `normalizePath(path.expand(path), winslash, mustWork)` : caminho [2] = "~ExternalLibraries/R/8/1": Acesso negado*

O motivo é que uma função do R tenta ler o caminho e falhará se o grupo de usuários internos **SQLRUserGroup**, não tem acesso de leitura. O aviso que é gerado não bloqueia a execução do script R atual, mas o aviso pode ocorrer repetidamente, sempre que o usuário executa qualquer outro script de R.

Se você tiver instalado o SQL Server para o local padrão, esse erro não ocorre, porque todos os usuários do Windows têm permissões de leitura no `Program Files` pasta.

Esse problema foi corrigido de ia em uma versão de serviço futura. Como alternativa, forneça o grupo **SQLRUserGroup**, com acesso de leitura para todas as pastas pai dos `ExternalLibraries`.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. Erro de serialização entre versões novas e antigas do RevoScaleR

Quando você passa um modelo usando um formato serializado para uma instância remota do SQL Server, você poderá receber o erro: 

> *Erro no memDecompress (dados, tipo = descompactar) erro interno -3 em memDecompress(2).*

Esse erro será gerado se você salvou o modelo usando uma versão recente do que a função de serialização [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), mas a instância do SQL Server em que você Desserialize o modelo tem uma versão mais antiga das APIs de RevoScaleR, do SQL Server 2017 CU2 ou anterior.

Como alternativa, você pode atualizar a instância do SQL Server 2017 CU3 ou posterior.

O erro não aparecer se a versão da API é o mesmo, ou se você estiver movendo um modelo salvo com uma função mais antiga de serialização para um servidor que usa uma versão mais recente da API de serialização.

Em outras palavras, use a mesma versão do RevoScaleR para operações de serialização e desserialização.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>3. Pontuação em tempo real não lida corretamente com o _learningRate_ parâmetro nos modelos de árvore e de floresta

Se você cria um modelo usando uma árvore de decisão ou um método de floresta de decisão e especificar a taxa de aprendizado, você poderá ver resultados inconsistentes, ao usar `sp_rxpredict` ou o SQL `PREDICT` função, em comparação com o `rxPredict`.

A causa é um erro na API que modela processos serializados e é limitada à `learningRate` parâmetro: por exemplo, na [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees), ou

Esse problema é corrigido em uma versão de serviço futura.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. Limitações na afinidade do processador para trabalhos do R

Na compilação de versão inicial do SQL Server 2016, você pode definir a afinidade de processador somente para CPUs no primeiro grupo k. Por exemplo, se o servidor for uma máquina de 2 soquetes com dois grupos k, apenas os processadores do primeiro grupo k são usados para os processos do R. A mesma limitação se aplica quando você configura a governança de recursos para trabalhos de script do R.

Esse problema é corrigido no SQL Server 2016 Service Pack 1. É recomendável que você atualize para a versão mais recente do serviço.

**Aplica-se a:** Versão RTM do SQL Server 2016 R Services

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5. Não é possível fazer alterações nos tipos de coluna durante a leitura de dados em um contexto de computação do SQL Server

Se o contexto de computação estiver definido como a instância do SQL Server, não será possível usar o argumento _colClasses_ (ou outros argumentos semelhante) para alterar o tipo de dados das colunas no código R.

Por exemplo, a seguinte instrução resultará em um erro se a coluna CRSDepTimeStr ainda não for um inteiro:

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

Como alternativa, você pode reescrever a consulta SQL para usar CAST ou CONVERT e apresentar os dados em R usando o tipo de dados correto. Em geral, desempenho é melhor quando você trabalha com dados usando SQL em vez de por meio da alteração de dados no código R.

**Aplica-se a:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. Limites de tamanho de modelos serializados

Quando você salva um modelo para uma tabela do SQL Server, você deve serializar o modelo e salvá-lo em um formato binário. Teoricamente, o tamanho máximo de um modelo que pode ser armazenado com esse método é 2 GB, que é o tamanho máximo de colunas varbinary no SQL Server.

Se você precisar usar modelos maiores, soluções alternativas a seguir estão disponíveis:

+ Tome medidas para reduzir o tamanho do seu modelo. Alguns pacotes de R de software livre incluem uma grande quantidade de informações no objeto de modelo, e grande parte dessas informações pode ser removido para implantação. 
+ Use seleção de recursos para remover colunas desnecessárias.
+ Se você estiver usando um algoritmo de código-fonte aberto, considere uma implementação semelhante usando o algoritmo correspondente em MicrosoftML ou RevoScaleR. Esses pacotes foram otimizados para cenários de implantação.
+ Depois que o modelo foi racionalizado e o tamanho reduzido usando as etapas anteriores, veja se o [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) função em R de base pode ser usada para reduzir o tamanho do modelo antes de passá-lo para o SQL Server. Essa opção é recomendada quando o modelo está próximo do limite de 2 GB.
+ Para modelos maiores, você pode usar o SQL Server [FileTable](../relational-databases/blob/filetables-sql-server.md) para armazenar os modelos de recursos, em vez de usar uma coluna varbinary.

    Para usar FileTables, você deve adicionar uma exceção de firewall, porque os dados armazenados em FileTables são gerenciados pelo driver de sistema de arquivos Filestream no SQL Server, e as regras de firewall padrão bloqueiam o acesso de arquivo de rede. Para obter mais informações, consulte [habilitar pré-requisitos para FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md).

    Depois que você tiver habilitado a FileTable gravar o modelo, que obter um caminho do SQL usando a API de FileTable e, em seguida, gravar o modelo para o local do seu código. Quando você precisar ler o modelo, você pode obter o caminho do SQL e, em seguida, chama o modelo usando o caminho do seu script. Para obter mais informações, consulte [acessar FileTables com APIs de arquivo de entrada e saída](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7. Evitar a limpeza de espaços de trabalho quando você executar o código R em um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contexto de computação

Se você usar um comando de R para limpar seu espaço de trabalho de objetos durante a execução de código R em um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contexto de computação ou se você limpar o espaço de trabalho como parte de um script de R chamado usando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), você poderá receber este erro : *revoScriptConnection de objeto do espaço de trabalho não encontrado*

O`revoScriptConnection` é um objeto no workspace do R que contém informações sobre uma sessão do R chamada por meio de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, se o código R incluir um comando para limpar o workspace (como `rm(list=ls()))`), todas as informações sobre a sessão e outros objetos no workspace do R também serão limpos.

Como alternativa, evite a limpeza indiscriminada de variáveis e outros objetos durante a execução do R [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Embora a limpar o espaço de trabalho é comum ao trabalhar no console do R, ele pode ter consequências não intencionais.

* Para excluir variáveis específicas, use o R `remove` função: por exemplo, `remove('name1', 'name2', ...)`
* Se houver várias variáveis a serem excluídas, salve os nomes das variáveis temporárias em uma lista e execute a coleta de lixo periódica.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. Restrições sobre dados que podem ser fornecidos como entrada para um script R

O sistema não permite usar os seguintes tipos de resultados de consulta em um script R:

- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência às colunas AlwaysEncrypted.
  
- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência à colunas mascaradas.
  
     Se precisar usar dados mascarados em um script R, uma solução alternativa é copiar os dados em uma tabela temporária e usar esses dados.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. Uso de cadeias de caracteres como fatores podem levar à degradação do desempenho

Usando variáveis de tipo de cadeia de caracteres como fatores podem aumentar significativamente a quantidade de memória usada para operações de R. Esse é um problema conhecido com o R em geral, e há muitos artigos sobre o assunto. Por exemplo, consulte [fatores não são cidadãos de primeira classe em R, por John montagem, no R bloggers)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) ou [stringsAsFactors: Uma biografia não autorizada, por Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Embora o problema não é específico para o SQL Server, ele pode afetar significativamente o desempenho do código R executado no SQl Server. Cadeias de caracteres normalmente são armazenadas como varchar ou nvarchar e, se uma coluna de dados de cadeia de caracteres tem muitos valores exclusivos, o processo de conversão internamente esses inteiros e voltar para cadeias de caracteres por R ainda pode levar a erros de alocação de memória.

Se você não exige absolutamente que um tipo de dados de cadeia de caracteres para outras operações, os valores de cadeia de caracteres de mapeamento para um numérico (integer) tipo de dados como parte da preparação de dados seria benéfico, de uma perspectiva de desempenho e escala.

Para uma discussão sobre esse problema e outras dicas, consulte [desempenho para serviços R – otimização de dados](r/r-and-data-optimization-r-services.md).

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. Argumentos *varsToKeep* e *varsToDrop* não há suporte para fontes de dados do SQL Server

Quando você usa a função rxDataStep para gravar os resultados em uma tabela, usando o *varsToKeep* e *varsToDrop* é uma maneira prática de especificar as colunas a serem incluídos ou excluídos como parte da operação. No entanto, esses argumentos não têm suporte para fontes de dados do SQL Server.

### <a name="11-limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>11. Suporte limitado para tipos de dados SQL no sp\_execute\_externo\_script

Nem todos os tipos de dados que têm suporte no SQL podem ser usados em R. Como alternativa, considere a conversão de tipo de dados sem suporte para um tipo de dados com suporte antes de passar os dados para sp\_execute\_externo\_script.

Para obter mais informações, consulte [tipos de dados e bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Corrupção de cadeia de caracteres possíveis usando cadeias de caracteres unicode em colunas varchar

Passando dados unicode nas colunas varchar de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para R/Python pode resultar na corrupção de cadeia de caracteres. Isso se deve a codificação dessas cadeia de caracteres unicode em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] agrupamentos podem não corresponder com a codificação de UTF-8 padrão usados em R/Python. 

Para enviar dados de cadeia de caracteres não ASCII [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para R/Python, use a codificação UTF-8 (disponível em [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) ou usar o tipo nvarchar para o mesmo.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>13. Apenas um valor do tipo `raw` pode ser retornado de `sp_execute_external_script`

Quando um tipo de dados binários (R **brutos** tipo de dados) é retornado de R, o valor deve ser enviado no quadro de dados de saída.

Com dados de tipos diferentes de **brutos**, é possível retornar valores de parâmetro junto com os resultados do procedimento armazenado, adicionando a palavra-chave OUTPUT. Para obter mais informações, consulte [parâmetros](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Se você quiser usar vários conjuntos de saída que incluem valores do tipo **bruto**, uma possível solução alternativa é fazer várias chamadas de procedimento armazenado ou para enviar o resultado voltar define como [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando ODBC.

### <a name="14-loss-of-precision"></a>14. Perda de precisão

Porque [!INCLUDE[tsql](../includes/tsql-md.md)] e R dão suporte a vários tipos de dados, tipos de dados numéricos podem sofrer perda de precisão durante a conversão.

Para obter mais informações sobre a conversão implícita de tipo de dados, consulte [tipos de dados e bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. Variável de erro de escopo quando você usa o parâmetro transformFunc

Para transformar os dados enquanto você estiver modelando, você pode passar uma *transformFunc* argumento em uma função, como `rxLinmod` ou `rxLogit`. No entanto, chamadas de função aninhada podem causar erros de escopo no contexto de computação do SQL Server, mesmo se as chamadas funcionem corretamente no contexto de computação local.

> *O conjunto de dados de exemplo para a análise não tem variáveis*

Por exemplo, suponha que você definiu duas funções, `f` e `g`, em seu ambiente global local, e `g` chamadas `f`. Nas chamadas distribuídas ou remotas envolva `g`, a chamada para `g` pode falhar com este erro, porque `f` não for encontrado, mesmo se você passar `f` e `g` para a chamada remota.

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

Quando **varchar** colunas são lidos de um banco de dados, espaço em branco é cortado. Para evitar isso, coloque as cadeias de caracteres entre caracteres de espaço não em branco.

Quando as funções, como `rxDataStep` são usados para criar tabelas de banco de dados que tenham **varchar** colunas, a largura da coluna é calculada com base em uma amostra dos dados. Se a largura pode variar, pode ser necessário preencher todas as cadeias de caracteres com um comprimento comum.

O uso de uma transformação para alterar o tipo de dados de uma variável não terá suporte quando chamadas repetidas para `rxImport` ou `rxTextToXdf` sejam usadas para importar e anexar linhas, combinando vários arquivos de entrada em um único arquivo .xdf.

### <a name="17-limited-support-for-rxexec"></a>17. Suporte limitado para rxExec

No SQL Server 2016, o `rxExec` função que é fornecido pelo RevoScaleR pacote pode ser usado apenas no modo single-threaded.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. Aumentar o tamanho máximo do parâmetro para dar suporte a rxGetVarInfo

Se você usar conjuntos de dados com um número muito grande de variáveis (por exemplo, mais de 40.000), defina as `max-ppsize` sinalizar quando iniciar R para usar funções como `rxGetVarInfo`. O sinalizador `max-ppsize` especifica o tamanho máximo da pilha de proteção do ponteiro.

Se você estiver usando o console do R (por exemplo, RGui.exe ou RTerm.exe), você pode definir o valor de _max max-ppsize_ em 500000 digitando:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. Problemas com a função rxDTree

Atualmente, a função `rxDTree` não tem suporte para transformações dentro da fórmula. Não temos suporte para o uso da sintaxe `F()` , em especial, para a criação de fatores dinâmicos. No entanto, os dados numéricos são automaticamente guardados.

Os fatores ordenados são tratados da mesma forma que os fatores de todas as funções de análise RevoScaleR, exceto o `rxDTree`.

## <a name="python-script-execution-issues"></a>Problemas de execução de script do Python

Esta seção contém problemas conhecidos que são específicos para execução de Python no SQL Server, bem como problemas relacionados aos pacotes Python publicados pela Microsoft, incluindo [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. Chamada para o modelo pré-treinado falhará se o caminho para o modelo é muito longo

Se você instalou os modelos pré-treinados em uma versão inicial do SQL Server 2017, o caminho completo para o arquivo de modelo treinado pode ser muito longo para o Python ler. Essa limitação foi corrigida em uma versão posterior do serviço.

Há várias possíveis soluções alternativas: 

+ Quando você instala os modelos pré-treinados, escolha um local personalizado.
+ Se possível, instale a instância do SQL Server em um caminho de instalação personalizada com um caminho mais curto, como C:\SQL\MSSQL14. MSSQLSERVER.
+ Use o utilitário do Windows [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) para criar um link físico que mapeia o arquivo de modelo para um caminho mais curto.
+ Atualize para a versão mais recente do serviço.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. Erro ao salvar serializou o modelo para o SQL Server

Quando você passar um modelo para uma instância remota do SQL Server e tente ler o modelo binário usando o `rx_unserialize` funcionar [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), você poderá receber o erro: 

> *NameError: o nome 'rx_unserialize_model' não está definido*

Esse erro é gerado se você salvou o modelo usando uma versão recente do que a função de serialização, mas a instância do SQL Server em que você Desserialize o modelo não reconhece a API de serialização.

Para resolver o problema, atualize a instância do SQL Server 2017 CU3 ou posterior.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. Falha ao inicializar uma variável varbinary causa um erro no BxlServer

Se você executar o código do Python no SQL Server usando `sp_execute_external_script`e o código de saída variáveis do tipo varbinary (max), varchar (max) ou tipos semelhantes, a variável deve ser inicializada ou definida como parte de seu script. Caso contrário, o componente de troca de dados, o BxlServer, gerará um erro e parar de funcionar.

Essa limitação será corrigida em uma versão de serviço futura. Como alternativa, certifique-se de que a variável é inicializada dentro do script de Python. Qualquer valor válido pode ser usado, como nos exemplos a seguir:

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

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. Aviso de telemetria em uma execução bem-sucedida de código do Python

Começando com o SQL Server 2017 CU2, a seguinte mensagem pode aparecer mesmo se outro tipo de código do Python é executado com êxito:

> *Mensagem (NS) STDERR do script externo:*
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state é usado antes da declaração global*


Esse problema foi corrigido no SQL Server 2017 atualização cumulativa 3 (CU3). 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open

Esta seção lista problemas específicos à conectividade de R, desenvolvimento e ferramentas de desempenho que são fornecidas pela Revolution Analytics. Essas ferramentas foram fornecidas em versões anteriores de pré-lançamento do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

Em geral, é recomendável que você desinstale dessas versões anteriores e instala a versão mais recente do SQL Server ou Microsoft R Server.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. Não há suporte para o Revolution R Enterprise

Instalar o Revolution R Enterprise lado a lado com qualquer versão do [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] não tem suporte.

Se você tiver uma licença existente para Revolution R Enterprise, você deve colocá-lo em um computador separado de ambas as [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instância e em qualquer estação de trabalho que você deseja usar para se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instância.

Algumas versões de pré-lançamento do [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluído um ambiente de desenvolvimento do R para Windows que foi criado pela Revolution Analytics. Essa ferramenta não é mais fornecida e não tem suporte.

Para compatibilidade com [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], recomendamos que você instale o Microsoft R Client. [Ferramentas do R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) e [Visual Studio Code](https://code.visualstudio.com/) também dá suporte a soluções de R da Microsoft.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. Problemas de compatibilidade com o driver ODBC do SQLite e o RevoScaleR

Revisão 0.92 do driver ODBC do SQLite é incompatível com o RevoScaleR. Revisões de 0.88 a 0.91 e 0,93 e posteriores são compatíveis.

## <a name="see-also"></a>Confira também

[Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Solução de problemas de aprendizado de máquina no SQL Server](machine-learning-troubleshooting-faq.md)
