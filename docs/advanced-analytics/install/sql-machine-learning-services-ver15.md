---
title: Diferenças no SQL Server de 2019 - serviços de aprendizado de máquina do SQL Server
description: Saiba o que há de novo para extensões de aprendizado de máquina R e Python SQL Server na versão de visualização do SQL Server de 2019.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/08/2018
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d0b91668141b73b8ce5e4708cb403b7cc09b4ce9
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432829"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>Diferenças na instalação de serviços do SQL Server Machine Learning no SQL Server 2019  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

No Windows, a instalação do SQL Server de 2019 altera o mecanismo de isolamento para processos externos. Essa alteração substitui as contas de local de trabalho com [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), uma tecnologia de isolamento para aplicativos cliente executados no Windows. 

Não há nenhum item de ação específica para o administrador como resultado da modificação. Em um servidor novo ou atualizado, todos os scripts externos e código executado a partir [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) seguem o modelo de isolamento de novo automaticamente. Isso se aplica a R, Python e a extensão da linguagem Java novos introduzidos no SQL Server de 2019.

As principais diferenças nesta versão resumida, são:

+ Contas de usuário local sob **grupo de usuários restritos de SQL (SQLRUserGroup)** não são criados ou usados para executar processos externos. AppContainers substituí-los.
+ **SQLRUserGroup** associação tiver mudado. Em vez de várias contas de usuário local, a associação consiste de apenas a conta de serviço do Launchpad do SQL Server. Processos de R, Python e Java agora executam sob a identidade do serviço Launchpad, isolada por meio de AppContainers.

Embora o modelo de isolamento foi alterado, os parâmetros de linha de comando e o Assistente de instalação permanecem o mesmo no SQL Server de 2019. Para obter ajuda com a instalação, consulte [instalar o SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md).

## <a name="about-appcontainer-isolation"></a>Sobre o isolamento do AppContainer

Em versões anteriores, **SQLRUserGroup** continha um pool do Windows contas de usuário locais (MSSQLSERVER00 MSSQLSERVER20) usado para isolar e execução de processos externos. Quando um processo externo era necessária, o serviço de Launchpad do SQL Server seria levar em conta uma disponível e usá-lo para executar um processo. 

No SQL Server de 2019, a instalação não cria mais contas de trabalho local. Em vez disso, o isolamento é obtido por meio [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). Em tempo de execução quando o script inserido ou o código é detectado em uma consulta ou procedimento armazenado, SQL Server chama o Launchpad com uma solicitação para um iniciador específicas da extensão. Launchpad invoca o ambiente de tempo de execução apropriado em um processo sob sua identidade e cria uma instância de um AppContainer para contê-lo. Essa alteração é benéfica porque o gerenciamento de conta e senha local não é mais necessário. Além disso, em instalações em que as contas de usuário local são proibidas, eliminação da dependência de conta de usuário local significa que agora você pode usar esse recurso.

Conforme implementado pelo SQL Server, AppContainers são um mecanismo interno. Embora você não ver evidências físicas de AppContainers no Monitor de processo, você pode encontrá-los nas regras de firewall de saída criadas pela instalação para impedir que processos façam chamadas de rede.

## <a name="firewall-rules-created-by-setup"></a>Regras de firewall criadas pela instalação do

Por padrão, o SQL Server desabilita conexões de saída com a criação de regras de firewall. No passado, essas regras foram com base em contas de usuário local, em que a instalação criou uma regra de saída para **SQLRUserGroup** que recebem acesso à rede a seus membros (cada conta de trabalho foi listada como um princípio local sujeitos ao rule_. 

Como parte da mudança para AppContainers, há novas regras de firewall com base em SIDs AppContainer: um para cada uma as 20 AppContainers criado pela instalação do SQL Server. Convenções de nomenclatura para o nome da regra de firewall são **bloquear o acesso de rede para AppContainer 00 na instância MSSQLSERVER do SQL Server**, onde 00 é o número de AppContainer (00 – 20 por padrão), e MSSQLSERVER é o nome do SQL Instância do servidor. 

> [!Note]
> Se as chamadas de rede são necessárias, você pode desabilitar as regras de saída no Firewall do Windows.

## <a name="program-file-permissions"></a>Permissões de arquivo do programa

Assim como acontece com versões anteriores, o **SQLRUserGroup** continua a fornecer a leitura e permissões de execução em arquivos executáveis do SQL Server **Binn**, **R_SERVICES**e  **PYTHON_SERVICES** diretórios. Nesta versão, o único membro da **SQLRUserGroup** é a conta de serviço do Launchpad do SQL Server.  Quando o serviço Launchpad inicia um ambiente de execução de R, Python ou Java, o processo é executado como serviço LaunchPad.

## <a name="implied-authentication"></a>Autenticação implícita

Como antes, a configuração adicional é ainda necessária para *autenticação implícita* nos casos em que o script ou código tem para se conectar novamente ao SQL Server usando autenticação confiável para recuperar dados ou recursos. A configuração adicional envolve a criação de um logon de banco de dados para **SQLRUserGroup**, cujo membro único agora é a única conta de serviço do Launchpad do SQL Server em vez de várias contas de trabalho. Para obter mais informações sobre essa tarefa, consulte [adicionar SQLRUserGroup como um usuário de banco de dados](../security/add-sqlrusergroup-to-database.md).


## <a name="symbolic-link-created-by-setup"></a>Link simbólico criado pela instalação do

Um link simbólico é criado para o padrão atual **R_SERVICES** e **PYTHON_SERIVCES** como parte da instalação do SQL Server. Se você não quiser criar esse link, uma alternativa é conceder permissão de leitura de 'todos os pacotes de aplicativos' para a hierarquia que levam à pasta.


## <a name="see-also"></a>Confira também

+ [Instalar serviços no Windows de aprendizado de máquina do SQL Server](sql-machine-learning-services-windows-install.md)

+ [Instalar 2019 serviços Machine Learning do SQL Server no Linux](../../linux/sql-server-linux-setup-machine-learning.md)
