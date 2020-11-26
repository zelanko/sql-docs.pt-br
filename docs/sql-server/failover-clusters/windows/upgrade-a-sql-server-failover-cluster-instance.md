---
title: Atualizar uma instância de cluster de failover
description: Etapas para fazer upgrade de uma instância de cluster de failover do SQL Server Always On usando a mídia de instalação. Saiba mais sobre como realizar atualizações sem interrupção e a atualização de um cluster de várias sub-redes.
ms.custom: seo-lt-2019
ms.date: 11/21/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover cluster instances
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: cawrites
ms.author: chadam
ms.openlocfilehash: cad44bde76e3915aeb5f99d8eeb415d89b02359e
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127579"
---
# <a name="upgrade-a-failover-cluster-instance"></a>Atualizar uma instância de cluster de failover 
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte ao upgrade de um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uma nova versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], para um novo service pack ou atualização cumulativa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou ao instalar um novo service pack ou atualização cumulativa do serviço Windows separadamente em todos os nós de cluster de failover, com tempo de inatividade limitado a um único failover manual (ou dois failovers manuais, em caso de failback para a primária original).  

  
 Não há suporte para fazer upgrade do sistema operacional Windows Server de um nó contendo uma instância de cluster de failover em sistemas operacionais anteriores ao [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)]. Para fazer upgrade de um nó de cluster de failover do Windows Server em execução no [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] ou posterior, confira [Realizar um upgrade ou uma atualização sem interrupção](#perform-a-rolling-upgrade-or-update).  
  
 Os detalhes do suporte são os seguintes:  
  
-   Há suporte para a atualização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por meio da interface do usuário e do prompt de comando. Você pode executar o upgrade pelo prompt de comando em cada nó de cluster de failover ou usando a interface do usuário de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para atualizar cada nó de cluster. Para obter mais informações, consulte:

   - Instalar uma nova instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]
   - [Instalar o SQL Server do prompt de comando](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

-   Os cenários a seguir não têm suporte como parte de uma atualização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
    -   Não é possível fazer upgrade de uma instância autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uma instância de cluster de failover.  
  
    -   Não é possível adicionar recursos a uma instância de cluster de failover. Por exemplo, você não pode adicionar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a uma instância de cluster de failover somente do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
    -   Não é possível fazer downgrade de uma instância de cluster de failover para uma instância autônoma em nenhum nó do cluster de failover do Windows Server.  
  
    -   A alteração da edição da instância de cluster de failover é limitada a determinados cenários. Para obter mais informações, consulte [Atualizações de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
-   Durante o upgrade da instância de cluster de failover, o tempo de inatividade estará limitado ao tempo de failover e ao tempo necessário para que os scripts de upgrade sejam executados. Se você seguir o processo de atualização sem interrupção da instância de cluster de failover abaixo e cumprir todos os pré-requisitos em todos os nós antes de começar o processo de upgrade, o tempo de inatividade será mínimo. O upgrade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando as tabelas com otimização de memória estiverem em uso levará um pouco mais de tempo. Para saber mais, confira [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de começar, examine as seguintes informações importantes:  
  
-   [Atualizações compatíveis de versão e edição](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): Verifique se você pode atualizar para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] de sua versão do sistema operacional Windows e da versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por exemplo, não é possível fazer upgrade diretamente de uma instância de clustering de failover do SQL Server 2005 para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ou fazer upgrade de uma instância de cluster de failover em execução no [!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)].  
  
-   [Escolher um método de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): selecione o método e as etapas de atualização apropriados com base em sua análise de atualizações de versão e de edição com suporte e também com base em outros componentes instalados em seu ambiente a fim de atualizar os componentes na ordem correta.  
  
-   [Planejar e testar o plano de atualização do mecanismo de banco de dados](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): Analise as notas de versão e os problemas conhecidos da atualização, a lista de verificação pré-atualização, e desenvolva e teste o plano de atualização.  
  
-   [Requisitos de hardware e software para a instalação do SQL Server](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md):  Analise os requisitos de software para a instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se for necessário um software adicional, instale-o em cada nó antes de começar o processo de atualização para minimizar qualquer tempo de inatividade.  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>Realizar uma atualização ou atualização sem interrupção  
 Para fazer upgrade de uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], use a configuração do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para fazer upgrade de cada nó participante da instância de cluster de failover, um por vez, começando com os nós passivos. Conforme você faz upgrade de cada nó, ele é omitido dos possíveis proprietários da instância de cluster de failover. Se houver um failover inesperado, os nós atualizados não participarão do failover até que a propriedade da função do cluster de failover do Windows Server seja movida para um nó atualizado pela instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] determina quando executar failover em um nó atualizado. Isso depende do número total de nós na instância de cluster de failover e do número de nós que já foram atualizados. Quando a metade ou mais da metade dos nós já tiver sido atualizada, a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provocará um failover em um nó atualizado quando você executar a atualização no próximo nó. Durante o failover em um nó atualizado, o grupo de clusters é movido para um nó atualizado. Todos os nós atualizados são colocados na lista de possíveis proprietários e todos os nós que ainda não foram atualizados são removidos da lista de possíveis proprietários. Conforme você fizer upgrade de cada nó restante, ele será adicionado aos possíveis proprietários da instância de cluster de failover.  
  
 Esse processo resulta em tempo de inatividade limitado a um tempo de failover e ao tempo de execução do script de atualização do banco de dados durante toda a atualização de cluster de failover.  
  
 Para controlar o comportamento de failover de nós de cluster durante o processo de atualização, execute a operação de atualização no prompt de comando e use o parâmetro /FAILOVERCLUSTERROLLOWNERSHIP. Para obter mais informações, consulte [Instalar o SQL Server por meio do prompt de comando](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  

 ## <a name="upgrade-with-installation-media"></a>Atualizar com mídia de instalação 
  
1.  Por meio da mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da edição que corresponde à edição que você está atualizando, clique duas vezes em setup.exe na pasta raiz. Talvez você receba uma solicitação para instalar os pré-requisitos, caso eles não tenham sido instalados anteriormente.  
  
2.  Após a instalação dos pré-requisitos, o Assistente de Instalação inicia a Central de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para atualizar uma instância existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]selecione sua instância.  
  
3.  Se os arquivos de suporte da instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] forem necessários, a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] os instalará. Se você for instruído a reiniciar o computador, reinicie-o antes de continuar.  
  
4.  O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
5.  Na página Chave do Produto (Product Key), digite a chave do PID da nova edição da versão correspondente à edição da antiga versão do produto. Por exemplo, para atualizar um cluster de failover do Enterprise, forneça uma chave do PID do [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]. Clique em **Avançar** para continuar. Lembre-se de que a chave do PID que você usa para uma atualização de cluster de failover deve ser consistente em todos os nós de cluster de failover na mesma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
6.  Na página Termos de Licença, leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. **Clique em Avançar para continuar**. Para finalizar a Instalação, clique em **Cancelar**.  
  
7.  Na página Selecionar Instância, especifique a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a ser atualizada para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. **Clique em Avançar para continuar**.  
  
8.  Na página Seleção de Recursos, os recursos a serem atualizados estão pré-selecionados. Uma descrição de cada grupo de componentes é exibida no painel à direita depois que você seleciona o nome do recurso. Lembre-se de que você não pode alterar os recursos a serem atualizados, nem adicionar recursos durante a operação de atualização. Para adicionar recursos a uma instância atualizada do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] após a conclusão da operação de atualização, veja [Adicionar recursos a uma instância do SQL Server 2016 &#40;instalação&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md).  
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. A Instalação do SQL Server instalará os pré-requisitos que ainda não estiverem instalados durante a etapa descrita posteriormente neste procedimento. Para economizar tempo, você deve instalar previamente esses pré-requisitos em cada nó.  
  
9. Na página Configuração da Instância, os campos são preenchidos automaticamente a partir da instância antiga. Você pode optar por especificar o novo valor de InstanceID.  
  
     **ID da Instância** – Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, marque a caixa de seleção **ID da Instância** e forneça um valor. Se você substituir o valor padrão, deverá especificar a mesma ID de Instância para a instância que está sendo atualizada em todos os nós de cluster de failover. A ID da Instância atualizada deve coincidir em todos os nós.  
  
     **Instâncias e recursos detectados** – A grade mostra as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que estão no computador em que a instalação está sendo executada. **Clique em Avançar para continuar**.  
  
10. A página Requisitos de Espaço em Disco calcula o espaço em disco necessário para os recursos especificados e compara os requisitos com o espaço em disco disponível no computador onde a Instalação está sendo executada.  
  
11. Na página Atualização da Pesquisa de Texto Completo, especifique as opções de atualização para os bancos de dados que estão sendo atualizados. Para obter mais informações, veja [Opções de atualização da Pesquisa de Texto Completo](../../../database-engine/install-windows/install-sql-server.md).  
  
12. Na página **Relatório de Erros** , especifique as informações que deseja enviar à [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que ajudarão a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por padrão, as opções de relatório de erros estão habilitadas.  
  
13. O Verificador de Configuração do Sistema executa mais um conjunto de regras para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificados antes do início da operação de atualização.  
  
14. A página Relatório de Atualização de Cluster exibe a lista de nós na instância de cluster de failover e as informações de versão de instância dos componentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em cada nó. Ela exibe o status do script de banco de dados e o status do script de replicação. Além disso, ela também exibe mensagens informativas sobre o que ocorrerá quando você clicar em **Avançar**. Dependendo do número de nós de cluster de failover que já foram atualizados e do número total de nós, a instalação exibirá o comportamento de failover que ocorrerá quando você clicar em **Avançar**. Ela também avisará sobre o tempo de inatividade potencialmente desnecessário se você ainda já não tiver instalado os pré-requisitos.   
  
15. A página Pronto para Atualizar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Atualizar**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
16. Durante a atualização, a página Progresso fornece o status para que você possa monitorar o progresso da atualização no nó atual enquanto a Instalação continua.  
  
17. Depois da atualização do nó atual, a página Relatório de Atualização de Cluster exibe informações sobre o status da atualização de todos os nós de cluster de failover, dos recursos em cada nó de cluster de failover e informações sobre as versões correspondentes. Confirme a informações sobre versão exibidas e continue com a atualização dos nós restantes. Se o failover em nós atualizados tiver ocorrido, isso também será aparente na página de status. Você também pode verificar na ferramenta do administrador de Cluster do Windows para confirmar.  
  
18. Depois da atualização, a página Concluído fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
19. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
20. Para concluir o processo de upgrade, repita as etapas em todos os outros nós da instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="upgrade-a-multi-subnet-failover-cluster-instance"></a>Fazer upgrade de uma instância de cluster de failover com várias sub-redes  

Siga estas etapas para fazer upgrade de sua instância de cluster de failover do Always On em um ambiente com várias sub-redes. 
  
### <a name="to-upgrade-to-a-ssnoversion-multi-subnet-failover-cluster-instance-existing-ssnoversion-cluster-is-a-non-multi-subnet-cluster"></a>Para fazer upgrade para uma instância de cluster de failover com várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (o cluster existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não é um cluster com várias sub-redes).  
  
1.  Siga as etapas acima para fazer upgrade de sua instância de cluster de failover.  
  
2.  Para adicionar um novo nó a uma sub-rede diferente usando a ação de Instalação AddNode e confirmar a dependência do recurso de endereço IP como OR na página **Configuração de rede de cluster**. Confira mais informações em [Adicionar ou remover nós em uma instância de cluster de failover do Always On (Instalação)](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
### <a name="to-upgrade-a-multi-subnet-failover-cluster-instance-currently-using-stretch-vlan-to-use-multi-subnet"></a>Para fazer upgrade de uma instância de cluster de failover com várias sub-redes usando atualmente a VLAN Stretch para usar várias sub-redes.  
  
1.  Execute as etapas acima para atualizar seu cluster para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Altere as configurações de rede para mover o nó remoto para uma sub-rede diferente.  
  
3.  Usando o Gerenciador de Cluster de Failover ou o PowerShell, adicione um novo endereço IP à nova sub-rede para definir a dependência do recurso de endereço IP como OR.  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de atualizar para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], conclua as seguintes tarefas:  
  
-   [Concluir a atualização do mecanismo de banco de dados](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [Aproveitar os Novos Recursos do SQL Server 2016](../../what-s-new-in-sql-server-2017.md)  
  

  
