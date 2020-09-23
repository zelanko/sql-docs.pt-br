---
title: Criar instância de cluster de failover
description: Este artigo descreve como usar o programa de instalação para instalar ou atualizar uma instância de cluster de failover do Always On do SQL Server ou adicionar um nó a uma instância de cluster de failover existente.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- adding nodes
- failover clustering [SQL Server], creating clusters
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- clusters [SQL Server], creating
- removing nodes
ms.assetid: 30e06a7d-75e9-44e2-bca3-b3b0c4a33f61
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 03a3b84d5f21391d957ea1ae1f71286133e4d492
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442379"
---
# <a name="create-a-new-always-on-failover-cluster-instance-setup"></a>Criar uma instância de cluster de failover do Always On (instalação)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Para instalar ou atualizar uma FCI (instância de cluster de failover) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você deve executar o programa de instalação em cada nó do cluster de failover do Windows Server subjacente. Para adicionar um nó a uma instância do cluster de failover existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é necessário executar a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no nó a ser adicionado à instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Não execute a Instalação no nó ativo para gerenciar os outros nós.  
  
 Dependendo de como os nós estão agrupados, a instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será configurada das seguintes maneiras:  
  
-   Nós na mesma sub-rede ou no mesmo conjunto de sub-redes - A dependência do recurso de endereço IP é definida como AND para esses tipos de configurações.  
  
-   Nós em sub-redes diferentes: a dependência do recurso de endereço IP será definida como OR, e essa configuração será chamada de configuração da instância de cluster de failover com várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Clustering de várias sub-redes do SQL Server &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md).  
  
 As opções a seguir estão disponíveis para a instalação de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 **Opção 1: Instalação de integração com Adicionar Nó**   
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consiste nas seguintes etapas:  
  
-   Criar e configurar uma instância de cluster de failover de um único nó do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Ao concluir a configuração bem-sucedida de um nó, você tem uma instância de cluster de failover totalmente funcional. Nesse ponto, ela não tem alta disponibilidade, porque há apenas um nó na instância do cluster de failover.  
  
-   Em cada nó a ser adicionado à instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], execute a Instalação com a funcionalidade Adicionar Nó.  
  
    -   Se o nó que você está incluindo tiver sub-redes adicionais ou diferentes, a instalação permitirá especificar endereços IP adicionais. Se o nó que você está adicionando estiver em uma sub-rede diferente, também será preciso confirmar a alteração de dependência do recurso de endereço IP para OR. Confira mais informações sobre os diferentes cenários possíveis durante as operações Adicionar Nó em [ Adicionar ou remover nós em uma instância de cluster de failover do Always On &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
 **Opção 2: Instalação Avançada/Corporativa**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A instalação Avançada/Corporativa do cluster de failover consiste nas seguintes etapas:  
  
-   Em cada nó que seja um possível proprietário do novo cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , siga as etapas de instalação de Preparar cluster de failover listadas na seção [Preparar](#prepare). Depois de executar a Preparação de Cluster de Failover em um nó, a Instalação criará o arquivo Configuration.ini que lista todas as configurações especificadas. Nos nós adicionais a serem preparados, em vez de seguir essas etapas, você pode fornecer o arquivo Configuration.ini gerado automaticamente do primeiro nó como uma entrada para a linha de comando de Instalação. Para obter mais informações, veja [Instalar o SQL Server 2016 usando um arquivo de configuração](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md). Essa etapa prepara os nós prontos para serem clusterizados, mas não há nenhuma instância operacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no final dessa etapa.  
  
-   Depois que os nós estiverem preparados para clustering, execute a Instalação em um dos nós preparados. Essa etapa configura e conclui a instância de cluster de failover. No final dessa etapa, você terá uma instância de cluster de failover operacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], e todos os nós preparados anteriormente para essa instância serão os possíveis proprietários da instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recém-criada.  
  
     Se você estiver criando uma instância de cluster de failover que abrange várias sub-redes, a Instalação detectará a união de todas as sub-redes em todos os nós que têm a instância de cluster de failover preparada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Você poderá especificar vários endereços IP para as sub-redes. Cada nó preparado deve ser o possível proprietário de pelo menos um endereço IP.  
  
     Se cada um dos endereços IP especificados para as sub-redes tiverem suporte em todos os nós preparados, a dependência será definida como AND.  
  
     Se cada um dos endereços IP especificados para as sub-redes não tiverem suporte em todos os nós preparados, a dependência será definida como OR. Para obter mais informações, consulte [Clustering de várias sub-redes do SQL Server &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md).  
  
    > [!NOTE]  
    >  O cluster de failover concluído exige que exista um cluster de failover subjacente do Windows Server. Se o cluster de failover do Windows Server não existir, a Instalação apresentará um erro e será encerrada.  
  
 Confira mais informações sobre como adicionar ou remover nós de uma instância de cluster de failover existente em [Adicionar ou remover nós em uma instância de cluster de failover do Always On &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
 Para obter mais informações sobre a instalação remota, consulte [Atualizações de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
 Confira mais informações sobre como instalar o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em um WSFC em [Como criar clusters do SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=396548).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de começar, examine os seguintes tópicos dos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   [Planejando uma instalação do SQL Server](../../../sql-server/install/planning-a-sql-server-installation.md)  
  
-   [Antes de instalar o cluster de failover](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [Considerações sobre segurança para uma instalação do SQL Server](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [Clustering de várias sub-redes do SQL Server &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)  
  
> [!NOTE]  
>  Anote o local da unidade compartilhada no Administrador de Cluster antes de executar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Você deve ter essas informações para criar uma instância de cluster de failover.  
  
### <a name="to-install-a-new-ssnoversion-failover-cluster-instance-using-integrated-install-with-add-node"></a>Para instalar uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a Instalação Integrada com Adicionar Nó.  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, vá para a pasta raiz do compartilhamento e clique duas vezes em Setup.exe. Para obter mais informações sobre como instalar os pré-requisitos, consulte [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md).  
  
2.  O Assistente de Instalação inicia o Centro de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para criar uma nova instalação de cluster do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], clique em **Nova instalação de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** na página de instalação.  
  
3.  O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**.  
  
4.  Para continuar, clique em **Avançar**.  
  
5.  Na página Arquivos de Suporte à Instalação, clique em **Instalar** para instalar os arquivos de suporte à Instalação.  
  
6.  O Verificador de Configuração do Sistema verifica o estado do sistema do computador antes da continuação da instalação. Depois de concluir a verificação, clique em **Avançar** para continuar. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**.  
  
7.  Na página Chave do Produto, indique se você está instalando uma edição gratuita do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ou se tem uma chave de PID para uma versão de produção do produto. Para obter mais informações, consulte [Edições e componentes do SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
8.  Na página Termos de Licença, leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Clique em **Avançar** para continuar. Para finalizar a Instalação, clique em **Cancelar**.  
  
9. Na página Seleção de Recursos, selecione os componentes para a instalação. Uma descrição de cada grupo de componentes é exibida no painel à direita depois que você seleciona o nome do recurso. Você pode selecionar qualquer combinação de caixas de seleção, mas apenas o [!INCLUDE[ssDE](../../../includes/ssde-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo de tabela e o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo multidimensional oferecem suporte ao clustering de failover. Outros componentes selecionados serão executados como um recurso autônomo, sem recurso de failover no nó atual em que você está executando a Instalação. Para obter mais informações sobre modos do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , consulte [Determina o Modo de Servidor de uma instância do Analysis Services](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance).  
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação instalará os pré-requisitos ainda não instalados na etapa de instalação descrita posteriormente neste procedimento.  
  
     Você também pode especificar um diretório personalizado para componentes compartilhados por meio do campo na parte inferior desta página. Para alterar o caminho de instalação de componentes compartilhados, atualize o caminho no campo fornecido na parte inferior da caixa de diálogo ou clique no botão de reticências para navegar até um diretório de instalação. O caminho de instalação padrão é C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] \\.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também dá suporte à instalação de bancos de dados de sistema (Mestre, Modelo, MSDB e TempDB) e bancos de dados de usuários de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] em um compartilhamento de arquivos de protocolo SMB. Para obter mais informações sobre como instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o compartilhamento de arquivos SMB como um armazenamento, consulte [Instalar o SQL Server com compartilhamento de arquivos SMB como uma opção de armazenamento](../../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
     O caminho especificado para os componentes compartilhados deve ser um caminho absoluto. A pasta não deve estar compactada ou criptografada. Não há suporte para unidades mapeadas. Se você estiver instalando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um sistema operacional de 64 bits, você verá as seguintes opções:  
  
    1.  Diretório de recursos compartilhados  
  
    2.  Diretório de recursos compartilhados (x86)  
  
     O caminho especificado para cada uma das opções anteriores deve ser diferente.  
  
    > [!NOTE]  
    >  Quando você seleciona o recurso Serviços de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , a replicação e a pesquisa de texto completo são selecionadas automaticamente. Data Quality Services (DQS) também é selecionado quando você seleciona o recurso de serviços do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] . Se esses sub-recursos forem desmarcados, o recurso Serviços de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] também será desmarcado.  
  
10. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executa mais um conjunto de regras baseadas nos recursos selecionados para validar a configuração.  
  
11. Na página Configuração da Instância, especifique se deseja instalar uma instância padrão ou uma instância nomeada. Para obter mais informações, consulte [Instance Configuration](../../install/instance-configuration.md).  
  
     **Nome da Rede do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** – especifique o nome da rede da nova instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse é o nome usado para identificar sua instância de cluster de failover na rede.  
  
    > [!NOTE]  
    >  Ele é conhecido como o nome virtual do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em versões anteriores de instâncias de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
     **ID da Instância** – Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, marque a caixa **ID da Instância** e forneça um valor.  
  
    > [!NOTE]  
    >  Instâncias autônomas típicas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], com instâncias padrão ou nomeadas, não usam um valor não padrão para a caixa **ID da Instância** .  
  
     **Diretório raiz da instância** – por padrão, o diretório raiz da instância é C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\. Para especificar um diretório raiz não padrão, use o campo fornecido ou clique no botão de reticências para localizar uma pasta de instalação.  
  
     **Instâncias e recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] detectados neste computador**: a grade mostra instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que estão no computador em que a Instalação está sendo executada. Se já existir uma instância padrão instalada no computador, instale uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Clique em **Avançar** para continuar.  
  
12. Use a página Grupo de Recursos de Cluster para especificar o nome do grupo de recursos de cluster, ou a função, em que os recursos do servidor virtual do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estarão localizados. Para especificar o nome do grupo de recursos de cluster do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , há duas opções:  
  
    -   Use a caixa suspensa para especificar um grupo existente a ser usado.  
  
    -   Digite o nome de um novo grupo a ser criado. Observe que o nome "Armazenamento disponível" não é um nome de grupo válido.  
  
13. Na página Seleção de Disco de Cluster, selecione o recurso de disco de cluster compartilhado para sua instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O disco de cluster é o local onde os dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serão colocados. É possível especificar mais de um disco. A grade Discos compartilhados disponíveis exibe uma lista de discos disponíveis, se cada um deles estiver qualificado como um disco compartilhado, e uma descrição de cada recurso de disco. Clique em **Avançar** para continuar.  
  
    > [!NOTE]  
    >  A primeira unidade é usada como a unidade padrão para todos os bancos de dados, mas é possível alterá-la nas páginas de configuração do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] ou do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
    >   
    >  Na página da Seleção de Disco de Cluster, você terá a opção de ignorar a seleção de qualquer disco compartilhado se desejar usar fileshare de SMB como uma pasta de dados.  
  
14. Na página Configuração de Rede de Cluster, especifique os recursos de rede para a instância de cluster de failover.  
  
    -   **Configurações de Rede** — Especifique o tipo e o endereço IP da instância de cluster de failover.  
  
     Clique em **Avançar** para continuar.  
  
15. Use esta página para especificar a Política de Segurança de Cluster.  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e versões posteriores: SIDs de serviço (IDs de segurança de servidor) são a configuração padrão e recomendada. Não há nenhuma opção para alterar isso para grupos de segurança. Para obter informações sobre a funcionalidade de SIDs no [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)], consulte [Configurar contas de serviço e permissões do Windows](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). Isso foi testado na instalação autônoma e em cluster no [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)].  
  
    -   No [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)], especifique os grupos de domínios para serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Todas as permissões de recurso são controladas por grupos no nível do domínio que incluem contas de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como membros de grupo.  
  
     Clique em **Avançar** para continuar.  
  
16. O fluxo de trabalho do restante deste tópico depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções ([!INCLUDE[ssDE](../../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]).  
  
17. Na página Configuração do Servidor – Contas de Serviço, especifique as contas de logon dos serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os serviços reais configurados nessa página dependem dos recursos selecionados para instalação.  
  
     Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. O tipo de inicialização é definido como manual para todos os serviços com suporte a cluster, inclusive a pesquisa de texto completo e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, e não pode ser alterado durante a instalação. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda que você configure contas de serviço individualmente para fornecer privilégios mínimos para cada serviço, em que os serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recebem as permissões mínimas para concluir suas tarefas. Para obter mais informações, consulte [Configuração do servidor — Contas de serviço](https://msdn.microsoft.com/library/c283702d-ab20-4bfa-9272-f0c53c31cb9f) e [Configurar contas de serviço e permissões do Windows](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], forneça credenciais nos campos na parte inferior da página.  
  
     **Observação de segurança** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     Depois de concluir a especificação de informações de logon para serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Avançar**.  
  
18. Use a guia **Configuração do Servidor — Ordenação** para especificar ordenações não padrão para o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
19. Use a página Configuração – Provisionamento de Conta do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para especificar o seguinte:  
  
    -   Modo de Segurança - selecione Autenticação do Windows ou Autenticação de Modo Misto para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se você selecionar Autenticação de Modo Misto, deverá fornecer uma senha forte para a conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
         Depois que um dispositivo estabelecer uma conexão com êxito com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o mecanismo de segurança será o mesmo para Autenticação do Windows e Modo Misto.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Administradores: você deve especificar pelo menos um administrador de sistema para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
     Ao concluir a edição da lista, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
20. Use a página Configuração do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] - Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**.  
  
    > [!IMPORTANT]  
    >  Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os diretórios de dados devem estar localizados no disco de cluster compartilhado da instância de cluster de failover.  
  
    > [!NOTE]  
    >  Para especificar um servidor de arquivo de protocolo SMB como o Diretório de Dados, defina o **diretório raiz de dados padrão** como o fileshare do formato \\\Servername\ShareName\\...  
   
21. Use a página Configuração do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] - FILESTREAM para habilitar FILESTREAM para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Clique em **Avançar** para continuar.  
  
22. Use a página Configuração do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] - Provisionamento de Conta para especificar usuários ou contas que tenham permissões de administrador para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Especifique pelo menos um administrador de sistema para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].
  
     Ao concluir a edição da lista, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
23. Use a página Configuração do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] - Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**.  
  
    > [!IMPORTANT]  
    >  Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os diretórios de dados devem estar localizados no disco de cluster compartilhado da instância de cluster de failover.  
   
24. Use a página Configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para especificar o tipo de instalação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] a ser criada. Para instalações da instância de cluster de failover, a opção é definida como instalação Não configurada do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Você deve configurar os serviços do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] depois de concluir a instalação.  
  
 
25. O Verificador de Configuração do Sistema executa mais um conjunto de regras para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificados.  
  
26. A página Pronto para Instalar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Instalar**. A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
27. Durante a instalação, a página Progresso da Instalação fornece o status para que você possa monitorar o progresso da Instalação.  
  
28. Após a instalação, a página **Concluído** fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
29. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
30. Para adicionar nós ao failover de um único nó que você acabou de criar, execute a Instalação em cada nó adicional e siga as etapas da operação AddNode. Saiba mais em [Adicionar ou remover nós em uma instância de cluster de failover do Always On &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
    > [!NOTE]  
    >  Se você estiver adicionando mais de um nó, poderá usar o arquivo de configuração para implantar as instalações. Para obter mais informações, veja [Instalar o SQL Server 2016 usando um arquivo de configuração](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
    >   
    >  A edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que você está instalando deve combinar com todos os nós de uma instância cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ao adicionar um novo nó a uma instância de cluster de failover existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especifique que a edição corresponde à edição dessa instância.  
  
##  <a name="prepare"></a><a name="prepare"></a> Preparar  
  
#### <a name="advancedenterprise-failover-cluster-instance-install-step-1-prepare"></a>Etapa 1 de instalação da instância de cluster de failover avançada/corporativa: Preparar  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, vá para a pasta raiz do compartilhamento e clique duas vezes em Setup.exe. Para obter mais informações sobre como instalar os pré-requisitos, consulte [Before Installing Failover Clustering](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md). Talvez você receba uma solicitação para instalar os pré-requisitos, caso eles não tenham sido instalados anteriormente.  
  
2.  O Windows Installer 4.5 é necessário e pode ser instalado pelo Assistente de Instalação. Se solicitado, reinicie o computador e, em seguida, inicie a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] novamente.  
  
3.  Após a instalação dos pré-requisitos, o Assistente de Instalação inicia a Central de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para preparar o nó para clustering, acesse a página **Avançado** e clique em **Preparação de cluster avançado**.  
  
4.  O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**.  
  
5.  Na página Arquivos de Suporte à Instalação, clique em **Instalar** para instalar os arquivos de suporte à Instalação.  
  
6.  O Verificador de Configuração do Sistema verifica o estado do sistema do computador antes da continuação da instalação. Depois de concluir a verificação, clique em **Avançar** para continuar. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**.  
  
7.  Na página de Seleção de Idioma, você pode especificar o idioma da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , se estiver instalando em um sistema operacional localizado, e se a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional. Para obter mais informações sobre suporte em qualquer idioma e considerações sobre instalação, veja [Versões de Idiomas Locais no SQL Server](../../../sql-server/install/local-language-versions-in-sql-server.md).  
  
     Para continuar, clique em **Avançar**.  
  
8.  Na página Chave do Produto, clique para indicar se você está instalando uma edição gratuita do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ou se tem uma chave de PID para uma versão de produção do produto. Para obter mais informações, consulte [Edições e componentes do SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
    > [!NOTE]  
    >  Você deverá especificar a mesma chave do produto em todos os nós que estiver preparando para a mesma instância de cluster de failover.  
  
9. Na página Termos de Licença, leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Clique em **Avançar** para continuar. Para finalizar a Instalação, clique em **Cancelar**.  
  
10. Na página Seleção de Recursos, selecione os componentes para a instalação. Uma descrição de cada grupo de componentes é exibida no painel à direita depois que você seleciona o nome do recurso. Você pode selecionar qualquer combinação de caixas de seleção, mas apenas o [!INCLUDE[ssDE](../../../includes/ssde-md.md)], o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo de tabela e o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no modo multidimensional oferecem suporte ao clustering de failover. Outros componentes selecionados serão executados como um recurso autônomo, sem recurso de failover no nó atual em que você está executando a Instalação. Para obter mais informações sobre modos do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , consulte [Determina o Modo de Servidor de uma instância do Analysis Services](https://docs.microsoft.com/analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance).  
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação instalará os pré-requisitos ainda não instalados na etapa de instalação descrita posteriormente neste procedimento.  
  
     Você também pode especificar um diretório personalizado para componentes compartilhados por meio do campo na parte inferior desta página. Para alterar o caminho de instalação de componentes compartilhados, atualize o caminho no campo fornecido na parte inferior da caixa de diálogo ou clique no botão de reticências para navegar até um diretório de instalação. O caminho de instalação padrão é C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\.  
  
    > [!NOTE]  
    >  Quando você seleciona o recurso Serviços de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] , a replicação e a pesquisa de texto completo são selecionadas automaticamente. Se esses sub-recursos forem desmarcados, o recurso Serviços de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] também será desmarcado.  
  
11. Na página Configuração da Instância, especifique se deseja instalar uma instância padrão ou uma instância nomeada.
  
     **ID da Instância** – Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, marque a caixa de texto **ID da Instância** e forneça um valor.  
  
    > [!NOTE]  
    >  As instâncias autônomas típicas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], sejam elas padrão ou nomeadas, não usam um valor não padrão para a caixa de texto **ID da Instância** .  
  
    > [!IMPORTANT]  
    >  Use a mesma InstanceID para todos os nós que estejam preparados para a instância de cluster de failover  
  
     **Diretório raiz da instância** – por padrão, o diretório raiz da instância é C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]\\. Para especificar um diretório raiz não padrão, use o campo fornecido ou clique no botão de reticências para localizar uma pasta de instalação.  
  
     **Instâncias instaladas** : a grade mostra as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que estão no computador em que a Instalação está sendo executada. Se já existir uma instância padrão instalada no computador, instale uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Clique em **Avançar** para continuar.  
  
12. A página Requisitos de Espaço em Disco calcula o espaço em disco necessário para os recursos especificados e compara os requisitos com o espaço em disco disponível no computador onde a Instalação está sendo executada.  
  
13. Use esta página para especificar a Política de Segurança de Cluster.  
  
    -   [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e versões posteriores: SIDs de serviço (IDs de segurança de servidor) são a configuração padrão e recomendada. Não há nenhuma opção para alterar isso para grupos de segurança. Para obter informações sobre a funcionalidade de SIDs no [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)], consulte [Configurar contas de serviço e permissões do Windows](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). Isso foi testado na instalação autônoma e em cluster no [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)].  
  
    -   No [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)], especifique os grupos de domínios para serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Todas as permissões de recurso são controladas por grupos no nível do domínio que incluem contas de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como membros de grupo.  
  
     Clique em **Avançar** para continuar.  
  
14. O fluxo de trabalho do restante deste tópico depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções.  
  
15. Na página Configuração do Servidor – Contas de Serviço, especifique as contas de logon dos serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os serviços reais configurados nessa página dependem dos recursos selecionados para instalação.  
  
     Você pode atribuir a mesma conta de logon a todos os serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou configurar cada conta de serviço individualmente. O tipo de inicialização é definido como manual para todos os serviços com suporte a cluster, inclusive a pesquisa de texto completo e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, e não pode ser alterado durante a instalação. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda que você configure contas de serviço individualmente para fornecer privilégios mínimos para cada serviço, em que os serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recebem as permissões mínimas para concluir suas tarefas. Para obter mais informações, consulte [Configurar contas de serviço e permissões do Windows](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Para especificar a mesma conta de logon para todas as contas de serviço nessa instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], forneça credenciais nos campos na parte inferior da página.  
  
     **Observação de segurança** [!INCLUDE[ssNoteStrongPass](../../../includes/ssnotestrongpass-md.md)]  
  
     Depois de concluir a especificação de informações de logon para serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Avançar**.  
  
16. Use a guia **Configuração do Servidor — Ordenação** para especificar ordenações não padrão para o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
17. Use **Configuração de Servidor - Filestream** para habilitar o FILESTREAM para a sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  Clique em **Avançar** para continuar.  
  
18. Use a página Configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para especificar o tipo de instalação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] a ser criada. Para instalações da instância de cluster de failover, a opção é definida como instalação Não configurada do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Você deve configurar os serviços do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] depois de concluir a instalação.  
   
19. Na página Relatório de Erros, especifique as informações que você deseja enviar à [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que ajudarão a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por padrão, as opções de relatório de erros estão habilitadas.  
  
20. O Verificador de Configuração do Sistema executa mais um conjunto de regras para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificados.  
  
21. A página Pronto para Instalar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Instalar**. A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
     Durante a instalação, a página Progresso da Instalação fornece o status para que você possa monitorar o progresso da Instalação. Após a instalação, a página **Concluído** fornece um link para o arquivo de log de resumo da instalação e outras observações importantes.  
  
22. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
23. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
24. Repita as etapas anteriores para preparar os outros nós da instância de cluster de failover. Você também pode usar o arquivo de configuração gerado automaticamente para executar a preparação nos outros nós. Para obter mais informações, veja [Instalar o SQL Server 2016 usando um arquivo de configuração](../../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
## <a name="complete"></a>Concluído  
  
#### <a name="advancedenterprise-failover-cluster-instance-install-step-2-complete"></a>Etapa 2 de instalação da instância de cluster de failover avançada/corporativa: Concluído  
  
1.  Após a preparação de todos os nós, conforme descrito na [etapa de preparação](#prepare), execute a Instalação em um dos nós preparados, de preferência no nó que tem o disco compartilhado. Na página **Avançado** da Central de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Conclusão de cluster avançado**.  
  
2.  O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**.  
  
3.  Na página Arquivos de Suporte à Instalação, clique em **Instalar** para instalar os arquivos de suporte à Instalação.  
  
4.  O Verificador de Configuração do Sistema verifica o estado do sistema do computador antes da continuação da instalação. Depois de concluir a verificação, clique em **Avançar** para continuar. Você pode exibir os detalhes na tela clicando em **Mostrar Detalhes**ou como um relatório HTML clicando em **Exibir relatório detalhado**.  
  
5.  Na página de Seleção de Idioma, você pode especificar o idioma da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , se estiver instalando em um sistema operacional localizado, e se a mídia de instalação incluir pacotes do idioma inglês e do idioma correspondente ao sistema operacional. Para obter mais informações sobre suporte em qualquer idioma e considerações sobre instalação, veja [Versões de Idiomas Locais no SQL Server](../../../sql-server/install/local-language-versions-in-sql-server.md).  
  
     Para continuar, clique em **Avançar**.  
  
6.  Use a página Configuração do nó de cluster para selecionar o nome da instância preparada para clustering e especifique o nome da rede da nova instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse é o nome usado para identificar sua instância de cluster de failover na rede.  
  
    > [!NOTE]  
    >  Ele é conhecido como o nome virtual do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em versões anteriores de instâncias de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
7.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executa mais um conjunto de regras baseadas nos recursos selecionados para validar a configuração.  
  
8.  Use a página Grupo de Recursos de Cluster para especificar o nome do grupo de recursos de cluster onde os recursos do servidor virtual do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serão localizados. Para especificar o nome do grupo de recursos de cluster do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Você tem duas opções:  
  
    -   Use a lista para especificar um grupo existente a ser usado.  
  
    -   Digite o nome de um novo grupo a ser criado. Observe que o nome "Armazenamento disponível" não é um nome de grupo válido.  
  
9. Na página Seleção de Disco de Cluster, selecione o recurso de disco de cluster compartilhado para sua instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O disco de cluster é o local onde os dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serão colocados. É possível especificar mais de um disco. A grade Discos compartilhados disponíveis exibe uma lista de discos disponíveis, se cada um deles estiver qualificado como um disco compartilhado, e uma descrição de cada recurso de disco. Clique em **Avançar** para continuar.  
  
    > [!NOTE]  
    >  A primeira unidade é usada como a unidade padrão para todos os bancos de dados, mas é possível alterá-la nas páginas de configuração do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] ou do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
10. Na página Configuração de Rede de Cluster, especifique os recursos de rede para a instância de cluster de failover.  
  
    -   **Configurações de Rede** – especifique o tipo e o endereço IP de todos os nós e sub-redes da instância de cluster de failover. Você pode especificar vários endereços IP para uma instância de cluster de failover com várias sub-redes, mas há suporte apenas para um endereço IP por sub-rede. Cada nó preparado deve ser um possível proprietário de pelo menos um endereço IP. Se você tiver várias sub-redes em sua instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], terá que definir a dependência do recurso de endereço IP como OR.  
  
     Clique em **Avançar** para continuar.  
  
11. O fluxo de trabalho do restante deste tópico depende dos recursos especificados para a instalação. Talvez você não veja todas as páginas, dependendo de suas seleções.  
  
12. Use a página Configuração – Provisionamento de Conta do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para especificar o seguinte:  
  
    -   Modo de Segurança - selecione Autenticação do Windows ou Autenticação de Modo Misto para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se você selecionar Autenticação de Modo Misto, deverá fornecer uma senha forte para a conta interna do administrador de sistema do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
         Depois que um dispositivo estabelecer uma conexão com êxito com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o mecanismo de segurança será o mesmo para Autenticação do Windows e Modo Misto.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Administradores: você deve especificar pelo menos um administrador de sistema para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
     Ao concluir a edição da lista, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
13. Use a página Configuração do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] - Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**.  
  
    > [!IMPORTANT]  
    >  Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os diretórios de dados devem estar localizados no disco de cluster compartilhado da instância de cluster de failover.  
  
  
14. Use a página Configuração do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] - Provisionamento de Conta para especificar usuários ou contas que tenham permissões de administrador para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Especifique pelo menos um administrador de sistema para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está sendo executada, clique em **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
     Ao concluir a edição da lista, [!INCLUDE[clickOK](../../../includes/clickok-md.md)]. Verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
15. Use a página Configuração do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] - Diretórios de Dados para especificar diretórios de instalação não padrão. Para instalar nos diretórios padrão, clique em **Avançar**.  
  
    > [!IMPORTANT]  
    >  Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os diretórios de dados devem estar localizados no disco de cluster compartilhado do cluster de failover.  
  
  
16. O Verificador de Configuração do Sistema executa mais um conjunto de regras para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificados.  
  
17. A página Pronto para Instalar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Instalar**. A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
18. Durante a instalação, a página Progresso da Instalação fornece o status para que você possa monitorar o progresso da Instalação.  
  
19. Após a instalação, a página **Concluído** fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Fechar**. Com essa etapa, todos os nós preparados para a mesma instância de cluster de failover agora fazem parte da instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concluída.  
  
## <a name="next-steps"></a>Próximas etapas  
 **Configure a nova instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** – para reduzir a área da superfície sujeita a ataque de um sistema, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala e habilita seletivamente serviços e recursos chave. Para obter mais informações, consulte [Surface Area Configuration](../../../relational-databases/security/surface-area-configuration.md).  
  
 Para obter mais informações sobre os locais de arquivo de log, consulte [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server 2016 do prompt de comando](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
