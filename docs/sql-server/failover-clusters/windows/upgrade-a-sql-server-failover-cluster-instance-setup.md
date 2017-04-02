---
title: "Atualizar uma inst&#226;ncia de cluster de failover do SQL Server (instala&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "01/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "atualizando clusters"
  - "clusters [SQL Server], atualizando"
  - "clustering de failover [SQL Server], criando clusters"
  - "clusters [SQL Server], criando"
  - "clustering de failover [SQL Server], atualizando"
ms.assetid: ea8b7d66-e5a1-402f-9928-8f7310e84f5c
caps.latest.revision: 63
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 63
---
# Atualizar uma inst&#226;ncia de cluster de failover do SQL Server (instala&#231;&#227;o)
  Você pode atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um cluster de failover do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando a interface de usuário de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou com um prompt de comando.  
  
 Em instalações locais, você deve executar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como um administrador. Se você instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura no compartilhamento remoto.  
  
 Antes de atualizar, veja [Atualizar uma instância de cluster de failover do SQL Server](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md).  
  
##  <a name="UpgradeSteps"></a> Para atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### Para atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Por meio da mídia de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da edição que corresponde à edição que você está atualizando, clique duas vezes em setup.exe na pasta raiz. Talvez você receba uma solicitação para instalar os pré-requisitos, caso eles não tenham sido instalados anteriormente.  
  
2.  Após a instalação dos pré-requisitos, o Assistente de Instalação inicia a Central de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para atualizar uma instância existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]selecione sua instância.  
  
3.  Se os arquivos de suporte da instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] forem necessários, a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] os instalará. Se você for instruído a reiniciar o computador, reinicie-o antes de continuar.  
  
4.  O Verificador de Configuração do Sistema executa uma operação de descoberta no computador. Para continuar, [!INCLUDE[clickOK](../../../includes/clickok-md.md)].  
  
5.  Na página Chave do Produto (Product Key), digite a chave do PID da nova edição da versão correspondente à edição da antiga versão do produto. Por exemplo, para atualizar um cluster de failover do Enterprise, forneça uma chave do PID do [!INCLUDE[ssEnterprise](../../../includes/ssenterprise-md.md)]. Clique em **Avançar** para continuar. Lembre-se de que a chave do PID que você usa para uma atualização de cluster de failover deve ser consistente em todos os nós de cluster de failover na mesma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
6.  Na página Termos de Licença, leia o contrato de licença e marque a caixa de seleção para aceitar os termos e as condições da licença. Para ajudar a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você também pode habilitar a opção de uso de recursos e enviar relatórios à [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. **Clique em Avançar para continuar**. Para finalizar a Instalação, clique em **Cancelar**.  
  
7.  Na página Selecionar Instância, especifique a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a ser atualizada para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. **Clique em Avançar para continuar**.  
  
8.  Na página Seleção de Recursos, os recursos a serem atualizados estão pré-selecionados. Uma descrição de cada grupo de componentes é exibida no painel à direita depois que você seleciona o nome do recurso. Lembre-se de que você não pode alterar os recursos a serem atualizados, nem adicionar recursos durante a operação de atualização. Para adicionar recursos a uma instância atualizada do [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] após a conclusão da operação de atualização, veja [Adicionar recursos a uma instância do SQL Server 2016 &#40;Instalação&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
  
     Os pré-requisitos dos recursos selecionados são exibidos no painel à direita. A Instalação do SQL Server instalará os pré-requisitos que ainda não estiverem instalados durante a etapa descrita posteriormente neste procedimento. Para economizar tempo, você deve instalar previamente esses pré-requisitos em cada nó.  
  
9. Na página Configuração da Instância, os campos são preenchidos automaticamente a partir da instância antiga. Você pode optar por especificar o novo valor de InstanceID.  
  
     **ID da Instância** – Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, marque a caixa de seleção **ID da Instância** e forneça um valor. Se você substituir o valor padrão, deverá especificar a mesma ID de Instância para a instância que está sendo atualizada em todos os nós de cluster de failover. A ID da Instância atualizada deve coincidir em todos os nós.  
  
     **Instâncias e recursos detectados** – A grade mostra as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que estão no computador em que a instalação está sendo executada. **Clique em Avançar para continuar**.  
  
10. A página Requisitos de Espaço em Disco calcula o espaço em disco necessário para os recursos especificados e compara os requisitos com o espaço em disco disponível no computador onde a Instalação está sendo executada.  
  
11. Na página Atualização da Pesquisa de Texto Completo, especifique as opções de atualização para os bancos de dados que estão sendo atualizados. Para obter mais informações, veja [Opções de atualização da Pesquisa de Texto Completo](../Topic/Full-Text%20Search%20Upgrade%20Options.md).  
  
12. Na página **Relatório de Erros** , especifique as informações que deseja enviar à [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que ajudarão a aperfeiçoar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por padrão, as opções de relatório de erros estão habilitadas.  
  
13. O Verificador de Configuração do Sistema executa mais um conjunto de regras para validar a configuração do computador com os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificados antes do início da operação de atualização.  
  
14. A página Relatório de Atualização de Cluster exibe a lista de nós na instância de cluster de failover e as informações de versão de instância dos componentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em cada nó. Ela exibe o status do script de banco de dados e o status do script de replicação. Além disso, ela também exibe mensagens informativas sobre o que ocorrerá quando você clicar em **Avançar**. Dependendo do número de nós de cluster de failover que já foram atualizados e do número total de nós, a instalação exibirá o comportamento de failover que ocorrerá quando você clicar em **Avançar**. Ela também avisará sobre o tempo de inatividade potencialmente desnecessário se você ainda já não tiver instalado os pré-requisitos.  
  
15. A página Pronto para Atualizar mostra uma exibição de árvore das opções de instalação que foram especificadas durante a Instalação. Para continuar, clique em **Atualizar**. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação instalará primeiro os pré-requisitos exigidos para os recursos selecionados, seguidos da instalação dos recursos.  
  
16. Durante a atualização, a página Progresso fornece o status para que você possa monitorar o progresso da atualização no nó atual enquanto a Instalação continua.  
  
17. Depois da atualização do nó atual, a página Relatório de Atualização de Cluster exibe informações sobre o status da atualização de todos os nós de cluster de failover, dos recursos em cada nó de cluster de failover e informações sobre as versões correspondentes. Confirme a informações sobre versão exibidas e continue com a atualização dos nós restantes. Se o failover em nós atualizados tiver ocorrido, isso também será aparente na página de status. Você também pode verificar na ferramenta do administrador de Cluster do Windows para confirmar.  
  
18. Depois da atualização, a página Concluído fornece um link para o arquivo de log de resumo da instalação e outras observações importantes. Para concluir o processo de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , clique em **Fechar**.  
  
19. Se você for instruído a reiniciar o computador, faça-o agora. É importante ler a mensagem do Assistente de Instalação ao concluir a Instalação. Para obter mais informações sobre os arquivos de log da Instalação, veja [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
20. Para concluir o processo de atualização, repita essas etapas em todos os outros nós no cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## Para atualizar um cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
#### Para atualizar para um cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (o cluster existente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não é um cluster de várias sub-redes).  
  
1.  Execute as etapas acima para atualizar seu cluster para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Adicione um nó a uma sub-rede diferente usando a ação de Instalação AddNode e confirme a dependência do recurso de endereço IP para OR na página **Configuração de rede de cluster** . Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
#### Para atualizar um cluster de várias sub-redes que use atualmente V-Lan expansível.  
  
1.  Execute as etapas acima para atualizar seu cluster para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
2.  Altere as configurações de rede para mover o nó remoto para uma sub-rede diferente.  
  
3.  Com a ferramenta de gerenciamento de Cluster de Failover do Windows, adicione um novo endereço IP à nova sub-rede e defina a dependência do recurso de endereço IP como OR.  
  
## Próximas etapas  
 Depois de atualizar para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], conclua as seguintes tarefas:  
  
-   [Concluir a atualização do mecanismo de banco de dados](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)  
  
-   [Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)  
  
-   [Aproveitar os Novos Recursos do SQL Server 2016](../Topic/Take%20Advantage%20of%20New%20SQL%20Server%202016%20Features.md)  
  
## Consulte também  
 [Atualizar uma instância de cluster de failover do SQL Server](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)   
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Adicionar recursos a uma instância do SQL Server 2016 &#40;instalação&#41;](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)  
  
  