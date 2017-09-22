---
title: "Problemas conhecidos de serviços de aprendizado de máquina | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
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
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 2d21756a05e9e51379faa194ec331517e510988d
ms.contentlocale: pt-br
ms.lasthandoff: 09/21/2017

---
# <a name="known-issues-in-machine-learning-services"></a>Problemas conhecidos nos serviços de aprendizado de máquina

Este artigo descreve problemas conhecidos ou limitações com componentes que são fornecidos como uma opção no SQL Server 2016 e no SQL Server 2017 de aprendizado de máquina.

As informações aqui se aplica a todos os itens a seguir, a menos que especificamente indicado:

* SQL Server 2016

  - R Services (no banco de dados)
  - Microsoft R Server (Autônomo)

* SQL Server 2017

  - Serviços de R (no banco de dados) de aprendizado de máquina
  - Serviços para Python (no banco de dados) de aprendizado de máquina
  - Servidor do Machine Learning (Autônomo)

## <a name="setup-and-configuration-issues"></a>Problemas de instalação e configuração

Para obter uma descrição dos processos e perguntas comuns relacionadas à configuração inicial e a configuração, consulte [perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md). Ele contém informações sobre atualizações, a instalação lado a lado e a instalação de novos componentes de R ou Python.

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>Não é possível instalar componentes do Python em offline instalações do SQL Server de 2017 CTP 2.0 ou posterior

Se você instalar uma versão de pré-lançamento do SQL Server 2017 em um computador sem acesso à internet, o instalador pode falhar exibir a página que solicita a localização dos componentes do Python baixados. Nesse caso, você pode instalar o recurso Serviços de aprendizado de máquina, mas não os componentes do Python.

Esse problema é corrigido na versão de lançamento. Se você encontrar esse problema, como alternativa, você pode habilitar temporariamente o acesso à internet durante a instalação. Essa limitação não se aplica a R.

**Aplica-se a:** SQL Server 2017 com Python

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Instalar a versão mais recente do serviço para garantir a compatibilidade com o cliente do Microsoft R

Se você instala a versão mais recente do cliente do Microsoft R e usá-lo para executar R no SQL Server em um contexto de computação remota, você poderá receber um erro semelhante ao seguinte:

>*Você está executando a versão 9.x.x do cliente do Microsoft R no seu computador, que é incompatível com o Microsoft R Server versão 8.x.x. Baixe e instale uma versão compatível.*

SQL Server 2016 requer que as bibliotecas de R no cliente correspondem exatamente as bibliotecas de R no servidor. A restrição foi removida para versões mais tarde do que R Server 9.0.1. No entanto, se você encontrar esse erro, verifique se a versão das bibliotecas de R que é usada pelo seu cliente e o servidor e, se necessário, atualize o cliente para corresponder à versão do servidor.

A versão do R que é instalado com o SQL Server R Services é atualizada sempre que uma versão de serviço do SQL Server está instalada. Para garantir que você sempre tenha as versões mais recentes dos componentes de R, certifique-se de instalar todos os service packs.

Para garantir a compatibilidade com o cliente do Microsoft R 9.0.0, instalar as atualizações que estão descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262).

Para evitar problemas com pacotes de R, você também pode atualizar a versão das bibliotecas de R que estão instalados no servidor, alterando para a política de ciclo de vida modernos descrito na [a próxima seção](#bkmk_sqlbindr). Quando você fizer isso, a versão do R que é instalado com o SQL Server é atualizada na mesma agenda que as atualizações são publicadas para o Microsoft R Server, que garante que o servidor e cliente sempre tenham as versões mais recentes do Microsoft R.

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="bkmk_sqlbindr"></a>Quando você conecta a uma versão mais antiga do SQL Server R Services de um cliente por meio de aviso de versão incompatível[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Quando você executar o código R em um contexto de computação do SQL Server 2016, e uma das duas instruções a seguir for verdadeira, você verá um erro semelhante à seguinte:
* Você instalou o R Server (autônomo) em um computador cliente usando o Assistente para instalação [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
* Você instalou o Microsoft R Server usando o [separadas do Windows installer](https://docs.microsoft.com/r-server/install/r-server-install-windows).

>*Você está executando a versão 9.0.0 do Cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

Você pode usar _associação_ no Microsoft R Server 9.0 e versões posteriores, para atualizar os componentes de R em instâncias do SQL Server 2016. Para determinar se há suporte para atualizações disponíveis para sua versão dos serviços do R, consulte [atualizar uma instância dos serviços do R usando SqlBindR.exe](/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>A instalação de versões de serviço do SQL Server 2016 poderá falhar ao instalar versões mais novas dos componentes do R

Quando você instala uma atualização cumulativa ou instala um service pack para SQL Server 2016 em um computador que não está conectado à internet, o Assistente de instalação pode falhar ao exibir o prompt que permite que você atualize os componentes de R usando arquivos CAB baixados. Esta falha ocorre normalmente quando vários componentes foram instalados junto com o mecanismo de banco de dados.

Como alternativa, você pode instalar a versão de serviço usando a linha de comando e especificando o */MRCACHEDIRECTORY* argumento conforme mostrado neste exemplo, que instala atualizações CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obter os instaladores mais recentes, consulte [instalar componentes de aprendizado de máquina sem acesso à internet](r/installing-ml-components-without-internet-access.md).

**Aplica-se a:** SQL Server 2016 R Services, com R Server versão 9.0.0 ou anterior

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>Serviços de barra inicial não será iniciado se a versão for diferente da versão do R

Se você instalar o SQL Server R Services separadamente do mecanismo de banco de dados e as versões de compilação forem diferentes, você verá o seguinte erro no log de eventos do sistema:

>_O serviço do Launchpad do SQL Server não pôde ser iniciado devido ao seguinte erro: O serviço não respondeu à solicitação de início ou controle de maneira oportuna._

Por exemplo, esse erro pode ocorrer se você instalar o mecanismo de banco de dados usando a versão de lançamento, aplicar um patch para atualizar o mecanismo de banco de dados e, em seguida, adicione o recurso Serviços de R usando a versão de lançamento.

Para evitar esse problema, verifique se todos os componentes têm o mesmo número de versão. Se você atualizar um componente, lembre-se de aplicar a mesma atualização a todos os outros componentes instalados.

Para exibir uma lista dos números de versão de R que são necessários para cada versão do SQL Server 2016, consulte [componentes instalar R sem acesso à internet](r/installing-ml-components-without-internet-access.md).

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>Contextos de computação remota estão bloqueados por um firewall em instâncias do SQL Server em execução em máquinas virtuais do Azure

Se você tiver instalado [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] em uma máquina virtual do Windows Azure, você não poderá usar os contextos de computação que exigem o uso de espaço de trabalho da máquina virtual. O motivo é que, por padrão, o firewall em máquinas virtuais do Azure inclui uma regra que bloqueia o acesso para contas de usuário locais do R de rede.

Como alternativa, na VM do Azure, abra **Firewall do Windows com segurança avançada**, selecione **as regras de saída**e desabilitar a regra a seguir: **bloquear o acesso de rede para contas de usuário local do R no A instância do SQL Server MSSQLSERVER**. Você também pode deixar a regra habilitada, mas altere a propriedade de segurança para **permitir se seguro**.

### <a name="implied-authentication-in-sqlexpress"></a>Autenticação implícita em SQLEXPRESS

Quando você executar trabalhos de R de uma estação de trabalho de ciência de dados remota usando a autenticação integrada do Windows, o SQL Server usa *autenticação implícita* para gerar qualquer local chamada ODBC que pode ser necessárias pelo script. No entanto, esse recurso não funcionou no build RTM do SQL Server Express Edition.

Para corrigir o problema, recomendamos atualizar para uma versão de serviço posterior.

Se não for possível atualizá-la, use um logon SQL para executar trabalhos remotos do R que podem exigir chamadas ODBC incorporadas.

**Aplica-se a:** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-r-libraries-are-called-from-other-r-tools"></a>Limites de desempenho quando bibliotecas de R são chamadas de outras ferramentas de R

É possível chamar as ferramentas de R e bibliotecas que são instaladas para o SQL Server de um aplicativo externo de R como RGui. Essa chamada pode ser útil quando você instala novos pacotes, ou quando você executa testes ad hoc em exemplos de código muito curto.

No entanto, lembre-se de que fora do SQL Server, o desempenho pode ser limitado. Por exemplo, mesmo se você tiver comprado o Enterprise Edition do SQL Server, R é executado no modo de thread único, quando você executa o código de R usando ferramentas externas. Desempenho deve ser melhor se você executar seu código R iniciando uma conexão do SQL Server e usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), que chama as bibliotecas de R para você.

* Evite chamar as bibliotecas de R usados pelo SQL Server a partir de ferramentas externas de R.
* Se você precisar executar código R extensivo no computador do SQL Server sem usar o SQL Server, instale uma instância separada do R, como o cliente do Microsoft R e, em seguida, verifique se as ferramentas de desenvolvimento R apontam para a nova biblioteca.

Para obter mais informações, consulte [Criar um R Server autônomo](r/create-a-standalone-r-server.md).

### <a name="the-r-script-is-throttled-due-to-resource-governance-default-values"></a>O script R é limitado devido a valores de padrão de controle de recursos

No Enterprise Edition, você pode usar pools de recursos para gerenciar processos de script externo. Em alguns compilações de versão anteriores, a memória máxima que pode ser alocada para os processos de R foi 20 por cento. Portanto, se o servidor tiver 32 GB de RAM, os executáveis de R (RTerm.exe e BxlServer.exe) podem usar um máximo de 6,4 GB em uma única solicitação.

Se você encontrar as limitações de recursos, verifique o padrão atual. Se 20% não seja suficiente, consulte a documentação para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sobre como alterar esse valor.

**Aplica-se a:** R Services do SQL Server 2016, Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>A execução de código R e problemas de pacote ou de função

Esta seção contém os problemas conhecidos que são específicos à execução de R no SQL Server, bem como alguns problemas relacionados a bibliotecas de R e ferramentas publicadas pela Microsoft, incluindo o RevoScaleR.

Para mais problemas conhecidos que podem afetar a soluções de R, vá para o [site Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-known-issues).

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Limitações na afinidade do processador para trabalhos do R

Na compilação de versão inicial do SQL Server 2016, você pode definir a afinidade do processador somente para CPUs no primeiro grupo de k. Por exemplo, se o servidor for uma máquina de 2 soquetes com dois grupos de k, processadores somente do primeiro grupo k são usados para os processos de R. As mesmas limitações se aplicam quando você configura o controle de recursos para trabalhos de script R.

Esse problema é corrigido no SQL Server 2016 Service Pack 1. É recomendável que você atualize para a versão mais recente do serviço.

**Aplica-se a:** versão RTM do SQL Server 2016 R Services

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>Não é possível fazer alterações nos tipos de coluna durante a leitura de dados em um contexto de computação do SQL Server

Se o contexto de computação estiver definido como a instância do SQL Server, não será possível usar o argumento _colClasses_ (ou outros argumentos semelhante) para alterar o tipo de dados das colunas no código R.

Por exemplo, a seguinte instrução resultará em um erro se a coluna CRSDepTimeStr ainda não for um inteiro:

```r
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
```

Como alternativa, você pode reescrever a consulta SQL para usar CAST ou converter e apresentar os dados em R usando o tipo de dados correto. Em geral, desempenho é melhor quando você trabalha com dados usando SQL em vez de alteração de dados no código de R.

**Aplica-se a:** SQL Server 2016 R Services

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>Evitar limpar espaços de trabalho quando você executar o código R em um [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contexto de computação

Se você usar o comando de R para limpar seu espaço de trabalho de objetos durante a execução de código R em uma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] computação contexto, ou se você limpar o espaço de trabalho como parte de um script de R chamado usando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), você pode obter isso Erro: 

>*objeto de espaço de trabalho 'revoScriptConnection' não encontrado*

O`revoScriptConnection` é um objeto no espaço de trabalho do R que contém informações sobre uma sessão do R chamada por meio de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, se o código R incluir um comando para limpar o espaço de trabalho (como `rm(list=ls()))`), todas as informações sobre a sessão e outros objetos no espaço de trabalho do R também serão limpos.

Como alternativa, evite limpando indiscriminado de variáveis e outros objetos enquanto você estiver executando o R no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Embora limpar o espaço de trabalho é comum quando trabalha no console de R, ele pode ter consequências não intencionais.

* Para excluir variáveis específicas, use o R *remover* função: `remove('name1', 'name2', ...)`.
* Se houver várias variáveis a serem excluídas, salve os nomes das variáveis temporárias em uma lista e execute a coleta de lixo periódica.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Restrições sobre dados que podem ser fornecidos como entrada para um script R

O sistema não permite usar os seguintes tipos de resultados de consulta em um script R:

- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência às colunas AlwaysEncrypted.
  
- Dados de uma consulta [!INCLUDE[tsql](../includes/tsql-md.md)] que faz referência à colunas mascaradas.
  
     Se precisar usar dados mascarados em um script R, uma solução alternativa é copiar os dados em uma tabela temporária e usar esses dados.

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

Dados de tipos diferentes de **bruto**, você pode retornar valores de parâmetro junto com os resultados do procedimento armazenado simplesmente adicionando a palavra-chave OUTPUT. Para obter mais informações, consulte [retornar dados usando parâmetros de saída](https://technet.microsoft.com/library/ms187004.aspx).

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

Se estiver usando o console de R, por exemplo, em rgui.exe ou em rterm.exe, você pode definir o valor máximo de max-ppsize em 500000 digitando:

```r
R --max-ppsize=500000
```

Se você estiver usando o [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] ambiente, você pode definir o `max-ppsize` sinalizador fazendo a chamada a seguir para o executável RevoIDE:

```
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```

### <a name="issues-with-the-rxdtree-function"></a>Problemas com a função rxDTree

Atualmente, a função `rxDTree` não tem suporte para transformações dentro da fórmula. Não temos suporte para o uso da sintaxe `F()` , em especial, para a criação de fatores dinâmicos. No entanto, os dados numéricos são automaticamente guardados.

Os fatores ordenados são tratados da mesma forma que os fatores de todas as funções de análise RevoScaleR, exceto o `rxDTree`.

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise e Microsoft R Open

Esta seção lista os problemas específicos para conectividade de R, desenvolvimento e ferramentas de desempenho que são fornecidas pela Revolution Analytics. Essas ferramentas foram fornecidas nas versões de pré-lançamento anteriores do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

Em geral, é recomendável que você desinstale essas versões anteriores e instala a versão mais recente do SQL Server ou Microsoft R Server.

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Execução lado a lado versões do Revolution R Enterprise

Instalar o Revolution R Enterprise lado a lado com qualquer versão do [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] não tem suporte.

Se tiver uma licença para usar uma versão diferente do Revolution R Enterprise, coloque-a em um computador separado, na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e na estação de trabalho que pretende usar para se conectar à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

### <a name="the-use-of-an-r-productivity-environment-is-not-supported"></a>Não há suporte para o uso de um ambiente de produtividade de R

Algumas versões de pré-lançamento do [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluído um ambiente de desenvolvimento R para Windows criado pela Revolution Analytics. Essa ferramenta não é mais fornecida e não há suporte.

Para compatibilidade com [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], é altamente recomendável que você instale o cliente do Microsoft R ou o Microsoft R Server em vez de ferramentas da Revolution Analytics. [Ferramentas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) e [código do Visual Studio](https://code.visualstudio.com/) também dá suporte a soluções de R da Microsoft.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Problemas de compatibilidade com o driver ODBC do SQLite e o RevoScaleR

Revisão 0.92 do driver ODBC do SQLite é incompatível com o RevoScaleR. Revisões de 0.88 a 0.91 e 0.93 e posteriores são compatíveis.

## <a name="python-code-execution-or-python-package-issues"></a>A execução de código Python ou problemas de pacotes do Python

Esta seção contém os problemas conhecidos que são específicos para em execução Python no SQL Server, bem como problemas relacionados aos pacotes Python publicados pela Microsoft, incluindo [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).


## <a name="see-also"></a>Consulte também

[Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Solucionando problemas de aprendizado de máquina no SQL Server](machine-learning-troubleshooting-faq.md)

