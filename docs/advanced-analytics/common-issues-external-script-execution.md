---
title: Problemas comuns com o serviço Launchpad e a execução de script externo
ms.prod: sql
ms.technology: ''
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c90c59f3b59850bb0e2d1cf4cf40eb569e965eba
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715281"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Problemas comuns com o serviço Launchpad e a execução de script externo no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server serviço Launchpad confiável dá suporte à execução de script externo para R e Python. 

Vários problemas podem impedir que o Launchpad inicie, incluindo problemas de configuração ou alterações ou protocolos de rede ausentes. Este artigo fornece orientação para a solução de muitos problemas. Para qualquer um que não tenhamos sido detectado, você pode postar perguntas no [Fórum de Machine Learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR).

## <a name="determine-whether-launchpad-is-running"></a>Determinar se o Launchpad está em execução

1. Abra o painel **Serviços** (Services. msc). Ou, na linha de comando, digite **SQLServerManager13. msc** ou **SQLServerManager14. msc** para abrir [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Anote a conta de serviço em que o Launchpad está sendo executado. Cada instância em que R ou Python está habilitada deve ter sua própria instância do serviço Launchpad. Por exemplo, o serviço para uma instância nomeada pode ser algo como _MSSQLLaunchpad $ InstanceName_.

3. Se o serviço for interrompido, reinicie-o. Ao reiniciar, se houver algum problema com a configuração, uma mensagem será publicada no log de eventos do sistema e o serviço será interrompido novamente. Verifique o log de eventos do sistema para obter detalhes sobre por que o serviço parou.

4. Examine o conteúdo de RSetup. log e certifique-se de que não haja nenhum erro na instalação. Por exemplo, a mensagem que *sai com o código 0* indica falha no início do serviço.

5. Para procurar outros erros, examine o conteúdo de rlauncher. log.

## <a name="check-the-launchpad-service-account"></a>Verificar a conta de serviço Launchpad

A conta de serviço padrão pode ser "NT\$Service sql2016" ou "NT\$Service sql2017". A parte final pode variar, dependendo do nome da instância do SQL.

O serviço Launchpad (Launchpad. exe) é executado usando uma conta de serviço de baixo privilégio. No entanto, para iniciar R e Python e se comunicar com a instância do banco de dados, a conta de serviço Launchpad requer os seguintes direitos de usuário:

- Fazer logon como um serviço (SeServiceLogonRight)
- Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)
- Ignorar verificação completa (SeChangeNotifyPrivilege)
- Ajustar cotas de memória para um processo (SeIncreaseQuotaSizePrivilege)

Para obter informações sobre esses direitos de usuário, consulte a seção "privilégios e direitos do Windows" em [Configurar contas de serviço e permissões do Windows](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Se você estiver familiarizado com o uso da ferramenta SDP (plataforma de diagnóstico de suporte) para diagnóstico de SQL Server, poderá usar o SDP para examinar o arquivo de saída com o nome MachineName_UserRights. txt.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>O grupo de usuários para Launchpad não pode fazer logon localmente

Durante a instalação do Serviços de Machine Learning, SQL Server cria o grupo de usuários do Windows **SQLRUserGroup** e, em seguida, o provisiona com todos os direitos necessários para que o Launchpad se conecte ao SQL Server e execute trabalhos de script externo. Se esse grupo de usuários estiver habilitado, ele também será usado para executar scripts Python.

No entanto, em organizações nas quais políticas de segurança mais restritivas são impostas, os direitos exigidos por esse grupo podem ter sido removidos manualmente ou podem ser revogados automaticamente pela política. Se os direitos tiverem sido removidos, o Launchpad não poderá mais se conectar ao SQL Server e SQL Server não poderá chamar o tempo de execução externo.

Para corrigir o problema, garanta que o **SQLRUserGroup** tenha o direito de sistema **Permitir logon local**.

Para saber mais, leia o tópico [Configurar contas de serviço e permissões do Windows](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

## <a name="permissions-to-run-external-scripts"></a>Permissões para executar scripts externos

Mesmo que o Launchpad esteja configurado corretamente, ele retornará um erro se o usuário não tiver permissão para executar scripts R ou Python.

Se você instalou SQL Server como um administrador de banco de dados ou se for um proprietário de banco de dados, receberá essa permissão automaticamente. No entanto, outros usuários geralmente têm permissões mais limitadas. Se eles tentarem executar um script do R, eles receberão um erro de Launchpad.

Para corrigir o problema, em SQL Server Management Studio, um administrador de segurança pode modificar o logon do SQL ou a conta de usuário do Windows executando o seguinte script:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Para obter mais informações, consulte [Grant (Transact-SQL](../t-sql/statements/grant-transact-sql.md).

## <a name="common-launchpad-errors"></a>Erros de Launchpad comuns

Esta seção lista as mensagens de erro mais comuns que o Launchpad retorna.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="unable-to-launch-runtime-for-r-script"></a>"Não é possível iniciar o tempo de execução para o script R"

Se o grupo do Windows para usuários do R (também usado para Python) não puder fazer logon na instância do que está executando o R Services, você poderá ver os seguintes erros:

- Erros gerados quando você tenta executar scripts do R:

    * *Não é possível iniciar o tempo de execução para o script do “R”. Verifique a configuração do tempo de execução do script do R.*

    * *Erro de script externo. Não é possível iniciar o tempo de execução.*

- Erros gerados pelo [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] serviço:

    * *Falha ao inicializar o inicializador RLauncher.dll*

    * *Nenhuma dll do inicializador foi registrada!*

    * *Os logs de segurança indicam que o serviço NT da conta não pôde fazer logon*

Para obter informações sobre como conceder a esse grupo de usuários as permissões necessárias, consulte [Install SQL Server R Services](install/sql-r-services-windows-install.md).

> [!NOTE]
> Essa limitação não se aplicará se você usar logons SQL para executar scripts do R em uma estação de trabalho remota.
::: moniker-end

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"Falha de logon: o usuário não recebeu o tipo de logon solicitado"

Por padrão, [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] o usa a seguinte conta na inicialização `NT Service\MSSQLLaunchpad`:. A conta é configurada pela [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] instalação do para ter todas as permissões necessárias.

Se você atribuir uma conta diferente ao Launchpad, ou a direita for removida por uma política no computador SQL Server, a conta poderá não ter as permissões necessárias e você poderá ver esse erro:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Falha de logon: o usuário não recebeu o tipo de logon solicitado neste computador.*

Para conceder as permissões necessárias para a nova conta de serviço, use o aplicativo de política de segurança local e atualize as permissões na conta para incluir as seguintes permissões:

+ Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
+ Ignorar verificação completa (SeChangeNotifyPrivilege)
+ Fazer logon como um serviço (SeServiceLogonRight)
+ Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"Não é possível se comunicar com o serviço Launchpad"

Se você tiver instalado e habilitado o aprendizado de máquina, mas receber esse erro ao tentar executar um script R ou Python, o serviço Launchpad da instância poderá ter parado de ser executado.

1. Em um prompt de comando do Windows, abra o SQL Server Configuration Manager. Para obter mais informações, consulte [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Clique com o botão direito do mouse em SQL Server Launchpad para a instância e selecione **Propriedades**.

3. Selecione a guia **serviço** e, em seguida, verifique se o serviço está em execução. Se não estiver em execução, altere o **modo de início** para **automático**e, em seguida, selecione **aplicar**.

4. A reinicialização do serviço geralmente corrige o problema para que os scripts do Machine Learning possam ser executados. Se a reinicialização não corrigir o problema, observe o caminho e os argumentos na propriedade **caminho binário** e faça o seguinte:

    a. Examine o arquivo. config do inicializador e verifique se o diretório de trabalho é válido.

    b. Verifique se o grupo do Windows usado pelo Launchpad pode se conectar à instância de SQL Server.

    c. Se você alterar qualquer uma das propriedades do serviço, reinicie o serviço Launchpad.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"Falha fatal ao criar tmpFile"

Nesse cenário, você instalou com êxito os recursos do Machine Learning e o Launchpad está em execução. Você tenta executar alguns códigos R ou Python simples, mas a barra inicial falha com um erro semelhante ao seguinte: 

>*Não é possível se comunicar com o tempo de execução do script R. Verifique os requisitos do tempo de execução do R.*

Ao mesmo tempo, o tempo de execução de script externo grava a seguinte mensagem como parte da mensagem STDERR: 

>*Erro fatal: falha na criação de tmpfile.*

Esse erro indica que a conta que o Launchpad está tentando usar não tem permissão para fazer logon no banco de dados. Essa situação pode ocorrer quando políticas de segurança estritas são implementadas. Para determinar se esse é o caso, examine os logs de SQL Server e verifique se a conta MSSQLSERVER01 foi negada no logon. As mesmas informações são fornecidas nos logs que são específicos do R\_Services ou dos serviços do Python.\_ Procure ExtLaunchError. log.

Por padrão, 20 contas são configuradas e associadas ao processo Launchpad. exe, com os nomes MSSQLSERVER01 por meio de MSSQLSERVER20. Se você fizer uso intensivo de R ou Python, poderá aumentar o número de contas.

Para resolver o problema, verifique se o grupo tem permissões de *logon local* para a instância local em que os recursos de Machine Learning foram instalados e habilitados. Em alguns ambientes, esse nível de permissão pode exigir uma exceção de GPO do administrador de rede.

## <a name="not-enough-quota-to-process-this-command"></a>"Não há cota suficiente para processar este comando"

Esse erro pode significar uma das várias coisas:

- O Launchpad pode ter usuários externos insuficientes para executar a consulta externa. Por exemplo, se você estiver executando mais de 20 consultas externas simultaneamente, e houver apenas 20 usuários padrão, uma ou mais consultas poderão falhar.

- Memória insuficiente disponível para processar a tarefa do R. Esse erro ocorre com mais frequência em um ambiente padrão, em que SQL Server pode estar usando até 70 por cento dos recursos do computador. Para obter informações sobre como modificar a configuração do servidor para dar suporte a um maior uso de recursos do R, consulte [operacionalização do código r](r/operationalizing-your-r-code.md).

## <a name="cant-find-package"></a>"Não é possível encontrar o pacote"

Se você executar o código R em SQL Server e receber essa mensagem, mas não recebeu a mensagem quando executou o mesmo código fora SQL Server, isso significa que o pacote não foi instalado no local da biblioteca padrão usado pelo SQL Server.

Esse erro pode ocorrer de várias maneiras:

- Você instalou um novo pacote no servidor, mas o acesso foi negado, então o R instalou o pacote em uma biblioteca de usuários.

- Você instalou o R Services e, em seguida, instalou outra ferramenta do R ou conjunto de bibliotecas, incluindo Microsoft R Server (autônomo), Microsoft R Client, RStudio e assim por diante.

Para determinar o local da biblioteca de pacotes do R que é usada pela instância do, abra SQL Server Management Studio (ou qualquer outra ferramenta de consulta de banco de dados), conecte-se à instância do e execute o seguinte procedimento armazenado:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Resultados de exemplo

*Mensagem(ns) STDOUT do script externo:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.SQL2016\\R_SERVICES"*

*[1] "C:/Arquivos de programas/Microsoft SQL Server/MSSQL13. Sql2016/R_SERVICES/biblioteca "*

Para resolver o problema, você deve reinstalar o pacote na biblioteca de instâncias de SQL Server.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
>[!NOTE]
>Se você tiver atualizado uma instância do SQL Server 2016 para usar a versão mais recente do Microsoft R, o local da biblioteca padrão será diferente. Para obter mais informações, consulte [usar o Sqlbindr para atualizar uma instância do R Services](install/upgrade-r-and-python.md).
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>Launchpad desligado devido a DLLs incompatíveis

Se você instalar o mecanismo de banco de dados com outros recursos, corrija o servidor e, posteriormente, adicione o recurso de Machine Learning usando a mídia original, a versão errada do Machine Learning componentes poderá ser instalada. Quando o Launchpad detecta uma incompatibilidade de versão, ele é desligado e cria um arquivo de despejo.

Para evitar esse problema, certifique-se de instalar os novos recursos no mesmo nível de patch que a instância de servidor.

**A maneira errada de atualizar:**

1. Instale o SQL Server 2016 sem o R Services.
2. Atualize SQL Server atualização cumulativa 2 2016.
3. Instale o R Services (no banco de dados) usando a mídia RTM.

**A maneira correta de atualizar:**

1. Instale o SQL Server 2016 sem o R Services.
2. Atualize SQL Server 2016 para o nível de patch desejado. Por exemplo, instale o Service Pack 1 e, em seguida, a atualização cumulativa 2.
3. Para adicionar o recurso no nível de patch correto, execute o SP1 e a instalação do CU2 novamente e, em seguida, escolha R Services (no banco de dados). 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>A barra inicial não será iniciada se a notação 8dot3 for necessária

> [!NOTE] 
> Em sistemas mais antigos, o Launchpad pode falhar ao iniciar se houver um requisito de notação 8dot3. Esse requisito foi removido em versões posteriores. SQL Server os clientes do 2016 R Services devem instalar um dos seguintes:
> * SQL Server 2016 SP1 e CU1: [Atualização cumulativa 1 para SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, atualização cumulativa 3 e este [hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), que está disponível sob demanda.

Para compatibilidade com R, SQL Server 2016 R Services (no banco de dados) exigia a unidade em que o recurso está instalado para dar suporte à criação de nomes de arquivo curtos usando a *notação 8dot3*. Um nome de arquivo 8,3 também é chamado de *nome de arquivo curto*e é usado para compatibilidade com versões anteriores do Microsoft Windows ou como uma alternativa para nomes de arquivo longos.

Se o volume em que você está instalando o R não oferecer suporte a nomes de arquivo curtos, os processos que iniciam R do SQL Server talvez não possam localizar o executável correto e a barra inicial não será iniciada.

Como alternativa, você pode habilitar a notação 8dot3 no volume em que SQL Server está instalado e onde o R Services está instalado. Em seguida, será necessário fornecer o nome curto para o diretório de trabalho no arquivo de configuração do R Services.

1. Para habilitar a notação 8dot3, execute o utilitário fsutil com o argumento *8dot3name* , conforme descrito aqui: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Depois que a notação 8dot3 estiver habilitada, abra o arquivo RLauncher. config e observe `WORKING_DIRECTORY`a propriedade de. Para obter informações sobre como encontrar esse arquivo, consulte [coleta de dados para solução de problemas de Machine Learning](data-collection-ml-troubleshooting-process.md).

3. Use o utilitário fsutil com o argumento *File* para especificar um caminho de arquivo curto para a pasta especificada em WORKING_DIRECTORY.

4. Edite o arquivo de configuração para especificar o mesmo diretório de trabalho que você inseriu na propriedade WORKING_DIRECTORY. Como alternativa, você pode especificar um diretório de trabalho diferente e escolher um caminho existente que já seja compatível com a notação 8dot3.
::: moniker-end

## <a name="next-steps"></a>Próximas etapas

[Solução de problemas Serviços de Machine Learning e questões conhecidas](machine-learning-troubleshooting-faq.md)

[Coleta de dados para solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

[Perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexões do Database Engine](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
