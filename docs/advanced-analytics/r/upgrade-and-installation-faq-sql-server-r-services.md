---
title: "Perguntas frequentes sobre atualização e instalação de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.date: 10/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: "59"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 3c4fb79f04daeff6d98856b521fa1602a2334cdd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning"></a>Perguntas frequentes sobre atualização e instalação de aprendizado de máquina do SQL Server

Este tópico fornece respostas para algumas perguntas comuns sobre a instalação de recursos do SQL Server de aprendizado de máquina. Ele também aborda perguntas comuns sobre atualizações.

+ Alguns problemas ocorrem apenas com as atualizações de versões de pré-lançamento. Portanto, recomendamos que você identificar a versão e edição primeiro antes de ler estas notas.
+ Atualize para a versão mais recente ou assim que possível, a versão de serviço para resolver quaisquer problemas que foram corrigidos nas versões recentes.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 Services (no banco de dados) de aprendizado de máquina

## <a name="performing-setup-for-the-first-time"></a>Executar o programa de instalação pela primeira vez

Siga os procedimentos para configurar [!INCLUDE[sscurrent_md](../../includes/sscurrent_md.md)] e os componentes de R, conforme descrito aqui: 

+ [Configurar o SQL Server R Services ou Machine Learning serviços no banco de dados](../r/set-up-sql-server-r-services-in-database.md)
+ [Configurar o SQL Server 2017 com Python](../python/setup-python-machine-learning-services.md)
+ [Criar um R Server autônomo](../r/create-a-standalone-r-server.md)

> [!IMPORTANT]
> 
> Depois que você instalou o SQL Server e a aprendizado recursos, antes que você pode usar scripts de R ou Python de máquina, você deve concluir algumas etapas de configuração adicionais. Isso ocorre porque o recurso de execução do script externo não está habilitado por padrão.

### <a name="requirements-and-restrictions"></a>Requisitos e restrições

Dependendo de compilação do SQL Server que você está instalando, algumas das limitações a seguir podem ser aplicadas:

- Em versões anteriores do SQL Server 2016 R Services, era preciso uma notação 8ponto3 na unidade que contém o diretório de trabalho. Se você instalou uma versão de pré-lançamento, a atualização para o Service Pack 1 do SQL Server 2016 deve corrigir esse problema. Esse requisito não se aplicam às versões após o SP1.

- No momento, você não pode instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um cluster de failover. 

- Em uma VM do Azure, algumas configurações adicionais podem ser necessárias. Por exemplo, você precisará criar uma exceção de firewall para dar suporte a acesso remoto.

- Não há suporte para a instalação lado a lado com outra versão do R, ou com outras versões do Revolution Analytics.

- Não há mais suporte para uma nova instalação de nenhuma versão de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] . Se você estiver usando uma versão de pré-lançamento, atualize o mais rápido possível.

- Desabilite antivírus antes de iniciar a instalação. Após a instalação é concluída, é recomendável suspender a verificação de vírus nas pastas usadas pelo [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. De preferência, suspender a verificação em todo o [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] árvore.

### <a name="licensing-agreements-for-unattended-installs"></a>Contratos de licenciamento para instalações autônomas

Se você usar a linha de comando para atualizar uma instância do SQL Server, certifique-se de que a linha de comando inclui tanto o [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] licenciamento parâmetro do contrato e os novos parâmetros de contrato de licença para R e Python.

### <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server"></a>Instalação offline de componentes de aprendizado de máquina para uma versão localizada do SQL Server

Quando você instala [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] componentes de aprendizado de máquina em um computador que não tem acesso à internet, você deve realizar algumas etapas adicionais:

+ Baixe os instaladores de componente de R ou Python para uma pasta local antes de executar a instalação do SQL Server.
+ Em alguns casos, você precisará editar o arquivo do instalador para garantir que o idioma correto está instalado.
+ O identificador de idioma usado para a componentes de aprendizado de máquina deve ser o mesmo que o idioma da instalação do SQL Server, ou você não pode concluir a instalação.

Para obter mais informações, consulte [instalação de componentes de aprendizado de máquina sem acesso à internet](../r/installing-ml-components-without-internet-access.md).

## <a name="post-installation-configuration"></a>Configuração de pós-instalação

Para usar o aprendizado de máquina com R ou Python, alguma configuração adicional é necessária depois de executar a instalação do SQL Server. As etapas necessárias dependem do nível de segurança do servidor e como você configurou sua instância do SQL Server e bancos de dados.

Examine todas as opções na lista de instruções de pós-instalação para ver quais etapas adicionais podem ser necessárias em seu ambiente.

+ [Configurar o banco de dados de aprendizado de máquina do SQL Server](set-up-sql-server-r-services-in-database.md) 

## <a name="upgrades-or-uninstallation"></a>Atualizações ou desinstalação

Esta seção contém instruções detalhadas para cenários de atualização específicos.

### <a name="how-to-upgrade-sql-server"></a>Como atualizar o SQL Server

Você pode atualizar sua versão do SQL Server executando novamente o Assistente de instalação.

+ [Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Atualize o SQL Server usando o Assistente de instalação](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Você pode atualizar apenas a componentes usando um processo chamado associação de aprendizado de máquina: 
+ [Use SqlBindR para atualizar os componentes de aprendizado de máquina](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Fim do suporte para atualizações in-loco das versões de pré-lançamento

Não há suporte para atualizações de versões de pré-lançamento do SQL Server 2016. Isso inclui o SQL Server 2016 CTP3, CTP 3.1, CTP 3.2, RC0 ou RC1.

As seguintes versões foram instaladas com as versões de pré-lançamento do SQL Server 2016.

| Versão | Compilação         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Se você tiver alguma dúvida sobre qual versão você está usando, execute `@@VERSION` em uma consulta do SQL Server Management Studio.

Em geral, o processo de atualização é da seguinte maneira:

1. Fazer backup de dados e scripts.
2. Desinstale a versão de pré-lançamento.
3. Instale uma versão de lançamento.

Componentes de aprendizado de máquina desinstalar uma versão de pré-lançamento do SQL Server podem ser complexos e podem exigir a execução de um script especial. Contate o suporte técnico para obter ajuda.

### <a name="support-for-slipstream-upgrades"></a>Suporte para atualizações de instalação integrada

A instalação integrada refere-se à capacidade de aplicar um patch ou atualizar para uma instalação de instância com falha para corrigir problemas existentes. A vantagem desse método é que o SQL Server é atualizado ao mesmo tempo que você executar a instalação, evitando separado reiniciar mais tarde.

Se o servidor não tiver acesso à internet, certifique-se de baixar o instalador do SQL Server. Você também deve baixar separadamente versões correspondentes dos instaladores de componente do R *antes* do início do processo de atualização. 

Para locais de download, consulte [instalação de componentes de aprendizado de máquina sem acesso à internet](installing-ml-components-without-internet-access.md).

Quando todos os arquivos de instalação tiverem sido copiados para um diretório local, inicie o utilitário de configuração digitando SETUP.EXE na linha de comando.

- Use o */UPDATESOURCE* argumento para especificar o local de um arquivo local que contém a atualização do SQL Server, como uma versão do service pack ou uma atualização cumulativa.

- Use o */MRCACHEDIRECTORY* argumento para especificar a pasta que contém os arquivos de CAB do componente de R.

Para obter mais informações, consulte este blog pela equipe de suporte: [implantando serviços de R em computadores sem acesso à internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).

### <a name="get-machine-learning-components-for-offline-installs"></a>Obter componentes de aprendizado de máquina para instalação offline

Se você instalar ou atualiza os servidores que não estão conectados à internet, você deve baixar uma versão atualizada da máquina aprendizado componentes manualmente antes de iniciar a atualização. 

+ [Instalação de componentes de aprendizado de máquina sem acesso à internet](../../advanced-analytics/r/installing-ml-components-without-internet-access.md).

### <a name="support-policy-and-schedule-for-update-of-machine-learning-components"></a>Política de suporte e agendamento de atualização de componentes de aprendizado de máquina

Quando os hotfixes ou melhorias para o SQL Server são liberadas, componentes de aprendizado de máquina são automaticamente atualizadas ou atualizados, se sua instância já inclui o recurso.

A partir de dezembro de 2016, você pode atualizar os componentes de aprendizado de máquina em um ritmo mais rápido que o ciclo de versão do SQL Server. Para fazer isso, *associação* uma instância do SQL Server para a política de ciclo de vida do Software moderno. Sempre que uma nova versão das ferramentas de aprendizado de máquina é liberada, a equipe de desenvolvimento de aprendizado de máquina, você pode baixar a versão mais recente e aplicá-la a uma instância do SQL Server que é usada para o aprendizado de máquina.

Para obter mais informações, consulte:

+ [Linha do tempo de suporte para o Microsoft R Server e o servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)
+ [Use SqlBindR para atualizar uma instância do SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="r-server-standalone"></a>R Server (Autônomo)

Esta seção descreve problemas específicos para instalações do Microsoft R Server (autônomo) que usam a instalação do SQL Server 2016. 

Para problemas relacionados a atualizações do servidor de R para o servidor de aprendizado de máquina, consulte [instalar Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

### <a name="problems-when-r-services-and-r-server-standalone-are-installed-on-the-same-computer"></a>Problemas quando os serviços de R e R Server autônomo são instalados no mesmo computador

Em versões anteriores do SQL Server 2016, instalar o R Server (autônomo) e serviços de R (no banco de dados) ao mesmo tempo, às vezes, causou falha com uma mensagem de "acesso negado". Esse problema foi corrigido no Service Pack 1 para SQL Server 2016.

Se você encontrou este erro e precisa atualizar esses recursos, execute uma instalação integrada do SQL Server 2016 com SP1. Há duas maneiras de resolver o problema, que requerem a desinstalação e reinstalação.

1. Desinstalar o R Services (no banco de dados) e verifique se que as contas de usuário para SQLRUserGroup são removidas.

2. Reinicie o servidor e, em seguida, reinstalar o R Server (autônomo).

3. Execução do SQL Server setup uma vez mais e desta vez selecione **adicionar recursos ao SQL Server existente**.

4. Escolha a instância e, em seguida, selecione o **R Services (no banco de dados)** opção para adicionar.

Se esse procedimento não resolver o problema, tente a seguinte solução alternativa:

1. Desinstale o R Services (no banco de dados) e R Server (autônomo) ao mesmo tempo.

2. Remova as contas de usuário local (SQLRUserGroup).

3. Reinicie o servidor.

4. Execute a instalação do SQL Server e adicionar somente o recurso Serviços de R (no banco de dados). Não selecione **R Server (autônomo)**.

Em geral, é recomendável que você não instale os serviços de R (no banco de dados) e o R Server (autônomo) no mesmo computador. No entanto, supondo que o servidor tem capacidade suficiente, você pode achar que r Server autônomo pode ser útil como uma ferramenta de desenvolvimento. Outro cenário possível é que você precisa usar os recursos de operacionalização do R Server, mas também quer acessar dados do SQL Server sem movimentação de dados.

## <a name="see-also"></a>Consulte também

 [Introdução ao SQL Server R Services](../r/getting-started-with-sql-server-r-services.md)

 [Guia de Introdução ao Microsoft R Server autônomo](../r/getting-started-with-microsoft-r-server-standalone.md)
