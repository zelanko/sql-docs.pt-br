---
title: Solucionar problemas de coleta de dados para aprendizado de máquina - serviços de aprendizado de máquina do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2723131e66cc149209e77884a3a9c160d4c27a0e
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644985"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Solucionar problemas de coleta de dados para aprendizado de máquina

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve os métodos de coleta de dados, que você deve usar durante a tentativa de resolver problemas por conta própria ou com a Ajuda do cliente da Microsoft dão suporte.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 serviços de Machine Learning (R e Python)

## <a name="sql-server-version-and-edition"></a>Edição e versão do SQL Server

SQL Server 2016 R Services é a primeira versão do SQL Server para incluir o suporte R integrado. SQL Server 2016 Service Pack 1 (SP1) inclui vários aperfeiçoamentos importantes, incluindo a capacidade de executar scripts externos. Se você for um cliente do SQL Server 2016, você deve considerar a instalação do SP1 ou posterior.

SQL Server 2017 adicionada a integração de linguagem Python. Você não é possível obter a integração de recursos do Python em versões anteriores.

Para assistência obtendo edition e versões, neste artigo, que lista os números de compilação para cada um, consulte o [versões do SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

Dependendo da edição do SQL Server que você está usando, algumas funcionalidades de aprendizado de máquina pode estar indisponível ou ser limitado. A seguinte lista de artigos de recursos de aprendizado de máquina nas edições Enterprise, Developer, Standard e Express.

* [Edições e recursos com suporte do SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [Recursos de R e Python com as edições do SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>Versões de idioma e a ferramenta de R

Em geral, a versão do Microsoft R é instalado quando você seleciona o recurso R Services ou o recurso de serviços de Machine Learning é determinada pelo número de compilação do SQL Server. Se você atualizar ou aplicar patch do SQL Server, é necessário atualizar ou aplicar patch seus componentes de R.

Para obter uma lista das versões e links para downloads de componentes de R, consulte [instalar componentes de aprendizado de máquina sem acesso à internet](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access). Em computadores com acesso à internet, a versão necessária do R é identificada e instalada automaticamente.

É possível atualizar os componentes de R Server separadamente do mecanismo de banco de dados do SQL Server em um processo conhecido como ligação. Portanto, a versão do R que você usa quando você executa o código R no SQL Server pode ser diferentes dependendo da versão instalada do SQL Server e o se você tiver migrado do servidor para a versão mais recente do R.

### <a name="determine-the-r-version"></a>Determinar a versão do R

É a maneira mais fácil para determinar a versão do R obter as propriedades de tempo de execução, executando uma instrução como o seguinte:

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
> Se o R Services não estiver funcionando, tente executar somente a parte do script de R do RGui.

Como último recurso, você pode abrir arquivos no servidor para determinar a versão instalada. Para fazer isso, localize o arquivo rlauncher log para obter o local do tempo de execução de R e o diretório de trabalho atual. É recomendável que você verifique e abre uma cópia do arquivo para que você não alterar acidentalmente quaisquer propriedades.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Para obter a versão do R e versões de RevoScaleR, abra um prompt de comando do R ou abra o RGui que está associada com a instância.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

O console do R Exibe as informações de versão na inicialização. Por exemplo, a versão a seguir representa a configuração padrão do SQL Server 2017 CTP 2.0:

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Versões do Python

Há várias maneiras de obter a versão do Python. A maneira mais fácil é executar essa instrução do Management Studio ou qualquer outra ferramenta de consulta SQL:

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

Se não estiver executando serviços de Machine Learning, você pode determinar a versão instalada do Python, observando o arquivo pythonlauncher.config. É recomendável que você verifique e abre uma cópia do arquivo para que você não alterar acidentalmente quaisquer propriedades.

1. Para o SQL Server 2017 somente: `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config `
2. Obter o valor de **PYTHONHOME**.
3. Obtenha o valor do diretório de trabalho atual.

> [!NOTE]
> Se você tiver instalado o Python e R no SQL Server 2017, o diretório de trabalho e o pool de contas de trabalho são compartilhados para as linguagens R e Python.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>São várias instâncias do R ou Python instalado?

Verifique se mais de uma cópia das bibliotecas do R está instalada no computador. Essa duplicação poderá acontecer se:

* Durante a instalação você selecionar o R Services (no banco de dados) e o R Server (autônomo).
* Instalar o Microsoft R Client, além do SQL Server.
* Um conjunto diferente de bibliotecas do R foi instalado usando as ferramentas de R para Visual Studio, R Studio, Microsoft R Client ou outro IDE R.
* O computador hospeda várias instâncias do SQL Server e mais de uma instância usa o aprendizado de máquina.

As mesmas condições se aplicam ao Python.

Se você achar que várias bibliotecas ou tempos de execução são instalados, certifique-se de que você obtém apenas os erros associados com tempos de execução do Python ou R que são usados pela instância do SQL Server.

## <a name="origin-of-errors"></a>Origem de erros

Os erros que você vê quando você tentar executar o código R podem vir de qualquer uma das seguintes fontes:

* Mecanismo de banco de dados do SQL Server, incluindo o procedimento armazenado sp_execute_external_script
* Launchpad confiável para o SQL Server
* Outros componentes da estrutura de extensibilidade, incluindo processos de satélite e dos inicializadores de R e Python
* Provedores, como o Microsoft Open Connectivity (ODBC) do banco de dados
* Linguagem R

Quando você trabalha com o serviço pela primeira vez, pode ser difícil saber quais mensagens provenientes de quais serviços. É recomendável que você capture não apenas o texto da mensagem exata, mas o contexto no qual você viu a mensagem. Observe que o software cliente que você está usando para executar o código de aprendizado de máquina:

* Você está usando o Management Studio? Um aplicativo externo?
* Você está executando o código R em um cliente remoto ou diretamente em um procedimento armazenado?

## <a name="sql-server-log-files"></a>Arquivos de log do SQL Server

Obtenha o log de erros de servidor SQL mais recente. O conjunto completo de logs de erros consiste nos arquivos do diretório de log padrão a seguir:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> O nome exato da pasta é diferente dependendo do nome da instância.

## <a name="errors-returned-by-spexecuteexternalscript"></a>Erros retornados pelo sp_execute_external_script

Obter o texto completo de erros que são retornados, se houver, quando você executa o comando de sp_execute_external_script.

Para remover os problemas de R ou Python da consideração, você pode executar este script, que inicia o tempo de execução de R ou Python e passa os dados e para trás.

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

SQL Server gera logs separados para os tempos de execução de linguagem de script externo. Esses erros não são gerados pela linguagem Python ou R. Eles são gerados a partir de componentes de extensibilidade no SQL Server, incluindo os inicializadores de idioma específico e seus processos de satélite.

Você pode obter esses logs nos seguintes locais padrão:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog `

> [!NOTE]
> O nome da pasta exata varia de acordo com o nome da instância. Dependendo da sua configuração, a pasta pode ser em uma unidade diferente.

Por exemplo, as mensagens de log a seguir estão relacionadas à estrutura de extensibilidade:

* *Falha de LogonUser para o usuário MSSQLSERVER01*
  
  Isso pode indicar que as contas de trabalho que executam scripts externos não podem acessar a instância.

* *InitializePhysicalUsersPool falhou*
  
  Essa mensagem pode significar que as configurações de segurança estão impedindo a instalação de criação do pool de contas de trabalho que são necessários para executar scripts externos.

* *Falha na inicialização do Gerenciador de contexto de segurança*

* *Falha na inicialização do Gerenciador de sessão de satélite*

## <a name="system-events"></a>Eventos do sistema

1. Abra o Visualizador de eventos do Windows e pesquise o **evento do sistema** log de mensagens que incluem a cadeia de caracteres *Launchpad*.
2. Abra o arquivo ExtLaunchErrorlog e procure a cadeia de caracteres *ErrorCode*. Examine a mensagem que está associada com o código de erro.

Por exemplo, as seguintes mensagens são erros de sistema comuns relacionados à estrutura de extensibilidade do SQL Server:

* *O serviço Launchpad do SQL Server (MSSQLSERVER) falhou ao iniciar devido ao seguinte erro:  <text>*

* *O serviço não respondeu à solicitação de início ou controle de forma oportuna.*

* *Um tempo limite foi atingido (120000 milissegundos) enquanto aguarda o serviço Launchpad do SQL Server (MSSQLSERVER) para se conectar.*

## <a name="dump-files"></a>Arquivos de despejo

Se você tiver conhecimentos sobre a depuração, você pode usar os arquivos de despejo para analisar uma falha na barra inicial.

1. Localize a pasta que contém os logs de inicialização de instalação do SQL Server. Por exemplo, no SQL Server 2016, o caminho padrão era C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log.
2. Abra a subpasta de log de inicialização é específica para extensibilidade.
3. Se você precisar enviar uma solicitação de suporte, adicione todo o conteúdo dessa pasta para um arquivo compactado. Por exemplo, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
O local exato pode ser diferente em seu sistema, e ela pode estar em uma unidade diferente da unidade C. Certifique-se de obter os logs para a instância onde o aprendizado de máquina está instalado.

## <a name="configuration-settings"></a>Definições de configuração

Esta seção lista os componentes adicionais ou provedores que podem ser uma fonte de erros quando você executa scripts R ou Python.

### <a name="what-network-protocols-are-available"></a>Quais protocolos de rede estão disponíveis?

Serviços de Machine Learning exige os seguintes protocolos de rede para a comunicação interna entre os componentes de extensibilidade e para comunicação com clientes externos de R ou Python.

* Pipes nomeados
* TCP/IP

Abra o SQL Server Configuration Manager para determinar se um protocolo está instalado e, se ele estiver instalado, para determinar se ela está habilitada.

### <a name="security-configuration-and-permissions"></a>Configuração de segurança e permissões

Para contas de trabalho:

1. No painel de controle, abra **usuários e grupos**e localize o grupo usado para executar trabalhos de script externo. Por padrão, o grupo é **SQLRUserGroup**.
2. Verifique se o grupo existe e se contém pelo menos uma conta de trabalho.
3. No SQL Server Management Studio, selecione a instância em que serão executados trabalhos do R ou Python, selecione **segurança**e, em seguida, determine se há um logon para SQLRUserGroup.
4. Examine as permissões para o grupo de usuários.

Para contas de usuário:

1. Determine se a instância dá suporte à autenticação de modo misto, somente logons do SQL ou somente a autenticação do Windows. Essa configuração afeta o R ou requisitos de código do Python.
2. Para cada usuário que precisa executar o código R, determine o nível necessário de permissões em cada banco de dados em que objetos serão gravados de R, dados serão acessados ou objetos serão criados.
3. Para habilitar a execução do script, criar funções ou adicionar usuários a funções a seguir, conforme necessário:

   - Tudo, exceto *db_owner*: Exigir executar qualquer SCRIPT externo.
   - *db_datawriter*: Para gravar os resultados de R ou Python.
   - *db_ddladmin*: Para criar novos objetos.
   - *db_datareader*: Para ler dados que são usados pelo código R ou Python.
4. Observe que se você alterou as contas de inicialização padrão, quando você instalou o SQL Server 2016.
5. Se um usuário precisa para instalar novos pacotes de R ou usar os pacotes de R que foram instalados por outros usuários, talvez você precise habilitar o gerenciamento de pacote na instância e, em seguida, atribua permissões adicionais. Para obter mais informações, consulte [habilitar ou desabilitar o gerenciamento de pacotes R](r/r-package-how-to-enable-or-disable.md).

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>Quais pastas estão sujeitos a bloqueio pelo software antivírus?

Software antivírus pode bloquear pastas, que impede a instalação dos recursos e a execução bem-sucedida do script de aprendizado de máquina. Determine se as pastas na árvore do SQL Server estão sujeitos a verificação de vírus.

No entanto, quando vários serviços ou recursos são instalados em uma instância, pode ser difícil enumerar todas as pastas possíveis que são usadas pela instância. Por exemplo, quando novos recursos são adicionados, as novas pastas devem ser identificadas e excluídas.

Além disso, alguns recursos criam novas pastas dinamicamente em tempo de execução. Por exemplo, tabelas OLTP na memória, procedimentos armazenados e funções de criam novos diretórios em tempo de execução. Geralmente, esses nomes de pastas contêm os GUIDs e não podem ser previstas. O Launchpad confiável do SQL Server cria novos diretórios de trabalho para o R e trabalhos de script do Python.

Porque talvez ele não seja possível excluir todas as pastas que são necessários para o processo do SQL Server e seus recursos, é recomendável que você exclua a árvore de diretório de instância inteira do SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>O firewall está aberta para o SQL Server? A instância dá suporte a conexões remotas?

1. Para determinar se o SQL Server dá suporte a conexões remotas, consulte [configurar conexões de servidor remoto](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Determine se uma regra de firewall foi criada para o SQL Server. Por motivos de segurança, em uma instalação padrão, pode não ser possível para o cliente remoto de R ou Python para se conectar à instância. Para obter mais informações, consulte [solução de problemas de conexão ao SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="see-also"></a>Confira também

[Solucionar problemas de aprendizado de máquina no SQL Server](machine-learning-troubleshooting-faq.md)
