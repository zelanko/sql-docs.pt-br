---
title: "Opções de configuração para serviços de aprendizado de máquina avançada | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 369c630e249d7775e67508fc9b00e94447182012
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="advanced-configuration-options-for-machine-learning-services"></a>Opções de configuração avançadas para serviços de aprendizado de máquina

Este artigo descreve as alterações feitas após a instalação, para modificar a configuração de tempo de execução do script externo e outros serviços associados ao aprendizado de máquina no SQL Server.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 serviços de aprendizado de máquina

##  <a name="bkmk_Provisioning"></a>Contas de usuário adicional provisionar máquina aprendizado

Script externo processa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executado no contexto de contas de usuário local de baixo privilégio. Esses processos em execução em contas individuais de baixo privilégio tem os seguintes benefícios:

+ Reduz os privilégios dos processos de tempo de execução do script externo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador
+ Fornece isolamento entre as sessões de um tempo de execução externo, como R ou Python.

Como parte da instalação, uma nova janela de *pool de conta de usuário* é criado que contém as contas de usuário local necessárias para executar processos de tempo de execução externos, como R ou Python. Você pode modificar o número de usuários, conforme necessário para dar suporte a tarefas de aprendizado de máquina. 

Além disso, o administrador de banco de dados deve atribuir a esse grupo permissão para se conectar a qualquer instância em que o aprendizado de máquina tiver sido habilitado. Para obter mais informações, consulte [modificar o pool de conta de usuário para serviços de aprendizado de máquina do SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

A recursos confidenciais protext no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode definir uma lista de controle de acesso (ACL) para esse grupo. Especificando que o grupo negado acesso a recursos, você pode impedir o acesso por processos externos, como os tempos de execução de R ou Python.

+ O pool de conta de usuário está vinculado a uma instância específica. Um pool separado das contas de trabalho é necessário para cada instância no qual o machine learning foi habilitado. Contas não podem ser compartilhadas entre instâncias.

+ Nomes de conta de usuário no pool estão no formato SQLInstanceName*nn*. Por exemplo, se você estiver usando a instância padrão do aprendizado de máquina, o pool de contas de usuário oferece suporte a nomes de conta como MSSQLSERVER01, MSSQLSERVER02 e assim por diante.

+ O tamanho do pool de conta de usuário é estático e o valor padrão é 20. O número de sessões de tempo de execução externos que podem ser iniciadas simultaneamente é limitado pelo tamanho do pool de conta de usuário. Para alterar esse limite, um administrador deve usar o SQL Server Configuration Manager.

Para obter mais informações sobre como fazer alterações para o pool de conta de usuário, consulte [modificar o pool de conta de usuário para serviços de aprendizado de máquina do SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

##  <a name="bkmk_ManagingMemory"></a>Gerenciar a memória usada pelos processos de script externo

Por padrão, os tempos de execução do script externo para o aprendizado de máquina são limitados a não mais de 20% da memória total do computador. Depende do seu sistema, mas em geral, você pode encontrar esse limite inadequada para tarefas de aprendizado de máquina sério, como um modelo de treinamento ou previsão em várias linhas de dados. 

Para oferecer suporte de aprendizado de máquina, um administrador pode aumentar esse limite. Quando você fizer isso, talvez seja necessário reduzir a quantidade de memória reservada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para outros serviços. Você também deve considerar usando o administrador de recursos para definir um pool de recursos externos ou pools de forma que você pode alocar pools de recursos específicos para trabalhos de R ou Python.

Para obter mais informações, consulte [governança de recursos para o aprendizado de máquina](../../advanced-analytics/r/resource-governance-for-r-services.md).


## <a name="bkmk_Launchpad"></a>Modificar a conta de serviço barra inicial

Um separado [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço é criado para cada instância em que você configurou a serviços de aprendizado de máquina.

Por padrão, o Launchpad é configurado para ser executado usando a conta, NT Service\MSSQLLaunchpad, que é configurada com todas as permissões necessárias para executar scripts R. No entanto, se você alterar essa conta, a barra inicial não poderá iniciar ou acessar a instância do SQL Server em que os scripts externos devem ser executados.

Se você modificar a conta de serviço, certifique-se de usar o aplicativo **Política de segurança local** e atualizar as permissões em cada conta de serviço para incluir essas permissões:

+ Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
+ Ignorar verificação completa (SeChangeNotifyPrivilege)
+ Fazer logon como um serviço (SeServiceLogonRight)
+ Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

Para obter mais informações sobre as permissões necessárias para executar serviços SQL Server, consulte [Configurar contas de serviço e permissões do Windows](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

##  <a name="bkmk_ChangingConfig"></a>Alterar as opções de serviço avançadas

Em versões anteriores do SQL Server 2016 R Services, você pode alterar algumas propriedades do serviço, editando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] arquivo de configuração. 

No entanto, esse arquivo não é usado para alterar as configurações. É recomendável que você use o SQL Server Configuration Manager para alterações de efeito a configuração do serviço, como a conta de serviço e o número de usuários.

**Para modificar a configuração da barra inicial**

1. Abra [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md). 
2. Launchpad do SQL Server e selecione **propriedades**.

    + Para alterar a conta de serviço, clique o **logon** guia.

    + Para aumentar o número de usuários, clique o **avançado** guia.


**Para modificar as configurações de depuração**

Algumas propriedades só podem ser alteradas usando o arquivo de configuração da barra inicial, que pode ser útil em casos limitados, como depuração. O arquivo de configuração é criado durante a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalação e por padrão é salvo como um arquivo de texto sem formatação no seguinte local:`<instance path>\binn\rlauncher.config`

Você deve ser um administrador no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer alterações nesse arquivo. Se você editar o arquivo, é recomendável que você faça uma cópia de backup antes de salvar as alterações.

A tabela a seguir lista as configurações avançadas para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], com os valores permitidos. 

|**Nome da configuração**|**Tipo**|**Description**|
|----|----|----|
|TRABALHO\_LIMPEZA\_ON\_SAIR|Integer |Esta é uma configuração interna apenas, não altere esse valor. </br></br>Especifica se a pasta de trabalho temporária criada para cada sessão de tempo de execução externa deve ser limpa depois que a sessão seja concluída. Essa configuração é útil para depuração. </br></br>Valores com suporte são **0** (desativado) ou **1** (habilitado). </br></br>O padrão é 1, os arquivos de log significado são removidos ao sair.|
|RASTREAMENTO\_NÍVEL|Integer |Configura o nível de detalhamento do rastreamento de MSSQLLAUNCHPAD para fins de depuração. Isso afeta os arquivos de rastreamento no caminho especificado pela configuração LOG_DIRECTORY. </br></br>Valores com suporte são: **1** (erro) **2** (desempenho), **3** (aviso), **4** (informações). </br></br>O padrão é 1, que significa que somente os avisos de saída.|

Todas as configurações assumem a forma de um par chave-valor, com cada configuração em uma linha separada. Por exemplo, para alterar o nível de rastreamento, você deve adicionar a linha `Default: TRACE_LEVEL=4`.

## <a name="see-also"></a>Consulte também

[Considerações sobre segurança](security-considerations-for-the-r-runtime-in-sql-server.md)
