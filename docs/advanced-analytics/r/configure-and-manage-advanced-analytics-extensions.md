---
title: Configuração avançada para serviços do SQL Server Machine Learning | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8384773f6db4c0ced2fc68e52cd78100c98c52fd
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393569"
---
# <a name="advanced-configuration-options-for-sql-server-machine-learning-services"></a>Opções de configuração avançadas para serviços do SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve as alterações feitas após a instalação, para modificar a configuração de tempo de execução do script externo e outros serviços associados com o aprendizado de máquina no SQL Server.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 serviços de Machine Learning

##  <a name="bkmk_Provisioning"></a> Contas de usuário adicional para a máquina aprendizado

Processos de script externo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executados no contexto de contas de usuário local de baixo privilégio. Esses processos em execução em contas individuais de baixo privilégio tem os seguintes benefícios:

+ Reduz os privilégios dos processos de tempo de execução de script externo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador
+ Fornece isolamento entre as sessões de um tempo de execução externo, como R ou Python.

Como parte da instalação, um novo Windows *pool de contas de usuário* é criado que contém as contas de usuário local necessárias para processos em execução em tempo de execução externos, como R ou Python. Você pode modificar o número de usuários conforme necessário para dar suporte a tarefas de aprendizado de máquina. 

Além disso, o administrador de banco de dados deve dar a esse grupo permissão para se conectar a qualquer instância em que o aprendizado de máquina foi habilitado. Para obter mais informações, consulte [modificar o pool de conta de usuário para serviços do SQL Server Machine Learning](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

A recursos confidenciais protext sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode definir uma lista de controle de acesso (ACL) para esse grupo. Especificando que o grupo negado acesso a recursos, você pode impedir o acesso por processos externos, como os tempos de execução de R ou Python.

+ O pool de conta de usuário está vinculado a uma instância específica. Um pool separado de contas de trabalho é necessário para cada instância no qual o machine learning foi habilitado. Contas não podem ser compartilhadas entre instâncias.

+ Nomes de conta de usuário no pool estão no formato SQLInstanceName*nn*. Por exemplo, se você estiver usando a instância padrão para aprendizado de máquina, o pool de contas de usuário dá suporte a nomes de conta como MSSQLSERVER01, MSSQLSERVER02 e assim por diante.

+ O tamanho do pool de conta de usuário é estático e o valor padrão é 20. O número de sessões de tempo de execução externos que podem ser iniciadas simultaneamente é limitado pelo tamanho desse pool de conta de usuário. Para alterar esse limite, um administrador deve usar o SQL Server Configuration Manager.

Para obter mais informações sobre como fazer alterações para o pool de conta de usuário, consulte [modificar o pool de conta de usuário para serviços do SQL Server Machine Learning](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

##  <a name="bkmk_ManagingMemory"></a> Gerenciar a memória usada pelos processos de script externo

Por padrão, os tempos de execução do script externo para o machine learning são limitados a não mais de 20% da memória total do computador. Ele depende do seu sistema, mas em geral, você pode encontrar esse limite inadequado para tarefas de aprendizado de máquina graves, como um modelo de treinamento ou para prever em várias linhas de dados. 

Para oferecer suporte ao aprendizado de máquina, um administrador pode aumentar esse limite. Quando você fizer isso, talvez seja necessário reduzir a quantidade de memória reservada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para outros serviços. Você também deve considerar usando o Resource Governor para definir um pool de recursos externos ou pools, para que você pode alocar pools de recursos específicos para trabalhos de R ou Python.

Para obter mais informações, consulte [governança de recursos para o aprendizado de máquina](../../advanced-analytics/r/resource-governance-for-r-services.md).


## <a name="bkmk_Launchpad"></a>Modificar a conta de serviço do Launchpad

Um separado [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço é criado para cada instância em que você configurou os serviços de machine learning.

Por padrão, o Launchpad é configurado para ser executado usando a conta, NT Service\MSSQLLaunchpad, que é configurada com todas as permissões necessárias para executar scripts R. No entanto, se você alterar essa conta, o Launchpad não poderá para iniciar ou acessar a instância do SQL Server em que os scripts externos devem ser executados.

Se você modificar a conta de serviço, certifique-se de usar o aplicativo **Política de segurança local** e atualizar as permissões em cada conta de serviço para incluir essas permissões:

+ Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)
+ Ignorar verificação completa (SeChangeNotifyPrivilege)
+ Fazer logon como um serviço (SeServiceLogonRight)
+ Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)

Para obter mais informações sobre as permissões necessárias para executar serviços SQL Server, consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

##  <a name="bkmk_ChangingConfig"></a> Alterar as opções de serviço avançadas

Em versões anteriores do SQL Server 2016 R Services, você pode alterar algumas propriedades do serviço, editando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] arquivo de configuração. 

No entanto, esse arquivo não é usado para alterar as configurações. É recomendável que você use o SQL Server Configuration Manager para alterações de efeito a configuração de serviço, como a conta de serviço e o número de usuários.

**Para modificar a configuração de barra inicial**

1. Abra [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md). 
2. Launchpad do SQL Server com o botão direito e selecione **propriedades**.

    + Para alterar a conta de serviço, clique o **fazer logon** guia.

    + Para aumentar o número de usuários, clique o **avançado** guia.


**Para modificar as configurações de depuração**

Algumas propriedades só podem ser alteradas usando o arquivo de configuração da barra inicial, que pode ser útil em casos limitados, como a depuração. O arquivo de configuração é criado durante a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalação e por padrão é salvo como um arquivo de texto sem formatação no seguinte local: `<instance path>\binn\rlauncher.config`

Você deve ser um administrador no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer alterações nesse arquivo. Se você editar o arquivo, é recomendável que você faça uma cópia de backup antes de salvar as alterações.

A tabela a seguir lista as configurações avançadas para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], com os valores permitidos. 

|**Nome da configuração**|**Tipo**|**Descrição**|
|----|----|----|
|TRABALHO\_LIMPEZA\_ON\_SAIR|Integer |Isso é uma configuração interna apenas, não altere esse valor. </br></br>Especifica se a pasta de trabalho temporária criada para cada sessão de tempo de execução externos deve ser limpos após o término da sessão. Essa configuração é útil para depuração. </br></br>Valores com suporte são **0** (desativado) ou **1** (habilitado). </br></br>O padrão é 1, arquivos de log do significado são removidos ao sair.|
|RASTREAMENTO\_NÍVEL|Integer |Configura o nível de detalhamento do rastreamento de MSSQLLAUNCHPAD para fins de depuração. Isso afeta os arquivos de rastreamento no caminho especificado pela configuração LOG_DIRECTORY. </br></br>Valores com suporte são: **1** (erro), **2** (desempenho), **3** (aviso) **4** (informações). </br></br>O padrão é 1, que significa que somente os avisos de saída.|

Todas as configurações assumem a forma de um par chave-valor, com cada configuração em uma linha separada. Por exemplo, para alterar o nível de rastreamento, você adicionaria a linha `Default: TRACE_LEVEL=4`.

## <a name="see-also"></a>Consulte também

[Considerações sobre segurança](security-considerations-for-the-r-runtime-in-sql-server.md)
