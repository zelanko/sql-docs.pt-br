---
title: Solucionar problemas de coleta de dados para Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3dbca20d974570d04d65fba30110049efad4e90d
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470441"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Solucionar problemas de coleta de dados para Machine Learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve os métodos de coleta de dados que você deve usar ao tentar resolver problemas por conta própria ou com a ajuda do atendimento ao cliente da Microsoft.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 Serviços de Machine Learning (R e Python)

## <a name="sql-server-version-and-edition"></a>Versão e edição do SQL Server

SQL Server o 2016 R Services é a primeira versão do SQL Server para incluir suporte de R integrado. O SQL Server 2016 Service Pack 1 (SP1) inclui várias melhorias importantes, incluindo a capacidade de executar scripts externos. Se você for um cliente SQL Server 2016, deverá considerar a instalação do SP1 ou posterior.

SQL Server 2017 adicionada integração de linguagem Python. Você não pode obter a integração de recursos do Python em versões anteriores.

Para obter assistência para obter a edição e as versões, consulte este artigo, que lista os números de compilação para cada uma das [versões de SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

Dependendo da edição do SQL Server que você está usando, algumas funcionalidades de aprendizado de máquina podem estar indisponíveis ou limitadas. Os artigos a seguir listam os recursos de aprendizado de máquina nas edições Enterprise, Developer, Standard e Express.

* [Edições e recursos com suporte do SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [Recursos de R e Python por edições do SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>Versões da linguagem e da ferramenta R

Em geral, a versão do Microsoft R instalada quando você seleciona o recurso R Services ou o recurso Serviços de Machine Learning é determinado pelo número de Build do SQL Server. Se você atualizar o ou o patch SQL Server, também deverá atualizar os componentes do R ou corrigi-los.

Para obter uma lista de versões e links para downloads de componentes do R, consulte [instalar componentes do Machine Learning sem acesso à Internet](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access). Em computadores com acesso à Internet, a versão necessária do R é identificada e instalada automaticamente.

É possível atualizar os componentes do R Server separadamente do mecanismo de banco de dados SQL Server, em um processo conhecido como associação. Portanto, a versão do R que você usa ao executar o código R no SQL Server pode ser diferente dependendo da versão instalada do SQL Server e se você migrou o servidor para a versão mais recente do R.

### <a name="determine-the-r-version"></a>Determinar a versão do R

A maneira mais fácil de determinar a versão do R é obter as propriedades de tempo de execução executando uma instrução como a seguinte:

```sql
exec sp_execute_external_script
       @language = N'R'
       , @script = N'
# Transform R version properties to data.frame
OutputDataSet <- data.frame(
  property_name = c("R.version", "Revo.version"),
  property_value = c(R.Version()$version.string, Revo.version$version.string),
  stringsAsFactors = FALSE)
# Retrieve properties like R.home, libPath & default packages
OutputDataSet <- rbind(OutputDataSet, data.frame(
  property_name = c("R.home", "libPaths", "defaultPackages"),
  property_value = c(R.home(), .libPaths(), paste(getOption("defaultPackages"), collapse=", ")),
  stringsAsFactors = FALSE)
)
'
WITH RESULT SETS ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));

```

> [!TIP]
> Se o R Services não estiver funcionando, tente executar apenas a parte do script R de RGui.

Como último recurso, você pode abrir arquivos no servidor para determinar a versão instalada. Para fazer isso, localize o arquivo rlauncher. config para obter o local do tempo de execução do R e o diretório de trabalho atual. Recomendamos que você faça e abra uma cópia do arquivo para que você não altere acidentalmente nenhuma propriedade.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Para obter a versão do R e as versões do RevoScaleR, abra um prompt de comando do R ou abra o RGui associado à instância.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

O console do R exibe as informações de versão na inicialização. Por exemplo, a versão a seguir representa a configuração padrão para SQL Server 2017:

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Versões do Python

Há várias maneiras de obter a versão do Python. A maneira mais fácil é executar essa instrução de Management Studio ou qualquer outra ferramenta de consulta SQL:

```sql
-- Get Python runtime properties:
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import sys
import pkg_resources
OutputDataSet = pandas.DataFrame(
                    {"property_name": ["Python.home", "Python.version", "Revo.version", "libpaths"],
                    "property_value": [sys.executable[:-10], sys.version, pkg_resources.get_distribution("revoscalepy").version, str(sys.path)]}
)
'
with WITH RESULT SETS (SQL keywords) ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));
```

Se Serviços de Machine Learning não estiver em execução, você poderá determinar a versão instalada do Python examinando o arquivo pythonlauncher. config. Recomendamos que você faça e abra uma cópia do arquivo para que você não altere acidentalmente nenhuma propriedade.

1. Somente para o SQL Server 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. Obtenha o valor de **PYTHONHOME**.
3. Obter o valor do diretório de trabalho atual.

> [!NOTE]
> Se você tiver instalado o Python e o R no SQL Server 2017, o diretório de trabalho e o pool de contas de trabalho serão compartilhados para as linguagens de R e Python.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>Várias instâncias do R ou Python estão instaladas?

Verifique se mais de uma cópia das bibliotecas de R está instalada no computador. Essa duplicação pode ocorrer se:

* Durante a instalação, você seleciona o R Services (no banco de dados) e o servidor R (autônomo).
* Você instala Microsoft R Client além de SQL Server.
* Um conjunto diferente de bibliotecas de R foi instalado usando Ferramentas do R para Visual Studio, R Studio, Microsoft R Client ou outro IDE do R.
* O computador hospeda várias instâncias do SQL Server e mais de uma instância usa o aprendizado de máquina.

As mesmas condições se aplicam ao Python.

Se você descobrir que várias bibliotecas ou tempos de execução estão instalados, certifique-se de obter apenas os erros associados aos tempos de execução do Python ou do R que são usados pela instância de SQL Server.

## <a name="origin-of-errors"></a>Origem de erros

Os erros que você vê quando tenta executar o código R podem vir de qualquer uma das seguintes fontes:

* SQL Server mecanismo de banco de dados, incluindo o procedimento armazenado sp_execute_external_script
* O Launchpad confiável SQL Server
* Outros componentes da estrutura de extensibilidade, incluindo os iniciadores R e Python e os processos de satélite
* Provedores, como o Microsoft Open Database Connectivity (ODBC)
* Linguagem R

Quando você trabalha com o serviço pela primeira vez, pode ser difícil informar quais mensagens são originadas de quais serviços. É recomendável que você capture não apenas o texto exato da mensagem, mas o contexto no qual você viu a mensagem. Observe o software cliente que você está usando para executar o código de Machine Learning:

* Você está usando Management Studio? Um aplicativo externo?
* Você está executando o código R em um cliente remoto ou diretamente em um procedimento armazenado?

## <a name="sql-server-log-files"></a>SQL Server arquivos de log

Obtenha o log de erros SQL Server mais recente. O conjunto completo de logs de erros consiste nos arquivos do seguinte diretório de log padrão:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> O nome exato da pasta é diferente, dependendo do nome da instância.

## <a name="errors-returned-by-spexecuteexternalscript"></a>Erros retornados por sp_execute_external_script

Obtenha o texto completo de erros que são retornados, se houver, quando você executar o comando sp_execute_external_script.

Para remover problemas de R ou Python da consideração, você pode executar esse script, que inicia o tempo de execução de R ou Python e passa os dados de volta e para trás.

**Para R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Para Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>Erros gerados pela estrutura de extensibilidade

SQL Server gera logs separados para os tempos de execução de linguagem de script externo. Esses erros não são gerados pela linguagem Python ou R. Eles são gerados a partir dos componentes de extensibilidade no SQL Server, incluindo iniciadores específicos do idioma e seus processos de satélite.

Você pode obter esses logs dos seguintes locais padrão:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> O nome exato da pasta é diferente com base no nome da instância. Dependendo da sua configuração, a pasta pode estar em uma unidade diferente.

Por exemplo, as seguintes mensagens de log estão relacionadas à estrutura de extensibilidade:

* *Falha no LogonUser para o usuário MSSQLSERVER01*
  
  Isso pode indicar que as contas de trabalho que executam scripts externos não podem acessar a instância.

* *InitializePhysicalUsersPool falhou*
  
  Essa mensagem pode significar que as configurações de segurança estão impedindo que a instalação crie o pool de contas de trabalho que são necessárias para executar scripts externos.

* *Falha na inicialização do Gerenciador de contexto de segurança*

* *Falha na inicialização do Gerenciador de sessão satélite*

## <a name="system-events"></a>Eventos do sistema

1. Abra o Windows Visualizador de Eventos e pesquise o log de **eventos do sistema** em busca de mensagens que incluam a cadeia de caracteres *Launchpad*.
2. Abra o arquivo ExtLaunchErrorlog e procure a cadeia de caracteres *ErrorCode*. Examine a mensagem associada ao ErrorCode.

Por exemplo, as mensagens a seguir são erros comuns do sistema relacionados à estrutura de extensibilidade do SQL Server:

* *Falha ao iniciar o serviço de SQL Server Launchpad (MSSQLSERVER) devido ao seguinte erro:<text>*

* *O serviço não respondeu à solicitação de início ou de controle em tempo hábil.*

* *Um tempo limite foi atingido (120000 milissegundos) enquanto aguarda o serviço de SQL Server Launchpad (MSSQLSERVER) se conectar.*

## <a name="dump-files"></a>Arquivos de despejo

Se você tiver conhecimento sobre a depuração, poderá usar os arquivos de despejo para analisar uma falha no Launchpad.

1. Localize a pasta que contém os logs de inicialização da instalação para SQL Server. Por exemplo, no SQL Server 2016, o caminho padrão era C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log.
2. Abra a subpasta de log de inicialização específica para extensibilidade.
3. Se você precisar enviar uma solicitação de suporte, adicione todo o conteúdo dessa pasta a um arquivo compactado. Por exemplo, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
O local exato pode ser diferente no seu sistema e pode estar em uma unidade diferente da unidade C. Certifique-se de obter os logs para a instância em que o Machine Learning está instalado.

## <a name="configuration-settings"></a>Definições de configuração

Esta seção lista outros componentes ou provedores que podem ser uma fonte de erros quando você executa scripts R ou Python.

### <a name="what-network-protocols-are-available"></a>Quais protocolos de rede estão disponíveis?

Serviços de Machine Learning requer os seguintes protocolos de rede para comunicação interna entre componentes de extensibilidade e para comunicação com clientes R ou Python externos.

* Pipes nomeados
* TCP/IP

Abra SQL Server Configuration Manager para determinar se um protocolo está instalado e, se estiver instalado, para determinar se ele está habilitado.

### <a name="security-configuration-and-permissions"></a>Configuração e permissões de segurança

Para contas de trabalho:

1. No painel de controle, abra **usuários e grupos**e localize o grupo usado para executar trabalhos de script externo. Por padrão, o grupo é **SQLRUserGroup**.
2. Verifique se o grupo existe e se ele contém pelo menos uma conta de trabalho.
3. Em SQL Server Management Studio, selecione a instância em que os trabalhos R ou Python serão executados, selecione **segurança**e, em seguida, determine se há um logon para SQLRUserGroup.
4. Examine as permissões para o grupo de usuários.

Para contas de usuário individuais:

1. Determine se a instância dá suporte apenas à autenticação de modo misto, somente a logons do SQL ou à autenticação do Windows. Essa configuração afeta os requisitos de código de R ou Python.
2. Para cada usuário que precisa executar o código R, determine o nível de permissões necessário em cada banco de dados em que os objetos serão gravados do R, os dados serão acessados ou os objetos serão criados.
3. Para habilitar a execução de script, crie funções ou adicione usuários às seguintes funções, conforme necessário:

   - Todos, exceto *db_owner*: Exigir executar qualquer SCRIPT externo.
   - *db_datawriter*: Para gravar resultados de R ou Python.
   - *db_ddladmin*: Para criar novos objetos.
   - *db_datareader*: Para ler os dados usados pelo código R ou Python.
4. Observe se você alterou as contas de inicialização padrão quando instalou o SQL Server 2016.
5. Se um usuário precisar instalar novos pacotes de R ou usar pacotes de R que foram instalados por outros usuários, talvez seja necessário habilitar o gerenciamento de pacotes na instância e, em seguida, atribuir permissões adicionais. Para obter mais informações, consulte [habilitar ou desabilitar o gerenciamento de pacotes de R](r/r-package-how-to-enable-or-disable.md).

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>Quais pastas estão sujeitas a bloqueios por software antivírus?

O software antivírus pode bloquear pastas, o que impede a configuração dos recursos de Machine Learning e a execução de script bem-sucedida. Determine se alguma pasta na árvore de SQL Server está sujeita à verificação de vírus.

No entanto, quando vários serviços ou recursos são instalados em uma instância, pode ser difícil enumerar todas as pastas possíveis que são usadas pela instância. Por exemplo, quando novos recursos são adicionados, as novas pastas devem ser identificadas e excluídas.

Além disso, alguns recursos criam novas pastas dinamicamente em tempo de execução. Por exemplo, tabelas OLTP na memória, procedimentos armazenados e funções criam novos diretórios em tempo de execução. Esses nomes de pasta geralmente contêm GUIDs e não podem ser previstos. O Launchpad confiável SQL Server cria novos diretórios de trabalho para trabalhos de script R e Python.

Como talvez não seja possível excluir todas as pastas necessárias para o processo de SQL Server e seus recursos, recomendamos que você exclua toda a árvore de diretórios da instância SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>O firewall está aberto para SQL Server? A instância dá suporte a conexões remotas?

1. Para determinar se SQL Server oferece suporte a conexões remotas, consulte [Configurar conexões de servidor remoto](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Determine se uma regra de firewall foi criada para SQL Server. Por motivos de segurança, em uma instalação padrão, talvez não seja possível que o cliente R ou Python remoto se conecte à instância. Para obter mais informações, consulte [Solucionando problemas de conexão com o SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="see-also"></a>Confira também

[Solucionar problemas de aprendizado de máquina no SQL Server](machine-learning-troubleshooting-faq.md)
