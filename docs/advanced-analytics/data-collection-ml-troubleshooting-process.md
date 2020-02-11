---
title: Solucionar problemas de coleta de dados
description: Aprenda métodos de coleta de dados que você deve usar ao tentar resolver problemas por conta própria ou com a ajuda do atendimento ao cliente da Microsoft.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15c570594f84bf8d1d61abac4bc4e4c372f18784
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727610"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Solucionar problemas de coleta de dados para aprendizado de máquina

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve os métodos de coleta de dados que você deve usar ao tentar resolver problemas por conta própria ou com a ajuda do atendimento ao cliente da Microsoft.

## <a name="sql-server-version-and-edition"></a>Versão e edição do SQL Server

O SQL Server 2016 R Services é a primeira versão do SQL Server a incluir suporte ao R integrado. O SQL Server 2016 SP1 (Service Pack 1) inclui várias melhorias importantes, incluindo a capacidade de executar scripts externos. Se você estiver usando o SQL Server 2016, considere instalar o SP1 ou posterior.

O SQL Server 2017 e posteriores têm integração com a linguagem Python. Você não pode obter a integração com recursos do Python em versões anteriores.

Se precisar de ajuda para obter a edição e as versões, confira este artigo, que lista os números de build para cada uma das [versões do SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

Dependendo da edição do SQL Server que você está usando, algumas funcionalidades de aprendizado de máquina podem estar não disponíveis ou limitadas. Os artigos a seguir listam os recursos de aprendizado de máquina nas edições Enterprise, Developer, Standard e Express.

* [Edições e recursos compatíveis do SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [Recursos do R e do Python classificados pelas edições do SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>Versões da linguagem e da ferramenta R

Em geral, a versão do Microsoft R instalada quando você seleciona o recurso R Services ou o recurso Serviços de Machine Learning é determinada pelo número de build do SQL Server. Se você atualizar o SQL Server ou aplicar um patch a ele, também será necessário realizar o mesmo procedimento aos respectivos componentes do R.

Para obter uma lista de versões e links para downloads de componentes do R, confira [Instalar componentes de aprendizado de máquina sem acesso à Internet](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access). Em computadores com acesso à Internet, a versão necessária do R é identificada e instalada automaticamente.

É possível atualizar os componentes do R Server separadamente do mecanismo de banco de dados SQL Server, em um processo conhecido como associação. Assim, a versão do R que você usa ao executar o código R no SQL Server pode ser diferente, dependendo da versão instalada do SQL Server e também de você ter migrado ou não o servidor para a versão mais recente do R.

### <a name="determine-the-r-version"></a>Determinar a versão do R

A maneira mais fácil de determinar a versão do R é obter as propriedades de runtime executando uma instrução como a seguinte:

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
> Se o R Services não estiver funcionando, tente executar apenas a parte do script R por meio do RGui.

Como último recurso, você pode abrir os arquivos no servidor para determinar a versão instalada. Para fazer isso, localize o arquivo rlauncher.config para obter a localização do runtime do R e o diretório de trabalho atual. Recomendamos que você faça e abra uma cópia do arquivo para que você não altere acidentalmente nenhuma propriedade.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* Microsoft SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Para obter a versão do R e as versões do RevoScaleR, abra um prompt de comando do R ou abra o RGui associado à instância.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* Microsoft SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

O console do R exibe as informações de versão na inicialização. Por exemplo, a versão a seguir representa a configuração padrão para o SQL Server 2017:

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Versões do Python

Há várias maneiras de obter a versão do Python. A maneira mais fácil é executar essa instrução por meio do Management Studio ou de qualquer outra ferramenta de consulta SQL:

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

Se os Serviços de Machine Learning não estiverem em execução, você poderá determinar a versão instalada do Python examinando o arquivo pythonlauncher.config. Recomendamos que você faça e abra uma cópia do arquivo para que você não altere acidentalmente nenhuma propriedade.

1. Somente para o SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. Obtenha o valor para **PYTHONHOME**.
3. Obtenha o valor do diretório de trabalho atual.

> [!NOTE]
> Se você tiver instalado o Python e o R no SQL Server 2017, o diretório de trabalho e o pool de contas de trabalho serão compartilhados para as linguagens R e Python.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>Várias instâncias do R ou Python estão instaladas?

Verifique se mais de uma cópia das bibliotecas do R está instalada no computador. Essa duplicação poderá ocorrer se:

* Durante a instalação, você selecionar ambos o R Services (no banco de dados) e o R Server (autônomo).
* Você instalar o Microsoft R Client, além do SQL Server.
* Um conjunto diferente de bibliotecas do R tiver sido instalado usando as Ferramentas do R para Visual Studio, o R Studio, o Microsoft R Client ou outro IDE do R.
* O computador hospedar várias instâncias do SQL Server e mais de uma instância usar o aprendizado de máquina.

As mesmas condições se aplicam ao Python.

Se você descobrir que várias bibliotecas ou runtimes estão instalados, verifique se você obtém apenas os erros associados aos runtimes do Python ou do R que são usados pela instância de SQL Server.

## <a name="origin-of-errors"></a>Origem dos erros

Os erros que você vê quando tenta executar o código R podem vir de qualquer uma das seguintes origens:

* O mecanismo de banco de dados do SQL Server, incluindo o procedimento armazenado sp_execute_external_script
* O SQL Server Trusted Launchpad
* Outros componentes da estrutura de extensibilidade, incluindo os inicializadores do R e do Python e os respectivos processos satélite
* Provedores, tais como o Microsoft ODBC (Open Database Connectivity)
* Linguagem R

Quando você trabalha com o serviço pela primeira vez, pode ser difícil informar quais mensagens são originadas de quais serviços. É recomendável que você capture não apenas o texto exato da mensagem, mas também o contexto no qual você a viu. Observe o software cliente que você está usando para executar o código de aprendizado de máquina:

* Você está usando o Management Studio? Ou talvez um aplicativo externo?
* Você está executando o código R em um cliente remoto ou diretamente em um procedimento armazenado?

## <a name="sql-server-log-files"></a>Arquivos de log do SQL Server

Obtenha o ERRORLOG mais recente do SQL Server. O conjunto completo de logs de erros consiste nos arquivos do seguinte diretório de log padrão:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* Microsoft SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> O nome exato da pasta é diferente, dependendo do nome da instância.

## <a name="errors-returned-by-sp_execute_external_script"></a>Erros retornados por sp_execute_external_script

Ao executar o comando sp_execute_external_script, obtenha o texto completo dos erros que são retornados, se houver.

Para eliminar a possibilidade de problemas de R ou de Python, é possível executar este script, que inicia o runtime do R ou do Python, passa os dados e retorna-os.

**Para o R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Para o Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>Erros gerados pela estrutura de extensibilidade

O SQL Server gera logs separados para os runtimes de linguagem de script externo. Esses erros não são gerados pela linguagem Python ou R. Eles são gerados dos componentes de extensibilidade no SQL Server, incluindo inicializadores específicos a uma linguagem e os respectivos processos satélite.

Você pode obter esses logs dos seguintes locais padrão:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* Microsoft SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> O nome exato da pasta é diferente, dependendo do nome da instância. Dependendo da sua configuração, a pasta pode estar em uma unidade diferente.

Por exemplo, as seguintes mensagens de log estão relacionadas à estrutura de extensibilidade:

* *Falha em LogonUser para o usuário MSSQLSERVER01*
  
  Isso pode indicar que as contas de trabalho que executam scripts externos não podem acessar a instância.

* *InitializePhysicalUsersPool falhou*
  
  Essa mensagem pode significar que as configurações de segurança estão impedindo que a instalação crie o pool de contas de trabalho que são necessárias para executar scripts externos.

* *Falha na inicialização do Gerenciador de Contexto de Segurança*

* *Falha na inicialização do Gerenciador de Sessão Satélite*

## <a name="system-events"></a>Eventos do sistema

1. Abra o Visualizador de Eventos do Windows e pesquise o log de **Eventos do Sistema** em busca de mensagens que incluam a cadeia de caracteres *Launchpad*.
2. Abra o arquivo ExtLaunchErrorlog e procure a cadeia de caracteres *ErrorCode*. Examine a mensagem associada ao ErrorCode.

Por exemplo, as mensagens a seguir são erros comuns do sistema relacionados à estrutura de extensibilidade do SQL Server:

* *O serviço do SQL Server Launchpad (MSSQLSERVER) falhou ao iniciar devido ao seguinte erro: <text>*

* *O serviço não respondeu à solicitação de início ou de controle em um tempo oportuno.*

* *O tempo limite foi alcançado (120.000 milissegundos) ao aguardar o serviço SQL Server Launchpad (MSSQLSERVER) se conectar.*

## <a name="dump-files"></a>Arquivos de despejo

Se tiver conhecimento sobre depuração, você poderá usar os arquivos de despejo para analisar uma falha no Launchpad.

1. Localize a pasta que contém os logs de inicialização da instalação do SQL Server. Por exemplo, no SQL Server 2016, o caminho padrão era C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log.
2. Abra a subpasta de log de inicialização específica para extensibilidade.
3. Se você precisar enviar uma solicitação de suporte, adicione todo o conteúdo dessa pasta a um arquivo compactado. Por exemplo, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
A localização exata pode ser diferente no seu sistema e pode estar em uma unidade diferente da unidade C. Verifique se você obteve os logs para a instância em que o aprendizado de máquina está instalado.

## <a name="configuration-settings"></a>Definições de configuração

Esta seção lista outros componentes ou provedores que podem ser uma fonte de erros quando você executa scripts R ou Python.

### <a name="what-network-protocols-are-available"></a>Quais protocolos de rede estão disponíveis?

Os Serviços de Machine Learning requerem os protocolos de rede a seguir para comunicação interna entre componentes de extensibilidade e para comunicação com clientes R ou Python externos.

* Pipes nomeados
* TCP/IP

Abra o SQL Server Configuration Manager para determinar se um protocolo está instalado e, caso esteja, para determinar se ele está habilitado.

### <a name="security-configuration-and-permissions"></a>Permissões e configuração de segurança

Para contas de trabalho:

1. No Painel de Controle, abra **Usuários e Grupos** e localize o grupo usado para executar trabalhos de script externo. Por padrão, o grupo é **SQLRUserGroup**.
2. Verifique se o grupo existe e se ele contém pelo menos uma conta de trabalho.
3. No SQL Server Management Studio, selecione a instância em que os trabalhos do R ou Python serão executados, selecione **Segurança** e, em seguida, determine se há um logon para SQLRUserGroup.
4. Examine as permissões para o grupo de usuários.

Para contas de usuário individuais:

1. Determine se a instância dá suporte apenas à autenticação de modo misto, somente a logons do SQL ou somente à autenticação do Windows. Essa configuração afeta os requisitos de código do R ou do Python.
2. Para cada usuário que precisa executar o código R, determine o nível de permissões necessário em cada banco de dados em que objetos serão gravados do R, dados serão acessados ou objetos serão criados.
3. Para habilitar a execução de script, crie funções ou adicione usuários às seguintes funções, conforme necessário:

   - Todos, exceto *db_owner*: Exigem EXECUTE ANY EXTERNAL SCRIPT.
   - *db_datawriter*: Para gravar resultados do R ou do Python.
   - *db_ddladmin*: Para criar novos objetos.
   - *db_datareader*: Para ler dados usados pelo código R ou Python.
4. Observe se você alterou alguma conta de inicialização padrão quando instalou o SQL Server 2016.
5. Se um usuário precisar instalar novos pacotes do R ou usar pacotes do R que foram instalados por outros usuários, talvez seja necessário habilitar o gerenciamento de pacotes na instância e, em seguida, atribuir permissões adicionais. Para obter mais informações, confira [Habilitar ou desabilitar o gerenciamento de pacotes do R](r/r-package-how-to-enable-or-disable.md).

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>Quais pastas estão sujeitas a bloqueios por software antivírus?

Os softwares antivírus podem bloquear pastas, o que impede a configuração dos recursos de Machine Learning e a execução bem-sucedida de scripts. Determine se alguma pasta na árvore do SQL Server está sujeita à verificação de vírus.

No entanto, quando vários serviços ou recursos são instalados em uma instância, pode ser difícil enumerar todas as pastas que possivelmente são usadas pela instância. Por exemplo, quando novos recursos são adicionados, as novas pastas devem ser identificadas e excluídas.

Além disso, alguns recursos criam pastas dinamicamente no runtime. Por exemplo, tabelas OLTP in-memory, procedimentos armazenados e funções criam novos diretórios no runtime. Esses nomes de pasta geralmente contêm GUIDs e não podem ser previstos. O SQL Server Trusted Launchpad cria novos diretórios de trabalho para trabalhos de script R e Python.

Já que talvez não seja possível excluir todas as pastas necessárias para o processo do SQL Server e os respectivos recursos, recomendamos que você exclua toda a árvore de diretórios da instância do SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>O firewall está aberto para o SQL Server? A instância dá suporte a conexões remotas?

1. Para determinar se o SQL Server dá suporte a conexões remotas, confira [Configurar conexões de servidor remoto](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Determine se uma regra de firewall foi criada para o SQL Server. Por motivos de segurança, em uma instalação padrão, talvez não seja possível que o cliente R ou Python remoto se conecte à instância. Para obter mais informações, confira [Solucionar problemas ao se conectar a uma instância do SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="see-also"></a>Confira também

[Como solucionar problemas de aprendizado de máquina no SQL Server](machine-learning-troubleshooting-faq.md)
