---
title: Atualizar uma instância do cluster de failover do SQL Server (configuração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], creating clusters
- clusters [SQL Server], creating
- failover clustering [SQL Server], upgrading
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d018fb391c7633877f985b4e5e0798bfd803a5fc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62680352"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance-setup"></a>Atualizar uma instância de cluster de failover do SQL Server (instalação)
  Você pode atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um cluster de failover do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] com o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou com um prompt de comando.  
  
 Durante a atualização do cluster de failover, o tempo de inatividade está limitado ao tempo necessário à atualização de scripts para execução. Se você seguir o processo de atualização do cluster de failover em andamento, seu tempo de inatividade será mínimo. Se você não tiver todos os pré-requisitos instalados nos nós de cluster de failover, talvez tempo de inatividade adicional seja necessário para instalar esses pré-requisitos. Para obter mais informações sobre como minimizar o tempo de inatividade durante a atualização, consulte a seção [práticas recomendadas antes de atualizar o cluster de failover](#BestPractices) nesta página.  
  
 Para obter mais informações sobre como atualizar, consulte [atualizações de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md) e [atualização para o SQL Server 2014](../../../database-engine/install-windows/upgrade-sql-server.md).  
  
 Para obter mais informações sobre a sintaxe de exemplo para o uso do prompt de comando, consulte [instalar SQL Server 2014 no prompt de comando](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de começar, examine as seguintes informações importantes:  
  
-   [Antes de instalar o cluster de failover](../install/before-installing-failover-clustering.md)  
  
-   [Use o supervisor de atualização para se preparar para atualizações](../../install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
-   [Atualizar o Mecanismo de Banco de Dados](../../../database-engine/install-windows/upgrade-database-engine.md)  
  
-   O .NET Framework 4.0 é instalado em um sistema operacional clusterizado. Para minimizar qualquer possível tempo de inatividade, considere instalar o .NET Framework 4.0 antes de executar a Instalação.  
  
-   Para garantir que o componente Visual Studio seja instalado corretamente, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que você instale uma atualização. A Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verifica a presença dessa atualização e requer o download e a instalação da atualização antes de continuar com a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para evitar a interrupção durante a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , você pode baixar e instalar a atualização antes de executar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , conforme descrito abaixo (ou instalar todas as atualizações para o .NET 3.5 SP1 disponíveis no Windows Update):  
  
     Se você instalar [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] o em um computador com o sistema operacional Windows Server 2008 SP2, poderá obter a atualização necessária [aqui](https://go.microsoft.com/fwlink/?LinkId=198093)  
  
     Se você instalar o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] em um computador com o [!INCLUDE[win7](../../../includes/win7-md.md)] SP1 ou [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] SP1, essa atualização será incluída.  
  
-   O .NET Framework 3.5 SP1 não é mais instalado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], mas pode ser necessário durante a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)]. Para obter mais informações, [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]consulte [notas de versão](https://go.microsoft.com/fwlink/?LinkId=296445).  
  
-   Em instalações locais, você deve executar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura no compartilhamento remoto.  
  
-   Para atualizar uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] cluster de failover do, a instância que está sendo atualizada deve ser um cluster de failover.  
  
     Para mover uma instância autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um cluster de failover do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], instale um novo cluster de failover do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] e depois migre os bancos de dados do usuário da instância autônoma com o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="rolling-upgrades"></a>Atualizações sem interrupção  
 Para atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], você deve executar a instalação com uma ação de atualização em cada um dos nós de cluster de failover de cada vez, começando pelos nós passivos. Conforme você atualiza cada nó, ele é omitido dos possíveis proprietários do cluster de failover. Se houver um failover inesperado, os nós atualizados não participarão do failover até que a propriedade do grupo de recursos de cluster seja movida para um nó atualizado pela Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Por padrão, a Instalação determina quando executar failover em um nó atualizado. Isso depende do número total de nós na instância de cluster de failover e do número de nós que já foram atualizados. Quando a metade ou mais da metade dos nós já tiver sido atualizada, a Instalação provoca um failover em um nó atualizado quando você executa a instalação no próximo nó. Durante o failover em um nó atualizado, o grupo de clusters é movido para um nó atualizado. Todos os nós atualizados são colocados na lista de possíveis proprietários e todos os nós que ainda não foram atualizados são removidos da lista de possíveis proprietários. À medida que você atualiza cada nó restante, ele é omitido dos possíveis proprietários do cluster de failover.  
  
 Esse processo resulta em tempo de inatividade limitado a um tempo de failover e ao tempo de execução do script de atualização do banco de dados durante toda a atualização de cluster de failover.  
  
 Para controlar o comportamento de failover de nós de cluster durante o processo de atualização, execute a operação de atualização no prompt de comando e use o parâmetro /FAILOVERCLUSTERROLLOWNERSHIP. Para obter mais informações, consulte [Install SQL Server 2014 from the Command Prompt](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md) (Instalar o SQL Server 2014 do Prompt de Comando).  
  
 **Observação** Se houver um cluster de failover de nó único, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a instalação levará o grupo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recursos offline.  
  
## <a name="considerations-when-upgrading-from-ssversion2005"></a>Considerações ao fazer a atualização do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]  
 Se você especificou grupos de domínios para a política de segurança de cluster, não poderá especificar o SID de serviço em [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]. Se você quiser usar o SID de serviço, precisará executar uma atualização lado a lado.  
  
 Quando você seleciona o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para atualização, a pesquisa de texto completo é incluída na instalação, independentemente de ter sido ou não instalada no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Se a pesquisa de texto completo foi habilitada no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], a Instalação recompilará o catálogo de pesquisa de texto completo, independentemente das opções disponíveis para você.  
  
## <a name="upgrading-to-a-sssql14-multi-subnet-failover-cluster"></a>Atualizando para um cluster de failover de várias sub-redes do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]  
 Há dois possíveis cenários para atualizações:  
  
1.  O cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está atualmente configurado em uma única sub-rede: você deve atualizar primeiro o cluster existente para o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] iniciando a instalação e seguindo o processo de atualização. Concluída a atualização do cluster de failover existente, adicione um nó que esteja em uma sub-rede diferente usando a funcionalidade AddNode. Confirme a alteração da dependência do recurso de endereço IP para OR na página de configuração de rede de cluster. Agora você tem um cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  O cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está atualmente configurado em várias sub-redes que usam a tecnologia V-LAN expansível: você deve atualizar primeiro o cluster existente para o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. Como a tecnologia V-LAN expansível configura uma única sub-rede, a configuração de rede deve ser alterada para várias sub-redes. Altere a dependência do recurso de endereço IP com a ferramenta de administração de Cluster de Failover do Windows e altere a dependência de IP para OR.  
  
###  <a name="best-practices-before-upgrading-a-ssnoversion-failover-cluster"></a><a name="BestPractices"></a>Práticas recomendadas antes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] atualizar um cluster de failover  
 Para eliminar tempo de inatividade inesperado causado por uma reinicialização, pré-instale o pacote de não reinicialização para .NET Framework 4.0 em todos os nós de cluster de failover antes de executar a atualização nos nós de cluster. É recomendável seguir estas etapas para pré-instalar os pré-requisitos:  
  
-   Instale o pacote de não reinicialização para .NET Framework 4.0 e atualize somente os componentes compartilhados, começando pelos nós passivos. O [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 4.0, o Windows Installer 4.5 e os arquivos de suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] serão instalados.  
  
-   Reinicialize uma ou mais vezes, conforme necessário.  
  
-   Execute failover em um nó atualizado.  
  
-   Atualize os componentes compartilhados no último nó restante.  
  
 Depois que todos os componentes compartilhados estiverem atualizados e os pré-requisitos estiverem instalados, inicie o processo de atualização do cluster de failover. É necessário executar a atualização em cada nó de cluster de failover, começando primeiro com os nós passivos e abrindo caminho até o nó proprietário do grupo de recursos de cluster.  
  
-   Não é possível adicionar recursos a um cluster de failover existente.  
  
-   A alteração da edição do cluster de failover é limitada a determinados cenários. Para obter mais informações, consulte [Atualizações de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
##  <a name="to-upgrade-a-ssnoversion-failover-cluster"></a><a name="UpgradeSteps"></a> Para atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-a-ssnoversion-failover-cluster"></a>Para atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, vá para a pasta raiz no compartilhamento e clique duas vezes em Setup.exe. Talvez você receba uma solicitação para instalar os pré-requisitos, caso eles não tenham sido instalados anteriormente.  
  
2.  > [!IMPORTANT]  
    >  Para obter mais informações sobre as etapas 3 e 4, consulte a seção [práticas recomendadas antes de atualizar o cluster de failover](#BestPractices) .  
  
3.  Após a instalação dos pré-requisitos, o Assistente de Instalação inicia a Central de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para atualizar uma instância existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], clique em **Atualizar [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], ou [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].**  
  
4.  Se os arquivos de suporte à Instalação forem necessários, a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] os instalará. Se você for instruído a reiniciar o computador, reinicie-o antes de continuar.  
  
5.  O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
6.  Na página Chave do Produto (Product Key), digite a chave do PID da nova edição da versão correspondente à edição da antiga versão do produto. Por exemplo, para atualizar um cluster de failover do Enterprise, forneça uma chave do PID do [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]. Clique em **Próximo** para continuar. Lembre-se de que a chave do PID que você usa para uma atualização de cluster de failover deve ser consistente em todos os nós de cluster de failover na mesma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [edições e componentes do SQL Server 2014](../../editions-and-components-of-sql-server-2016.md) e [atualizações de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
7.  Na página Termos de Licença, leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. **Clique em Avançar para continuar**. Para finalizar a Instalação, clique em **Cancelar**.  
  
8.  Na página Selecionar Instância, especifique a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a ser atualizada para o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. **Clique em Avançar para continuar**.  
  
9. Na página Seleção de Recursos, os recursos a serem atualizados estão pré-selecionados. Uma descrição de cada grupo de componentes é exibida no painel à direita depois que você seleciona o nome do recurso. Lembre-se de que você não pode alterar os recursos a serem atualizados, nem adicionar recursos durante a operação de atualização. Para adicionar recursos a uma instância atualizada do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] após a conclusão da operação de atualização, consulte [Adicionar recursos a uma instância do SQL Server 2014 &#40;instalação&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md).  
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. A Instalação do SQL Server instalará os pré-requisitos que ainda não estiverem instalados durante a etapa descrita posteriormente neste procedimento.  
  
10. Na página Configuração da Instância, os campos são preenchidos automaticamente a partir da instância antiga. Você pode optar por especificar o novo valor de InstanceID.  
  
     **ID da instância** – por padrão, o nome da instância é usado como a ID da instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, marque a caixa de seleção **ID da Instância** e forneça um valor. Se você substituir o valor padrão, deverá especificar a mesma ID de Instância para a instância que está sendo atualizada em todos os nós de cluster de failover. A ID da Instância atualizada deve coincidir em todos os nós.  
  
     **Instâncias e recursos detectados** -a grade mostra as [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instâncias do que estão no computador em que a instalação está sendo executada. **Clique em Avançar para continuar**.  
  
11. A página Requisitos de Espaço em Disco calcula o espaço em disco necessário para os recursos especificados e compara os requisitos com o espaço em disco disponível no computador onde a Instalação está sendo executada.  
  
12. Na página Atualização da Pesquisa de Texto Completo, especifique as opções de atualização para os bancos de dados que estão sendo atualizados. Para obter mais informações, veja [Opções de atualização da Pesquisa de Texto Completo](../../install/full-text-search-upgrade-options.md).  
  
13. Na página **relatório de erros** , especifique as informações que você deseja enviar para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que o ajude a melhorar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]o. Por padrão, as opções de relatório de erros estão habilitadas.  
  
14. O Verificador de Configuração do Sistema executa mais um conjunto de regras para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificados antes do início da operação de atualização.  
  
15. A página Relatório de Atualização de Cluster exibe a lista de nós na instância de cluster de failover e as informações de versão de instância dos componentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em cada nó. Ela exibe o status do script de banco de dados e o status do script de replicação. Além disso, ela também exibe mensagens informativas sobre o que ocorrerá quando você clicar em **Avançar**. Dependendo do número de nós de cluster de failover que já foram atualizados e do número total de nós, a instalação exibirá o comportamento de failover que ocorre quando você clica em **Avançar**. Ela também avisará sobre o tempo de inatividade potencialmente desnecessário se você ainda já não tiver instalado os pré-requisitos.  
  
16. A página Pronto para Atualizar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Atualizar**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
17. Durante a atualização, a página Progresso fornece o status para que você possa monitorar o progresso da atualização no nó atual enquanto a Instalação continua.  
  
18. Depois da atualização do nó atual, a página Relatório de Atualização de Cluster exibe informações sobre o status da atualização de todos os nós de cluster de failover, dos recursos em cada nó de cluster de failover e informações sobre as versões correspondentes. Confirme a informações sobre versão exibidas e continue com a atualização dos nós restantes. Se o failover em nós atualizados tiver ocorrido, isso também será aparente na página de status. Você também pode verificar na ferramenta do administrador de Cluster do Windows para confirmar.  
  
19. Depois da atualização, a página Concluído fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
20. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
21. Para concluir o processo de atualização, repita as etapas de 1 a 21 em todos os outros nós no cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="to-upgrade-a-ssnoversion-multi-subnet-failover-cluster"></a>Para atualizar um cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### <a name="to-upgrade-to-a-ssnoversion-multi-subnet-failover-cluster-existing-ssnoversion-cluster-is-a-non-multi-subnet-cluster"></a>Para atualizar para um cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (o cluster existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não é um cluster de várias sub-redes).  
  
1.  Siga as etapas de 1 a 24 descritas na seção [para atualizar um cluster de failover SQL Server](#UpgradeSteps) acima para atualizar o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]cluster para o.  
  
2.  Adicione um nó a uma sub-rede diferente usando a ação de Instalação AddNode e confirme a dependência do recurso de endereço IP para OR na página **Configuração de rede de cluster** . Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de Failover SQL Server &#40;instalação&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
#### <a name="to-upgrade-a-multi-subnet-cluster-currently-using-stretch-v-lan"></a>Para atualizar um cluster de várias sub-redes que use atualmente V-Lan expansível.  
  
1.  Siga as etapas de 1 a 24 descritas na seção [para atualizar um cluster de failover SQL Server](#UpgradeSteps) acima para atualizar o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]cluster para o.  
  
2.  Altere as configurações de rede para mover o nó remoto para uma sub-rede diferente.  
  
3.  Com a ferramenta de gerenciamento de Cluster de Failover do Windows, adicione um novo endereço IP à nova sub-rede e defina a dependência do recurso de endereço IP como OR.  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de atualizar para o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], conclua as seguintes tarefas:  
  
-   Registre os servidores  
  
     A atualização remove as configurações do Registro da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior. Depois de atualizar, você deve registrar os servidores novamente.  
  
-   Atualizar estatísticas  
  
     Para ajudar a otimizar o desempenho de consultas, é recomendável atualizar as estatísticas em todos os bancos de dados após a atualização. Use o procedimento armazenado **sp_updatestats** para atualizar as estatísticas em tabelas definidas pelo usuário nos bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Configure a nova instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
     Para reduzir a área da superfície de um sistema vulnerável a ataques, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala e habilita seletivamente serviços e recursos essenciais. Para obter mais informações sobre a configuração da área de superfície, consulte o arquivo leiame desta versão.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server 2014 no prompt de comando](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
