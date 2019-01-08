---
title: Configurar o serviço Integration Services como um recurso de Cluster | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 367835aa-9855-4791-a989-b3d08402ad4c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0bd0382906d3ee56055cc026036816af64b55dc6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408953"
---
# <a name="configure-the-integration-services-service-as-a-cluster-resource"></a>Configurar o serviço Integration Services como um recurso de cluster
  Para os clientes que chegaram à conclusão de que as vantagens dessa configuração do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] como um recurso de cluster sobrepõem-se às desvantagens, esta seção contém as instruções de configuração necessárias. Entretanto, o [!INCLUDE[msCoName](../includes/msconame-md.md)] não recomenda que o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] seja configurado como um recurso de cluster.  
  
 Para configurar o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] como um recurso de cluster, é necessário concluir as tarefas a seguir.  
  
-   Instale o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um cluster.  
  
     Para instalar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um cluster, instale o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em cada nó do cluster.  
  
-   Configure o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] como um recurso de cluster.  
  
     Com o Integration Services instalado em cada nó do cluster, é preciso configurar o Integration Services como um recurso de cluster. Ao configurar o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] como um recurso de cluster, você pode adicionar o serviço ao mesmo grupo de recursos do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]ou a outro grupo. A tabela a seguir descreve as possíveis vantagens e desvantagens na seleção de um grupo de recursos.  
  
    |Quando o Integration Services e o SQL Server estão no mesmo grupo de recursos|Quando o Integration Services e o SQL Server estão em grupos de recursos diferentes|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |Os computadores cliente podem usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para gerenciar os pacotes armazenados no banco de dados msdb, porque os serviços [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] são executados no mesmo servidor virtual. Esta configuração evita os problemas de delegação do cenário de salto duplo.|Os computadores cliente não podem usar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para gerenciar os pacotes armazenados no banco de dados msdb. O cliente pode conectar-se ao servidor virtual no qual o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está em execução. Entretanto, esse computador não pode delegar as credenciais do usuário ao servidor virtual no qual o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução. Esse processo é conhecido como um cenário de salto duplo.|  
    |O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] compete com outros serviços [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por recursos da CPU e outros recursos do computador.|O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não compete com outros serviços [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por recursos da CPU e outros recursos do computador, porque os diferentes grupos de recursos são configurados em nós diferentes.|  
    |As ações de carregar e salvar pacotes no banco de dados msdb são mais rápidas e geram menos tráfego de rede, pois os dois serviços estão em execução no mesmo computador.|As ações de carregar e salvar pacotes no banco de dados msdb podem ser mais lentas e gerar mais tráfego de rede.|  
    |Os dois serviços estão online ou offline ao mesmo tempo.|O serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] pode estar online enquanto o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] estiver offline. Assim, os pacotes armazenados no banco de dados msdb do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] não estão disponíveis.|  
    |O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não poderá ser movido rapidamente para outro nó, se necessário.|O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] pode ser movido mais rapidamente para outro nó, se necessário.|  
  
     Depois de decidir a qual grupo de recursos o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]será adicionado, configure o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] como um recurso de cluster nesse grupo.  
  
-   Configure o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e o repositório de pacotes.  
  
     Ao configurar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] como um recurso de cluster, é preciso modificar o local e o conteúdo do arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em cada nó no cluster. Essas modificações disponibilizam tanto o arquivo de configuração quanto o repositório de pacotes para todos os nós se houver um failover. Depois de modificar o local e o conteúdo do arquivo de configuração, coloque o serviço online.  
  
-   Coloque o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] online como um recurso de cluster.  
  
 Depois de configurar o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um cluster, ou em algum servidor, será preciso configurar as permissões DCOM antes de estabelecer conexão com o serviço por meio de um computador cliente. Para obter mais informações, consulte [Conectar-se a um servidor remoto do Integration Services &#40;Serviço SSIS&#41;](../../2014/integration-services/connect-to-a-remote-integration-services-server-ssis-service.md).  
  
 O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não pode delegar credenciais. Portanto, você não pode usar o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para gerenciar os pacotes armazenados no banco de dados msdb quando as seguintes condições forem verdadeiras:  
  
-   Os serviços [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] estão em execução em servidores separados ou servidores virtuais.  
  
-   O [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] está sendo executado por um terceiro computador.  
  
 O cliente pode conectar-se ao servidor virtual no qual o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está em execução. Entretanto, esse computador não pode delegar as credenciais do usuário ao servidor virtual no qual o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução. Esse processo é conhecido como um cenário de salto duplo.  
  
### <a name="to-install-integration-services-on-a-cluster"></a>Para instalar o Integration Services em um cluster  
  
1.  Instale e configure um cluster com um ou mais nós.  
  
2.  (Opcional) Instale serviços clusterizados, como o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].  
  
3.  Instale o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em cada nó do cluster.  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>Para configurar o Integration Services como um recurso de cluster  
  
1.  Abra o **Administrador de Cluster**.  
  
2.  Na árvore de console, selecione a pasta Grupos.  
  
3.  No painel de resultados, selecione o grupo ao qual deseja adicionar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
    -   Para adicionar o Integrations Services como um recurso de cluster ao mesmo grupo de recursos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], selecione o grupo ao qual o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pertence.  
  
    -   Para adicionar o Integrations Services como um recurso de cluster a um grupo diferente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], selecione outro grupo que não seja aquele ao qual o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pertence.  
  
4.  No menu **Arquivo** , aponte para **Novo**e clique em **Recurso**.  
  
5.  Na página **Novo Recurso** do Assistente de Recurso, digite um nome e selecione **"Serviço Genérico"** como o **Tipo de Serviço**. Não altere o valor de **Grupo**. Clique em **Avançar**.  
  
6.  Na página **Possíveis Proprietários** , adicione ou remova os nós do cluster como os possíveis proprietários do recurso. Clique em **Avançar**.  
  
7.  Para adicionar dependências, na página **Dependências** , selecione um recurso em **Recursos disponíveis**e clique em **Adicionar**. Caso ocorra um failover, tanto o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] quanto o disco compartilhado que armazena os pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] devem retornar ao estado online antes que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fique online. Depois de selecionar as dependências, clique em **Avançar**.  
  
     Para obter mais informações, consulte [Adicionar dependências a um recurso do SQL Server](../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md).  
  
8.  Na página **Parâmetros de Serviço Genérico** , insira **MsDtsServer** como o nome do serviço. Clique em **Avançar**.  
  
9. Na página **Replicação de Registro** , clique em **Adicionar** para adicionar a chave do Registro que identifica o local do arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Este arquivo deve estar localizado em um disco compartilhado que esteja no mesmo grupo de recursos do serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
10. Na caixa de diálogo **Chave do Registro** , digite **SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile**. Clique em **OK**e em **Concluir**.  
  
     O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] agora foi adicionado como um recurso de cluster.  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>Para configurar o serviço Integration Services e o repositório de pacotes  
  
1.  Localize o arquivo de configuração em %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml. Copie-o no disco compartilhado do grupo ao qual você adicionou o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  No disco compartilhado, crie uma nova pasta chamada **Pacotes** para servir como o local do repositório de pacotes. Conceda as permissões de gravação e pastas de listas na nova pasta para usuários e grupos apropriados.  
  
3.  No disco compartilhado, abra o arquivo de configuração em um editor de texto ou XML. Altere o valor do elemento `ServerName` para o nome do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] virtual que é igual ao grupo de recursos.  
  
4.  Altere o valor da `StorePath` elemento para o caminho totalmente qualificado do **pacotes** pasta criada no disco compartilhado em uma etapa anterior.  
  
5.  Atualize o valor de **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** no Registro para o caminho totalmente qualificado e o nome do arquivo de configuração de serviço no disco compartilhado.  
  
### <a name="to-bring-the-integration-services-service-online"></a>Para colocar o serviço do Integration Services online  
  
-   No **Administrador de Cluster**, selecione o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , clique com o botão direito do mouse e selecione **Colocar Online** no menu pop-up. Agora, o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está online como um recurso de cluster.  
  
  
