---
title: "Perguntas frequentes sobre atualização e instalação (SQL Server R Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 59
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 395554af6b9d014d560d8b6520d032966630c5b2
ms.contentlocale: pt-br
ms.lasthandoff: 09/08/2017

---
# <a name="upgrade-and-installation-faq-sql-server-r-services"></a>Perguntas frequentes sobre atualização e instalação (SQL Server R Services)

Este tópico fornece respostas para algumas perguntas comuns sobre a instalação de recursos do SQL Server de aprendizado de máquina. Ele também aborda perguntas comuns sobre atualizações. Alguns problemas ocorrem apenas com as atualizações de versões de pré-lançamento. Portanto, recomendamos que você identificar a versão e edição primeira e, atualize para a versão mais recente ou a versão de serviço assim que possível.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 Services (no banco de dados) de aprendizado de máquina

## <a name="performing-setup-for-the-first-time"></a>Executar o programa de instalação pela primeira vez

Siga os procedimentos de configuração de [! INCLUDEssCurrent] e os componentes de R, conforme descrito aqui: 

+ [Configurar o SQL Server R Services ou Machine Learning serviços no banco de dados](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)
+ [Configurar o SQL Server 2017 com Python](../python/setup-python-machine-learning-services.md)
+ [Criar um R Server autônomo](create-a-standalone-r-server.md)

Após a instalação do SQL Server para usar scripts de R ou Python externos, você deve concluir algumas configurações adicionais. Isso ocorre porque o recurso de execução do script externo não está habilitado por padrão.

> [!NOTE]
> Não use as instruções de configuração que foram publicadas antes do lançamento do SQL Server 2016. O processo de instalação completamente alterado entre versões iniciais e a versão de lançamento oficial. 

### <a name="requirements-and-restrictions"></a>Requisitos e restrições

Dependendo da construção de serviços de R que você está instalando, algumas das limitações a seguir podem ser aplicadas:

- Em versões anteriores do SQL Server 2016 R Services, era preciso uma notação 8ponto3 na unidade que contém o diretório de trabalho. Se você instalou uma versão de pré-lançamento, a atualização para o Service Pack 1 do SQL Server 2016 deve remover esse requisito.

- Não é possível instalar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] em um cluster de failover. 

- Em uma VM do Azure, algumas configurações adicionais podem ser necessárias. Por exemplo, você precisará criar uma exceção de firewall para dar suporte a acesso remoto.

- Não há suporte para a instalação lado a lado com outra versão do R, ou com outras versões do Revolution Analytics.

- Não há mais suporte para uma nova instalação de nenhuma versão de pré-lançamento do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] . Se você estiver usando uma versão de pré-lançamento, atualize o mais rápido possível.

- Desabilite antivírus antes de iniciar a instalação. Após a instalação é concluída, é recomendável suspender a verificação de vírus nas pastas usadas pelo SQL Server (preferencialmente toda a árvore).

### <a name="licensing-agreements-for-unattended-installs"></a>Contratos de licenciamento para instalações autônomas

Se você usar a linha de comando para atualizar uma instância do SQL Server, certifique-se de que a linha de comando inclui o novo parâmetro de contrato de licença, */IACCEPTROPENLICENSEAGREEMENT*. A instalação pode falhar se você não usar esse parâmetro.

### <a name="offline-installation-of-r-components-for-a-localized-version-of-sql-server"></a>Instalação offline de componentes de R para uma versão localizada do SQL Server

Quando você instala o R Services em um computador que não tem acesso à internet, você deve levar duas etapas adicionais. Baixe o instalador de componentes de R em uma pasta local antes de executar a instalação do SQL Server e editar o arquivo do instalador para garantir que o idioma correto está instalado.

O identificador de idioma usado para os componentes de R deve ser o mesmo que o idioma da instalação do SQL Server, ou o **próximo** botão será desabilitado e não pode concluir a instalação.

Para obter mais informações, consulte [instalar componentes de R sem acesso à internet](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md).

## <a name="post-installation-configuration"></a>Configuração de pós-instalação

Para usar o aprendizado de máquina com R ou Python, alguma configuração adicional é necessária depois de executar a instalação do SQL Server. Etapas adicionais podem ser necessárias dependendo do nível de segurança do servidor e de sua instância do SQL Server e bancos de dados. Examine essas etapas das instruções de instalação para determinar se qualquer configuração adicional pode ser necessário.

[Defina o SQL Server R Services no banco de dados](set-up-sql-server-r-services-in-database.md)

- O recurso que oferece suporte à execução de scripts externos, como Python, ou de R é desabilitado por padrão para a segurança de banco de dados e deve ser habilitado.

- Verifique se as contas de trabalho que são usadas pela barra inicial para executar R ou Python tem acesso à instância.

- Talvez seja necessário habilitar o acesso remoto no servidor, ou criar uma regra de firewall que permite a comunicação de entrada com o SQL Server.

- Dependendo da carga de trabalho planejada, convém otimizar o servidor para tarefas de aprendizado de máquina. 

## <a name="upgrades-or-uninstallation"></a>Atualizações ou desinstalação

Esta seção contém instruções detalhadas para cenários de atualização específicos.

Não há suporte para atualizações de uma versão de pré-lançamento do SQL Server 2016 R Services. É recomendável que você desinstale a versão de pré-lançamento e, em seguida, instala uma versão de lançamento assim que possível.

### <a name="support-for-slipstream-upgrades"></a>Suporte para atualizações de instalação integrada

A instalação integrada refere-se à capacidade de aplicar um patch ou atualizar para uma instalação de instância com falha para corrigir problemas existentes. A vantagem desse método é que o SQL Server é atualizado ao mesmo tempo que você executar a instalação, evitando separado reiniciar mais tarde.

Se o servidor não tiver acesso à internet, certifique-se de baixar o instalador do SQL Server. Você também deve baixar separadamente versões correspondentes dos instaladores de componente do R *antes* do início do processo de atualização. 

Para locais de download, consulte [componentes de instalação de R sem acesso à internet](installing-ml-components-without-internet-access.md).

Quando todos os arquivos de instalação tiverem sido copiados para um diretório local, inicie o utilitário de configuração digitando SETUP.EXE na linha de comando.

- Use o */UPDATESOURCE* argumento para especificar o local de um arquivo local que contém a atualização do SQL Server, como uma versão do service pack ou uma atualização cumulativa.

- Use o */MRCACHEDIRECTORY* argumento para especificar a pasta que contém os arquivos de CAB do componente de R.

Para obter mais informações, consulte este blog pela equipe de suporte: [implantando serviços de R em computadores sem acesso à internet](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/).

### <a name="upgrade-r-components-offline"></a>Atualizar os componentes de R offline

Se você instalar ou atualiza os servidores que não estão conectados à internet, você deve baixar uma versão atualizada dos componentes de R manualmente antes de iniciar a atualização. Para obter mais informações, consulte [componentes de instalação de R sem acesso à internet](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md).

### <a name="schedule-for-update-of-r-components"></a>Agenda de atualização de componentes de R

Quando os hotfixes ou melhorias para o SQL Server 2016 são liberadas, componentes de R também são atualizadas ou atualizados, se sua instância já inclui o recurso Serviços de R.

Se você estiver usando o SQL Server 2017, atualizações para componentes de R são instaladas automaticamente.

A partir de dezembro de 2016, você pode atualizar os componentes de R em um ritmo mais rápido que o ciclo de versão do SQL Server. Para fazer isso, *associação* uma instância dos serviços do R para a política de ciclo de vida do Software moderno. Atualmente o suporte é fornecido apenas para a atualização de instâncias de 2016. Quando uma nova versão do servidor do R é liberada, você poderá atualizar para instâncias de 2017 também.

Para obter mais informações, consulte [SqlBindR de uso para atualizar uma instância do SQL Server R Services](../../advanced-analytics/r-services/use-sqlbindr-exe-to-upgrade-an-instance-of-r-services.md).

### <a name="upgrade-from-a-pre-release-version-of-sql-server-2016"></a>Atualizar de uma versão de pré-lançamento do SQL Server 2016

Em geral, as atualizações in-loco, não há suporte para as versões de pré-lançamento.

Para instalar os serviços de R com êxito, você deve desinstalar as versões anteriores do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] e seus componentes de R relacionados. Isso inclui o SQL Server 2016 CTP3, CTP 3.1, CTP 3.2, RC0 ou RC1.

Desinstalando uma versão de pré-lançamento pode ser complexo e requer a execução de um script especial. Contate o suporte técnico para obter ajuda.

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

Se você tiver alguma dúvida sobre qual versão você está usando, execute `@@VERSION` do SQL Server Management Studio.

### <a name="problems-with-setup-of-r-server-standalone"></a>Problemas com a instalação do R Server (autônomo)

Esta seção descreve problemas específicos para instalações do Microsoft R Server (autônomo) que usam a instalação do SQL Server 2016. Para problemas mais gerais relacionados a atualizações de R Server, consulte [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) no MSDN.

#### <a name="failure-to-install-localized-versions"></a>Falha ao instalar as versões localizadas

Quando você instala o R Server offline, as versões de pré-lançamento não permitem que você use idiomas traduzidos.

Em geral, quando o servidor não tem acesso à internet, antes de executar a instalação você deve baixar os pacotes de instalação para o servidor de R. Em seguida, você deve especificar o local dos arquivos durante a instalação.

No entanto, se o identificador de idioma associado ao pacote de instalador não é o mesmo que o idioma da instalação do SQL Server, ocorre um problema. Quando você chegar à página para a instalação de componentes de R, o **próximo** botão será desabilitado e não pode prosseguir com a instalação. Como alternativa, você pode renomear o pacote para usar um identificador correspondente.

Por exemplo, o nome dos pacotes de instalação pode ser `SRO_3.2.2.0_1031.cab`.
Para instalar o idioma 104 no SQL Server, renomeie o arquivo para `SRO_3.2.2.0_1041.cab`.

#### <a name="installing-r-services-and-r-server-standalone-on-the-same-computer"></a>Instalando serviços do R e R Server autônomo no mesmo computador

Em geral, você não instalar os serviços de R (no banco de dados) e o R Server (autônomo) no mesmo computador. No entanto, se o servidor tiver capacidade suficiente, R Server autônomo pode ser útil como uma ferramenta de desenvolvimento. Talvez você precise usar os recursos de operacionalização do R Server e acessar dados do SQL Server do servidor de R sem movimentação de dados.

Observe que, se você instalar o R Server e serviços do R no mesmo computador, dois conjuntos separados das mesmas bibliotecas de R estão instalados. Uma é para uso pela instância do SQL Server, e uma é para o desenvolvimento de usar ou usar por R Server.

Em versões anteriores do SQL Server 2016, instalar o R Server (autônomo) e serviços de R (no banco de dados) ao mesmo tempo pode causar falha com uma mensagem de "acesso negado". Esse problema foi corrigido no Service Pack 1 para SQL Server 2016.

Se você encontrou este erro e precisa atualizar esses recursos, execute uma instalação integrada do SQL Server 2016 com SP1. Há duas maneiras de resolver o problema, que requerem a desinstalação e reinstalação.

1. Desinstalar o R Services (no banco de dados) e verifique se que as contas de usuário para SQLRUserGroup são removidas.

2. Reinicie o servidor e, em seguida, reinstalar o R Server (autônomo).

3. Execução do SQL Server setup uma vez mais e desta vez selecione **adicionar recursos ao SQL Server existente**.

4. Escolha a instância e, em seguida, selecione o **R Services (no banco de dados)** opção para adicionar.

Em alguns casos, esse procedimento não resolver o problema. Tente a seguinte solução alternativa:

1. Desinstale o R Services (no banco de dados) e R Server (autônomo) ao mesmo tempo.

2. Remova as contas de usuário local (SQLRUserGroup).

3. Reinicie o servidor.

4. Execute a instalação do SQL Server e adicionar somente o recurso Serviços de R (no banco de dados). Não selecione **R Server (autônomo)**.

## <a name="see-also"></a>Consulte também

 [Introdução ao SQL Server R Services](../r/getting-started-with-sql-server-r-services.md)

 [Guia de Introdução ao Microsoft R Server autônomo](../r/getting-started-with-microsoft-r-server-standalone.md)

