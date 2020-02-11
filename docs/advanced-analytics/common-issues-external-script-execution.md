---
title: Problemas comuns do Launchpad
description: Este artigo fornece diretrizes para a solução de vários problemas que impedem a inicialização do serviço SQL Server Trusted Launchpad, incluindo problemas de configuração, alterações ou protocolos de rede ausentes.
ms.prod: sql
ms.technology: ''
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 68c731767a83acbd4b7df84843f2c140c5a63d3e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727703"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Problemas comuns com o serviço do Launchpad e a execução de script externo no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O serviço SQL Server Trusted Launchpad é compatível com a execução de script externo de R e Python. 

Vários problemas podem impedir que o Launchpad inicie, incluindo problemas de configuração, alterações ou protocolos de rede ausentes. Neste artigo, você verá diretrizes de solução para vários problemas. Caso não abordemos alguns problemas, poste perguntas no [fórum do Machine Learning Server](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR).

## <a name="determine-whether-launchpad-is-running"></a>Determinar se o Launchpad está em execução

1. Abra o painel **Serviços** (Services.msc). Outra opção é, na linha de comando, digite **SQLServerManager13.msc** ou **SQLServerManager14.msc** para abrir o [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Anote a conta de serviço em que o Launchpad está sendo executado. Cada instância em que R ou Python estiverem habilitados deve ter sua própria instância do serviço Launchpad. Por exemplo, o serviço de uma instância nomeada pode ser algo como _MSSQLLaunchpad$InstanceName_.

3. Se tiver sido interrompido, reinicie o serviço. Ao reiniciar, se houver algum problema com a configuração, uma mensagem será publicada no log de eventos do sistema e o serviço será interrompido novamente. Verifique o log de eventos do sistema para ver detalhes sobre por que o serviço parou.

4. Examine o conteúdo de RSetup.log e certifique-se de que não haja nenhum erro na instalação. Por exemplo, a mensagem *Saindo do processo com o código de erro 0* indica falha do serviço a ser iniciado.

5. Para procurar outros erros, examine o conteúdo de rlauncher.log.

## <a name="check-the-launchpad-service-account"></a>Verificar a conta de serviço do Launchpad

A conta de serviço padrão pode ser "NT Service\$SQL2016" ou "NT Service\$SQL2017". A parte final pode variar, dependendo do nome da instância do SQL.

O serviço do Launchpad (Launchpad.exe) será executado usando uma conta de serviço de baixo privilégio. No entanto, para iniciar R e Python e se comunicar com a instância do banco de dados, a conta de serviço do Launchpad requer os seguintes direitos de usuário:

- Fazer logon como um serviço (SeServiceLogonRight)
- Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)
- Ignorar verificação completa (SeChangeNotifyPrivilege)
- Ajustar cotas de memória para um processo (SeIncreaseQuotaSizePrivilege)

Para saber mais sobre esses direitos de usuário, confira a seção "Privilégios e direitos do Windows" em [Configurar contas de serviço e permissões do Windows](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Se você estiver familiarizado com o uso da ferramenta SDP (Plataforma de Diagnóstico de Suporte) para diagnóstico do SQL Server, poderá usá-la para examinar o arquivo de saída com o nome MachineName_UserRights.txt.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>O grupo de usuários do Launchpad não pode fazer logon localmente

Durante a instalação dos Serviços de Machine Learning, o SQL Server cria o grupo de usuários do Windows, **SQLRUserGroup**. Em seguida, provisiona a ele todos os direitos necessários para o Launchpad conectar-se ao SQL Server e executar trabalhos de script externo. Se esse grupo de usuários estiver habilitado, ele também será usado para executar scripts Python.

No entanto, em organizações em que políticas de segurança mais restritivas são impostas, os direitos exigidos por esse grupo podem ter sido removidos manualmente ou revogados automaticamente pela política. Se os direitos tiverem sido removidos, o Launchpad não poderá mais se conectar ao SQL Server e o SQL Server não poderá chamar o runtime externo.

Para corrigir o problema, garanta que o **SQLRUserGroup** tenha o direito de sistema **Permitir logon local**.

Para saber mais, leia o tópico [Configurar contas de serviço e permissões do Windows](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

## <a name="permissions-to-run-external-scripts"></a>Permissões para executar scripts externos

Mesmo que o Launchpad esteja configurado corretamente, ele retornará um erro se o usuário não tiver permissão para executar scripts de R ou Python.

Se você tiver instalado o SQL Server como um administrador de banco de dados ou se for um proprietário de banco de dados, receberá essa permissão automaticamente. No entanto, outros usuários geralmente têm permissões mais limitadas. Se eles tentarem executar um script do R, receberão um erro do Launchpad.

Para corrigir o problema, no SQL Server Management Studio, um administrador de segurança pode modificar o logon do SQL ou a conta de usuário do Windows executando o seguinte script:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Para saber mais, confira [GRANT (Transact-SQL](../t-sql/statements/grant-transact-sql.md).

## <a name="common-launchpad-errors"></a>Erros comuns do Launchpad

Nesta seção, você verá uma lista das mensagens de erro mais comuns retornadas pelo Launchpad.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="unable-to-launch-runtime-for-r-script"></a>"Não é possível iniciar o runtime para o script do R"

Se o grupo do Windows para usuários do R (também usado para Python) não puder fazer logon na instância que está executando o R Services, você poderá ver os seguintes erros:

- Erros gerados quando você tenta executar scripts do R:

    * *Não é possível iniciar o runtime para o script do “R”. Verifique a configuração do runtime do script do R.*

    * *Erro de script externo. Não é possível iniciar o runtime.*

- Erros gerados pelo serviço do [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)]:

    * *Falha ao inicializar o inicializador RLauncher.dll*

    * *Nenhuma dll do inicializador foi registrada!*

    * *Os logs de segurança indicam que o SERVIÇO NT da conta não pôde fazer logon*

Para saber mais sobre como conceder a esse grupo de usuários as permissões necessárias, confira [Instalar o SQL Server R Services](install/sql-r-services-windows-install.md).

> [!NOTE]
> Essa limitação não se aplicará se você usar logons SQL para executar scripts do R em uma estação de trabalho remota.
::: moniker-end

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"Falha de logon: não foi concedido ao usuário o tipo de logon solicitado"

Por padrão, [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] usa a seguinte conta na inicialização: `NT Service\MSSQLLaunchpad`. A conta é configurada pela instalação de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] para ter todas as permissões necessárias.

Se você atribuir uma conta diferente ao Launchpad ou o direito for removido por uma política no computador do SQL Server, talvez conta não tenha as permissões necessárias e você poderá ver este erro:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Falha de logon: o usuário não recebeu o tipo de logon solicitado neste computador.*

Para conceder as permissões necessárias à nova conta de serviço, use o aplicativo Política de Segurança Local e atualize as permissões na conta para incluir estas permissões:

+ Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
+ Ignorar verificação completa (SeChangeNotifyPrivilege)
+ Fazer logon como um serviço (SeServiceLogonRight)
+ Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"Não é possível se comunicar com o serviço Launchpad"

Se você tiver instalado e habilitado o aprendizado de máquina, mas receber esse erro ao tentar executar um script R ou Python, a execução do serviço do Launchpad da instância poderá ter sido interrompida.

1. Em um prompt de comando do Windows, abra o SQL Server Configuration Manager. Para obter mais informações, consulte [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Clique com o botão direito do mouse no SQL Server Launchpad da instância e, em seguida, selecione **Propriedades**.

3. Selecione a guia **Serviço** e verifique se o serviço está em execução. Se não estiver, altere o **Modo Inicial** para **Automático** e clique em **Aplicar**.

4. A reinicialização do serviço geralmente corrige o problema para que os scripts de aprendizado de máquina possam ser executados. Se a reinicialização não corrigir o problema, observe o caminho e os argumentos na propriedade **Caminho Binário** e faça o seguinte:

    a. Examine o arquivo .config do inicializador e verifique se o diretório de trabalho é válido.

    b. Verifique se o grupo do Windows usado pelo Launchpad pode se conectar à instância do SQL Server.

    c. Se você alterar qualquer uma das propriedades do serviço, reinicie o serviço Launchpad.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"Erro fatal: falha na criação do tmpFile"

Nesse cenário, você instalou com êxito os recursos de aprendizado de máquina e o Launchpad está em execução. Você tenta executar alguns códigos simples de R ou Python, mas o Launchpad falha com um erro semelhante ao seguinte: 

>*Não é possível se comunicar com o runtime do script R. Verifique os requisitos do runtime do R.*

Ao mesmo tempo, o runtime do script externo grava a seguinte mensagem como parte da mensagem STDERR: 

>*Erro fatal: falha na criação do tmpfile.*

Esse erro indica que a conta que o Launchpad está tentando usar não tem permissão para fazer logon no banco de dados. Essa situação pode ocorrer quando políticas de segurança rigorosas são implementadas. Para determinar se esse é o caso, examine os logs do SQL Server e verifique se a conta MSSQLSERVER01 foi negada no logon. As mesmas informações são fornecidas nos logs específicos dos R\_SERVICES ou PYTHON\_SERVICES. Procure ExtLaunchError.log.

Por padrão, 20 contas são configuradas e associadas ao processo Launchpad.exe, com os nomes MSSQLSERVER01 por meio de MSSQLSERVER20. Se você fizer uso intensivo de R ou Python, poderá aumentar o número de contas.

Para resolver o problema, verifique se o grupo tem as permissões *Permitir logon local* para a instância local em que os recursos de aprendizado de máquina foram instalados e habilitados. Em alguns ambientes, esse nível de permissão pode exigir uma exceção de GPO do administrador de rede.

## <a name="not-enough-quota-to-process-this-command"></a>"Não há cota suficiente para processar este comando"

Esse erro pode significar uma entre várias coisas:

- O Launchpad pode ter usuários externos insuficientes para executar a consulta externa. Por exemplo, se você estiver executando mais de 20 consultas externas simultaneamente e houver apenas 20 usuários padrão, uma ou mais consultas poderão falhar.

- Memória insuficiente disponível para processar a tarefa do R. Esse erro ocorre com mais frequência em um ambiente padrão, em que o SQL Server pode estar usando até 70% dos recursos do computador. Para saber mais sobre como modificar a configuração do servidor usar mais recursos no R, confira [Operacionalização do código R](r/operationalizing-your-r-code.md).

## <a name="cant-find-package"></a>"Não é possível encontrar o pacote"

Se você executar o código R no SQL Server e receber essa mensagem, mas não recebê-la ao executar o mesmo código fora do SQL Server, isso significa que o pacote não foi instalado na localização da biblioteca padrão usada pelo SQL Server.

Esse erro pode ocorrer de várias maneiras:

- Você instalou um novo pacote no servidor, mas o acesso foi negado, então o R instalou o pacote em uma biblioteca de usuários.

- Você instalou o R Services e, em seguida, instalou outra ferramenta do R ou conjunto de bibliotecas, incluindo Microsoft R Server (autônomo), Microsoft R Client, RStudio e assim por diante.

Para determinar a localização da biblioteca de pacotes do R usada pela instância, abra o SQL Server Management Studio (ou qualquer outra ferramenta de consulta de banco de dados), conecte-se à instância e execute o seguinte procedimento armazenado:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Resultados de exemplo

*Mensagem(ns) STDOUT do script externo:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.SQL2016\\R_SERVICES"*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

Para resolver o problema, você deve reinstalar o pacote na biblioteca da instância do SQL Server.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
>[!NOTE]
>Se você tiver atualizado uma instância do SQL Server 2016 para usar a versão mais recente do Microsoft R, a localização da biblioteca padrão será diferente. Para saber mais, confira [Usar SqlBindR para atualizar uma instância do R Services](install/upgrade-r-and-python.md).
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>Launchpad desliga devido a DLLs incompatíveis

Se você instalar o mecanismo de banco de dados com outros recursos, aplicar patches no servidor e, posteriormente, adicionar o recurso do Machine Learning usando a mídia original, a versão errada dos componentes do Machine Learning poderá ser instalada. Quando o Launchpad detecta uma incompatibilidade de versão, ele é desligado e cria um arquivo de despejo.

Para evitar esse problema, certifique-se de instalar os novos recursos no mesmo nível de patch que a instância de servidor.

**A maneira errada de atualizar:**

1. Instalar o SQL Server 2016 sem o R Services.
2. Atualizar o SQL Server 2016 (Atualização Cumulativa 2).
3. Instalar o R Services (no banco de dados) usando a mídia RTM.

**A maneira correta de atualizar:**

1. Instalar o SQL Server 2016 sem o R Services.
2. Atualizar o SQL Server 2016 para o nível de patch desejado. Por exemplo, instale o Service Pack 1 e, em seguida, a Atualização Cumulativa 2.
3. Para adicionar o recurso no nível de patch correto, execute o SP1 e a instalação do CU2 novamente e, em seguida, escolha o R Services (no banco de dados). 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>O Launchpad falhará ao iniciar se a notação 8dot3 for necessária

> [!NOTE] 
> Em sistemas mais antigos, o Launchpad poderá falhar ao iniciar se houver um requisito de notação 8dot3. Esse requisito foi removido em versões posteriores. Os clientes do SQL Server 2016 R Services devem instalar um dos seguintes:
> * SQL Server 2016 SP1 e CU1: [Atualização Cumulativa 1 para SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, Atualização Cumulativa 3 e este [hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), que está disponível sob demanda.

Para compatibilidade com R, o SQL Server 2016 R Services (no banco de dados) exigia que a unidade em que o recurso está instalado fosse compatível com a criação de nomes de arquivo curtos usando a *notação 8dot3*. Um nome de arquivo 8.3 também é chamado de um *nome de arquivo curto* e é usado para compatibilidade com versões anteriores do Microsoft Windows ou como uma alternativa a nomes de arquivo longos.

Se o volume em que você está instalando o R não for compatível com nomes de arquivos curtos, os processos que iniciam o R por meio do SQL Server não poderão localizar o executável correto e o Launchpad não será iniciado.

Como alternativa, você deverá habilitar a notação 8dot3 no volume em que o SQL Server e o R Services estão instalados. Em seguida, será necessário fornecer o nome curto para o diretório de trabalho no arquivo de configuração do R Services.

1. Para habilitar a notação 8dot3, execute o utilitário fsutil com o argumento *8dot3name*, conforme descrito aqui: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Depois que a notação 8dot3 estiver habilitada, abra o arquivo RLauncher.config e observe a propriedade de `WORKING_DIRECTORY`. Para saber mais sobre como encontrar esse arquivo, confira [Coleta de dados para solucionar problemas do Machine Learning](data-collection-ml-troubleshooting-process.md).

3. Use o utilitário fsutil com o argumento *file* para especificar um caminho de arquivo curto para a pasta especificada em WORKING_DIRECTORY.

4. Edite o arquivo de configuração para especificar o mesmo diretório de trabalho que você inseriu na propriedade WORKING_DIRECTORY. Como alternativa, especifique outro diretório de trabalho e escolha um caminho que já seja compatível com a notação 8dot3.
::: moniker-end

## <a name="next-steps"></a>Próximas etapas

[Solução de problemas dos Serviços de Machine Learning e problemas conhecidos](machine-learning-troubleshooting-faq.md)

[Coleta de dados para a solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

[Perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexões de mecanismo de banco de dados](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
