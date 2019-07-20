---
title: Diferenças no SQL Server 2019
description: Saiba o que há de novo para o R e Python SQL Server as extensões de aprendizado de máquina na versão de visualização do SQL Server 2019.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8996d47c58841f668813c8ff344683150e456fb3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344999"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>Diferenças na instalação do SQL Server Serviços de Machine Learning no SQL Server 2019  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

No Windows, SQL Server instalação do 2019 altera o mecanismo de isolamento para processos externos. Essa alteração substitui as contas de trabalho locais por [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), uma tecnologia de isolamento para aplicativos cliente em execução no Windows. 

Não há itens de ação específicos para o administrador como resultado da modificação. Em um servidor novo ou atualizado, todos os scripts externos e códigos executados no [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) seguem o novo modelo de isolamento automaticamente. 

Resumido, as principais diferenças nesta versão são:

+ As contas de usuário local no **grupo de usuários restritos do SQL (SQLRUserGroup)** não são mais criadas ou usadas para executar processos externos. AppContainers os substitua.
+ A associação **SQLRUserGroup** foi alterada. Em vez de várias contas de usuário local, a associação consiste apenas na conta de serviço SQL Server Launchpad. Os processos R e Python agora são executados sob a identidade do serviço Launchpad, isolado por meio de AppContainers.

Embora o modelo de isolamento tenha sido alterado, o assistente de instalação e os parâmetros de linha de comando permanecem os mesmos no SQL Server 2019. Para obter ajuda com a instalação, consulte [instalar SQL Server serviços de Machine Learning](sql-machine-learning-services-windows-install.md).

## <a name="about-appcontainer-isolation"></a>Sobre o isolamento do AppContainer

Em versões anteriores, **SQLRUserGroup** continha um pool de contas de usuário do Windows locais (MSSQLSERVER00-MSSQLSERVER20) usado para isolar e executar processos externos. Quando um processo externo era necessário, SQL Server Launchpad serviço iria pegar uma conta disponível e usá-la para executar um processo. 

No SQL Server 2019, a instalação não cria mais contas de trabalho locais. Em vez disso, o isolamento é obtido por meio de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). Em tempo de execução, quando o script inserido ou o código é detectado em um procedimento armazenado ou consulta, SQL Server chama o Launchpad com uma solicitação para um iniciador específico da extensão. O Launchpad invoca o ambiente de tempo de execução apropriado em um processo sob sua identidade e cria uma instância de um AppContainer para contê-lo. Essa alteração é benéfica porque o gerenciamento de conta local e de senha não é mais necessário. Além disso, em instalações em que as contas de usuário local são proibidas, a eliminação da dependência de conta de usuário local significa que agora você pode usar esse recurso.

Conforme implementado por SQL Server, AppContainers são um mecanismo interno. Embora você não veja evidências físicas de AppContainers no monitor de processos, pode encontrá-las em regras de firewall de saída criadas pela instalação para impedir que processos façam chamadas de rede.

## <a name="firewall-rules-created-by-setup"></a>Regras de firewall criadas pela instalação

Por padrão, SQL Server desabilita as conexões de saída criando regras de firewall. No passado, essas regras eram baseadas em contas de usuário local, em que a instalação criou uma regra de saída para **SQLRUserGroup** que negou acesso à rede a seus membros (cada conta de trabalho estava listada como um princípio local sujeito ao rule_. 

Como parte da mudança para AppContainers, há novas regras de firewall baseadas em SIDs de AppContainer: uma para cada uma das 20 AppContainers criadas pela instalação do SQL Server. As convenções de nomenclatura para o nome da regra de firewall são **bloquear o acesso à rede para o appcontainer-00 na instância SQL Server MSSQLSERVER**, em que 00 é o número do appcontainer (00-20 por padrão) e MSSQLSERVER é o nome da instância de SQL Server. 

> [!Note]
> Se forem necessárias chamadas de rede, você poderá desabilitar as regras de saída no firewall do Windows.

## <a name="program-file-permissions"></a>Permissões de arquivo de programa

Assim como nas versões anteriores, o **SQLRUserGroup** continua fornecendo permissões de leitura e execução em executáveis nos diretórios SQL Server **Binn**, **R_SERVICES**e **PYTHON_SERVICES** . Nesta versão, o único membro de **SQLRUserGroup** é a conta de serviço SQL Server Launchpad.  Quando o serviço Launchpad inicia um ambiente de execução R ou Python, o processo é executado como um serviço LaunchPad.

## <a name="implied-authentication"></a>Autenticação implícita

Como antes, a configuração adicional ainda é necessária para *autenticação implícita* em casos em que o script ou o código precise se conectar de volta ao SQL Server usando a autenticação confiável para recuperar dados ou recursos. A configuração adicional envolve a criação de um logon de banco de dados para **SQLRUserGroup**, cujo único membro é agora a única conta de serviço de SQL Server Launchpad em vez de várias contas de trabalho. Para obter mais informações sobre essa tarefa, consulte [Adicionar SQLRUserGroup como um usuário de banco de dados](../security/create-a-login-for-sqlrusergroup.md).


## <a name="symbolic-link-created-by-setup"></a>Link simbólico criado pela instalação

Um link simbólico é criado para o **R_SERVICES** e o **PYTHON_SERVICES** padrão atuais como parte da instalação do SQL Server. Se você não quiser criar esse link, uma alternativa é conceder a permissão de leitura ' todos os pacotes de aplicativos ' à hierarquia que leva até a pasta.


## <a name="see-also"></a>Confira também

+ [Instalar SQL Server Serviços de Machine Learning no Windows](sql-machine-learning-services-windows-install.md)

+ [Instalar o SQL Server 2019 Serviços de Machine Learning no Linux](../../linux/sql-server-linux-setup-machine-learning.md)
