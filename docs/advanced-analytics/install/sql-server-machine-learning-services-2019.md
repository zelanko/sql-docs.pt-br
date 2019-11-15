---
title: Alterações de isolamento para Windows
description: Este artigo descreve as alterações no mecanismo de isolamento dos Serviços de Machine Learning no SQL Server 2019 no Windows. Essas alterações afetam o SQLRUserGroup, as regras de firewall, a permissão de arquivo e a autenticação implícita.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4fae460e78682263c604d8e1e86ca40b7b62df97
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69531045"
---
# <a name="sql-server-2019-on-windows-isolation-changes-for-machine-learning-services"></a>SQL Server 2019 no Windows: Alterações de isolamento nos Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve as alterações no mecanismo de isolamento dos Serviços de Machine Learning no SQL Server 2019 no Windows. Essas alterações afetam o **SQLRUserGroup**, as regras de firewall, a permissão de arquivo e a autenticação implícita.

Para obter mais informações, confira como instalar os [Serviços de Machine Learning do SQL Server no Windows](sql-machine-learning-services-windows-install.md).

## <a name="changes-to-isolation-mechanism"></a>Alterações no mecanismo de isolamento

No Windows, a instalação do SQL Server 2019 altera o mecanismo de isolamento para processos externos. Essa alteração substitui as contas de trabalho locais por [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), uma tecnologia de isolamento para aplicativos cliente em execução no Windows. 

Não há itens de ação específicos para o administrador como resultado da modificação. Em um servidor novo ou atualizado, todos os scripts externos e códigos executados de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) seguem o novo modelo de isolamento automaticamente. 

Resumidamente, as principais diferenças nesta versão são:

+ As contas de usuário local no **SQLRUserGroup (grupo de usuários com restrições do SQL)** não são mais criadas ou usadas para executar processos externos. O AppContainers as substitui.
+ A associação do **SQLRUserGroup** foi alterada. Em vez de várias contas de usuário local, a associação consiste apenas na conta de serviço do SQL Server Launchpad. Os processos de R e Python agora são executados sob a identidade do serviço Launchpad, isolado por meio de AppContainers.

Embora o modelo de isolamento tenha sido alterado, o assistente de instalação e os parâmetros de linha de comando permanecem os mesmos no SQL Server 2019. Para ajuda com a instalação, confira [Instalar os Serviços de Machine Learning do SQL Server](sql-machine-learning-services-windows-install.md).

## <a name="about-appcontainer-isolation"></a>Sobre o isolamento do AppContainer

Nas versões anteriores, o **SQLRUserGroup** continha um pool de contas de usuário local do Windows (MSSQLSERVER00-MSSQLSERVER20) usadas para isolar e executar processos externos. Quando um processo externo era necessário, o serviço do SQL Server Launchpad pegava uma conta disponível e a usava para executar um processo. 

No SQL Server 2019, a instalação não cria mais contas de trabalho locais. Em vez disso, o isolamento é obtido por meio de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). No tempo de execução, quando o script incorporado ou o código é detectado em um procedimento armazenado ou consulta, o SQL Server chama o Launchpad com uma solicitação para um inicializador específico da extensão. O Launchpad invoca o ambiente de runtime apropriado em um processo sob sua identidade e instancia um AppContainer para contê-lo. Essa alteração é benéfica porque o gerenciamento de conta local e de senha não é mais necessário. Além disso, em instalações em que as contas de usuário local são proibidas, a eliminação da dependência de conta de usuário local significa que agora você pode usar esse recurso.

Conforme implementado pelo SQL Server, os AppContainers são um mecanismo interno. Embora você não veja evidências físicas de AppContainers no monitor de processos, pode encontrá-las em regras de firewall de saída criadas pela instalação para impedir que processos façam chamadas de rede.

## <a name="firewall-rules-created-by-setup"></a>Regras de firewall criadas pela instalação

Por padrão, o SQL Server desabilita as conexões de saída criando regras de firewall. Anteriormente, essas regras se baseavam em contas de usuário local, em que a instalação criava uma regra de saída para **SQLRUserGroup** que negava acesso à rede para seus membros (cada conta de trabalho era listada como uma entidade de princípio local para a regra). 

Como parte da mudança para os AppContainers, há novas regras de firewall baseadas em SIDs de AppContainer: uma para cada um dos 20 AppContainers criados pela instalação do SQL Server. As convenções de nomenclatura para o nome da regra de firewall são **Bloquear o acesso à rede para o AppContainer-00 na instância MSSQLSERVER do SQL Server**, em que 00 é o número do AppContainer (00-20 por padrão) e MSSQLSERVER é o nome da instância do SQL Server. 

> [!Note]
> Se forem necessárias chamadas de rede, você poderá desabilitar as regras de saída no Firewall do Windows.

## <a name="program-file-permissions"></a>Permissões de arquivo de programa

Assim como nas versões anteriores, o **SQLRUserGroup** continua a fornecer permissões de leitura e execução em executáveis nos diretórios SQL Server **Binn**, **R_SERVICES** e **PYTHON_SERVICES**. Nesta versão, o único membro de **SQLRUserGroup** é a conta de serviço do SQL Server Launchpad.  Quando o serviço Launchpad inicia um ambiente de execução de R ou Python, o processo é executado como um serviço Launchpad.

## <a name="implied-authentication"></a>Autenticação implícita

Como antes, a configuração adicional ainda é necessária para *autenticação implícita* nos casos em que o script ou o código precisa se conectar novamente ao SQL Server usando a autenticação confiável para recuperar dados ou recursos. A configuração adicional envolve a criação de um logon de banco de dados para **SQLRUserGroup**, cujo único membro é agora a única conta de serviço do SQL Server Launchpad em vez de várias contas de trabalho. Para obter mais informações sobre essa tarefa, confira [Adicionar SQLRUserGroup como um usuário de banco de dados](../security/create-a-login-for-sqlrusergroup.md).


## <a name="symbolic-link-created-by-setup"></a>Link simbólico criado pela instalação

Um link simbólico é criado para o **R_SERVICES** e o **PYTHON_SERVICES** padrão atual como parte da instalação do SQL Server. Se você não quiser criar esse link, uma alternativa será conceder a permissão de leitura “todos os pacotes de aplicativos” à hierarquia que leva até a pasta.


## <a name="see-also"></a>Confira também

+ [Instalar Serviços de Machine Learning do SQL Server no Windows](sql-machine-learning-services-windows-install.md)
+ [Instalar Serviços de Machine Learning do SQL Server no Linux](../../linux/sql-server-linux-setup-machine-learning.md)
