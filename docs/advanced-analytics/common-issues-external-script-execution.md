---
title: Problemas comuns com o serviço Launchpad e execução de script externo - serviços do SQL Server Machine Learning
ms.prod: sql
ms.technology: ''
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a6943a850a2955a36723d14c0226bd5c503f23ec
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140206"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Problemas comuns com o serviço Launchpad e execução de script externo no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 Serviço do Launchpad confiável do SQL Server dá suporte à execução de script externo para R e Python. No SQL Server 2016 R Services, o SP1 fornece o serviço. SQL Server 2017 inclui o serviço Launchpad como parte da instalação inicial.

Vários problemas podem impedir que a barra inicial de início, incluindo problemas de configuração ou alterações ou ausentes de protocolos de rede. Este artigo fornece orientação para a solução para muitos problemas. Para qualquer sentíamos, você pode postar perguntas para o [Fórum do Machine Learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR).

## <a name="determine-whether-launchpad-is-running"></a>Determinar se o Launchpad estiver em execução

1. Abra o **Services** painel (Services. msc). Ou, na linha de comando, digite **SQLServerManager13.msc** ou **SQLServerManager14.msc** para abrir [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Tome nota da conta de serviço Launchpad está sendo executado. Cada instância em que o R ou Python está habilitado deve ter sua própria instância do serviço Launchpad. Por exemplo, o serviço para uma instância nomeada pode ser algo como _MSSQLLaunchpad$ InstanceName_.

3. Se o serviço for interrompido, reinicie-o. Na reinicialização, se houver algum problema com a configuração, uma mensagem é publicada no log de eventos do sistema e o serviço for interrompido novamente. Verifique o log de eventos do sistema para obter detalhes sobre por que o serviço foi interrompido.

4. Examine o conteúdo do RSetup.log e certifique-se de que não há nenhum erro na instalação. Por exemplo, a mensagem *sendo encerrada com o código 0* indica a falha do serviço para iniciar.

5. Para procurar outros erros, examine o conteúdo de rlauncher. log.

## <a name="check-the-launchpad-service-account"></a>Verifique a conta de serviço do Launchpad

A conta de serviço padrão pode ser "NT Service\$SQL2016" ou "NT Service\$SQL2017". A parte final pode variar, dependendo do seu nome de instância do SQL.

O serviço Launchpad (Launchpad.exe) é executado usando uma conta de serviço de baixo privilégio. No entanto, para iniciar o R e Python e se comunicar com a instância de banco de dados, a conta de serviço do Launchpad exige os seguintes direitos de usuário:

- Fazer logon como um serviço (SeServiceLogonRight)
- Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)
- Ignorar verificação completa (SeChangeNotifyPrivilege)
- Ajustar quotas de memória para um processo (SeIncreaseQuotaPrivilege)

Para obter informações sobre esses direitos de usuário, consulte a seção "direitos e privilégios de Windows" em [Windows configurar contas de serviço e permissões](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Se você estiver familiarizado com o uso da ferramenta de plataforma de diagnóstico de suporte (SDP) para o diagnóstico do SQL Server, você pode usar SDP examine o arquivo de saída com o nome MachineName_UserRights.txt.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>Grupo de usuários para o Launchpad não pode fazer logon localmente

Durante a instalação dos serviços de aprendizado de máquina, o SQL Server cria o grupo de usuários do Windows **SQLRUserGroup** e, em seguida, provisiona a ele todos os direitos necessários para o Launchpad conectar-se ao SQL Server e executar trabalhos de script externo. Se esse grupo de usuários estiver habilitado, ele também é usado para executar scripts Python.

No entanto, em organizações onde as políticas de segurança mais restritivas são aplicadas, os direitos necessários para este grupo podem ter sido manualmente removidos ou eles podem ser revogados automaticamente pela política. Se os direitos de tem sido removidos, Launchpad não poderá se conectar ao SQL Server e do SQL Server não é possível chamar o tempo de execução externo.

Para corrigir o problema, garanta que o **SQLRUserGroup** tenha o direito de sistema **Permitir logon local**.

Para obter mais informações, consulte [Windows configurar contas de serviço e permissões](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

## <a name="permissions-to-run-external-scripts"></a>Permissões para executar scripts externos

Mesmo se o Launchpad estiver configurado corretamente, ele retornará um erro se o usuário não tem permissão para executar scripts R ou Python.

Se você instalou o SQL Server como um administrador de banco de dados ou se você for um proprietário de banco de dados, você automaticamente recebe essa permissão. No entanto, outros usuários geralmente têm mais permissões limitadas. Se eles tentarem executar um script R, eles obtêm um erro de barra inicial.

Para corrigir o problema, no SQL Server Management Studio, um administrador de segurança pode modificar o logon SQL ou a conta de usuário do Windows, executando o script a seguir:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Para obter mais informações, consulte [GRANT (Transact-SQL](../t-sql/statements/grant-transact-sql.md).

## <a name="common-launchpad-errors"></a>Erros comuns da barra inicial

Esta seção lista as mensagens de erro mais comuns que retorna da barra inicial.

## <a name="unable-to-launch-runtime-for-r-script"></a>"Não é possível iniciar o tempo de execução para o script R"

Se o grupo do Windows para usuários de R (também é usado para o Python) não pode fazer logon para a instância que executa o R Services, você poderá ver os seguintes erros:

- Erros gerados ao tentar executar scripts do R:

    * *Não é possível iniciar o tempo de execução para o script do “R”. Verifique a configuração do tempo de execução do script do R.*

    * *Erro de script externo. Não é possível iniciar o tempo de execução.*

- Erros gerados pelo [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] serviço:

    * *Falha ao inicializar o inicializador RLauncher.dll*

    * *Nenhuma dll do inicializador foi registrada!*

    * *Logs de segurança indicam que a conta NT SERVICE não pôde fazer logon*

Para obter informações sobre como conceder as permissões necessárias esse grupo de usuários, consulte [instalar o SQL Server 2016 R Services](install/sql-r-services-windows-install.md).

> [!NOTE]
> Essa limitação não se aplicará se você usar logons SQL para executar scripts do R em uma estação de trabalho remota.

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"Falha de logon: o usuário não recebeu o tipo de logon solicitado"

Por padrão, [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] usa a seguinte conta na inicialização: `NT Service\MSSQLLaunchpad`. A conta é configurada por [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] instalação ter todas as permissões necessárias.

Se você atribuir uma conta diferente ao Launchpad ou a direita for removida por uma política no computador do SQL Server, a conta pode não ter as permissões necessárias, e você poderá ver esse erro:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Falha de logon: o usuário não recebeu o tipo de logon solicitado neste computador.*

Para conceder as permissões necessárias para a nova conta de serviço, use o aplicativo de diretiva de segurança Local e atualizar as permissões na conta para incluir as seguintes permissões:

+ Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
+ Ignorar verificação completa (SeChangeNotifyPrivilege)
+ Fazer logon como um serviço (SeServiceLogonRight)
+ Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"Não é possível se comunicar com o serviço Launchpad"

Se você tiver instalado e habilitado, em seguida, aprendizado de máquina, mas você receber esse erro ao tentar executar um script de R ou Python, o serviço Launchpad da instância pode ter parado em execução.

1. Em um prompt de comando do Windows, abra o SQL Server Configuration Manager. Para obter mais informações, consulte [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Launchpad do SQL Server para a instância e, em seguida, selecione **propriedades**.

3. Selecione o **serviço** guia e, em seguida, verifique se que o serviço está em execução. Se não estiver, altere a **modo de início** para **automática**e, em seguida, selecione **aplicar**.

4. Reiniciar o serviço geralmente corrige o problema para que possam ser executados scripts de aprendizado de máquina. Se a reinicialização não corrigir o problema, observe o caminho e argumentos de **caminho binário** propriedade e faça o seguinte:

    a. Examine o arquivo. config do iniciador e certifique-se de que o diretório de trabalho é válido.

    b. Certifique-se de que o grupo do Windows que é usado pelo Launchpad pode se conectar à instância do SQL Server.

    c. Se você alterar qualquer uma das propriedades do serviço, reinicie o serviço Launchpad.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"Falha na criação de erro fatal de tmpFile"

Nesse cenário, você instalou com êxito os recursos de aprendizado de máquina e Launchpad estiver em execução. Você tenta executar um código de R ou Python simples, mas Launchpad falhará com um erro semelhante ao seguinte: 

>*Não é possível se comunicar com o tempo de execução de script R. Verifique se os requisitos de tempo de execução de R.*

Ao mesmo tempo, o tempo de execução do script externo grava a mensagem a seguir como parte da mensagem STDERR: 

>*Erro fatal: criação de tmpfile falhou.*

Esse erro indica que a conta que o Launchpad está tentando usar não tem permissão para fazer logon no banco de dados. Essa situação pode acontecer quando as políticas de segurança estrita são implementadas. Para determinar se esse for o caso, examine os logs do SQL Server e verifique para ver se a conta MSSQLSERVER01 foi negada no logon. As mesmas informações são fornecidas nos logs que são específicos ao R\_serviços ou PYTHON\_serviços. Procure ExtLaunchError.log.

Por padrão, 20 contas são configuradas e associadas com o processo de Launchpad.exe, com os nomes MSSQLSERVER01 por meio de MSSQLSERVER20. Se você fizer uso intenso de R ou Python, você pode aumentar o número de contas.

Para resolver o problema, verifique se o grupo *permitir logon localmente* permissões para a instância local em que os recursos de aprendizado de máquina foi instalados e habilitados. Em alguns ambientes, esse nível de permissão pode exigir que uma exceção de GPO do administrador de rede.

## <a name="not-enough-quota-to-process-this-command"></a>"Não há cota suficiente para processar este comando"

Esse erro pode significar várias coisas:

- Barra inicial pode ter usuários externos insuficientes para executar a consulta externa. Por exemplo, se você estiver executando mais de 20 consultas externas simultaneamente, e existem apenas 20 usuários padrão, uma ou mais consultas poderá falhar.

- Não há memória suficiente está disponível para processar a tarefa de R. Esse erro geralmente ocorre em um ambiente padrão, em que os do SQL Server pode estar usando até 70% dos recursos do computador. Para obter informações sobre como modificar a configuração do servidor para dar suporte à maior uso de recursos por R, consulte [operacionalização do código R](r/operationalizing-your-r-code.md).

## <a name="cant-find-package"></a>"Não é possível localizar o pacote"

Se você executa o código R no SQL Server e receber essa mensagem, mas não recebeu a mensagem quando você executou o mesmo código fora do SQL Server, isso significa que o pacote não foi instalado para o local da biblioteca padrão usado pelo SQL Server.

Esse erro pode acontecer de várias maneiras:

- Você instalou um novo pacote no servidor, mas o acesso foi negado, portanto, o R instalado o pacote em uma biblioteca do usuário.

- Você instalou o R Services e, em seguida, instalou outra ferramenta de R ou conjunto de bibliotecas, incluindo Microsoft R Server (autônomo), Microsoft R Client, RStudio e assim por diante.

Para determinar o local da biblioteca de pacote do R que é usado pela instância, abra o SQL Server Management Studio (ou qualquer outra ferramenta de consulta de banco de dados), conecte-se à instância e, em seguida, execute o seguinte procedimento armazenado:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Resultados do exemplo

*Mensagem(ns) STDOUT do script externo:*

*[1] "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.SQL2016\\R_SERVICES"*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

Para resolver o problema, reinstale o pacote para a biblioteca de instância do SQL Server.

>[!NOTE]
>Se você tiver atualizado uma instância do SQL Server 2016 para usar a versão mais recente do Microsoft R, o local da biblioteca padrão é diferente. Para obter mais informações, consulte [usar SqlBindR para atualizar uma instância do R Services](install/upgrade-r-and-python.md).

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>Barra inicial é desligado devido a DLLs incompatíveis

Se você instala o mecanismo de banco de dados com outros recursos, o servidor de patch e, em seguida, adicione o recurso de aprendizado de máquina mais tarde usando a mídia original, a versão incorreta dos componentes do Machine Learning pode ser instalada. Quando o Launchpad detecta uma incompatibilidade de versão, ele é desligado e cria um arquivo de despejo.

Para evitar esse problema, certifique-se de instalar os novos recursos no mesmo nível de patch como a instância do servidor.

**A maneira errada para atualizar:**

1. Instale o SQL Server 2016 sem os serviços de R.
2. Atualize a atualização cumulativa do SQL Server 2016 2.
3. Instale o R Services (no banco de dados) usando a mídia do RTM.

**A maneira correta de atualizar:**

1. Instale o SQL Server 2016 sem os serviços de R.
2. Atualize o SQL Server 2016 para o nível de patch desejado. Por exemplo, instale o Service Pack 1 e, em seguida, a atualização cumulativa 2.
3. Para adicionar o recurso no nível do patch correto, execute novamente a instalação do SP1 e CU2 e, em seguida, escolha R Services (no banco de dados). 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>Launchpad não pode ser iniciado se a notação 8dot3 é necessária

> [!NOTE] 
> Em sistemas mais antigos, o Launchpad pode falhar ao iniciar se há um requisito de notação 8dot3. Esse requisito foi removido em versões posteriores. Os clientes do SQL Server 2016 R Services devem instalar um dos seguintes:
> * SQL Server 2016 SP1 e CU1: [Atualização cumulativa 1 para SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, atualização cumulativa 3 e isso [hotfix](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), que está disponível sob demanda.

Para compatibilidade com R, o SQL Server 2016 R Services (no banco de dados) necessária a unidade onde o recurso é instalado para dar suporte a criação de nomes de arquivos curtos usando *notação 8dot3*. Um nome de 8.3 arquivo também é chamado de um *nome de arquivo curto*, e ele é usado para compatibilidade com versões anteriores do Microsoft Windows ou como uma alternativa para nomes de arquivo longos.

Se o volume em que você está instalando o R não oferece suporte a nomes de arquivos curtos, os processos que iniciam o R do SQL Server talvez não consiga localizar o executável correto e Launchpad não será iniciado.

Como alternativa, você pode habilitar a notação 8dot3 no volume em que o SQL Server está instalado e em que o R Services está instalado. Em seguida, será necessário fornecer o nome curto para o diretório de trabalho no arquivo de configuração do R Services.

1. Para habilitar a notação 8dot3, execute o utilitário fsutil com o *8dot3name* argumento conforme descrito aqui: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Depois que a notação 8dot3 estiver habilitada, abra o arquivo Rlauncher config e observe a propriedade de `WORKING_DIRECTORY`. Para obter informações sobre como encontrar esse arquivo, consulte [coleta de dados para a solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md).

3. Use o utilitário fsutil com o *arquivo* argumento para especificar um caminho de arquivo curto para a pasta que é especificada em WORKING_DIRECTORY.

4. Edite o arquivo de configuração para especificar o mesmo diretório de trabalho que você inseriu na propriedade de WORKING_DIRECTORY. Como alternativa, você pode especificar um diretório de trabalho diferentes e escolha um caminho existente que já é compatível com a notação 8dot3.


## <a name="next-steps"></a>Próximas etapas

[Problemas conhecidos e solução de problemas de serviços de aprendizado de máquina](machine-learning-troubleshooting-faq.md)

[Coleta de dados para solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

[Perguntas frequentes sobre atualização e instalação](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexões do mecanismo de banco de dados](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
