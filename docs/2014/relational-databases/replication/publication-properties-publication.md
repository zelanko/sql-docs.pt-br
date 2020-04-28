---
title: Propriedades da publicação do Replicação do SQL Server-| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql12.rep.newpubwizard.pubproperties.datapartitions.f1
- sql12.rep.newpubwizard.pubproperties.filterrows.f1
- sql12.rep.newpubwizard.pubproperties.internetsynchronization.f1
- sql12.rep.newpubwizard.pubproperties.general.f1
- sql12.rep.newpubwizard.pubproperties.publicationaccesslist.f1
- sql12.rep.newpubwizard.pubproperties.snapshotformat.f1
helpviewer_keywords:
- Publication Properties dialog box
ms.assetid: 66e845e9-1308-4288-9110-ad2f22f1fc58
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19fee33c63b1287e43077640f381d4b57f489535
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "80380717"
---
# <a name="sql-server-replication-publication-properties"></a>Propriedades da publicação do Replicação do SQL Server 
  Esta seção fornece informações sobre todas as páginas da caixa de diálogo **Propriedades da publicação** . 

## <a name="general"></a>Geral
  A página **Geral** da caixa de diálogo **Propriedades de Publicação** contém informações básicas sobre a publicação, incluindo nome, descrição e a política de validade da assinatura.  
  
### <a name="options"></a>Opções  
 **Nome**  
 O nome da publicação (somente leitura).  
  
 **Backup de banco de dados**  
 O nome do banco de dados de publicação (somente leitura).  
  
 **Descrição**  
 A descrição da publicação.  
  
 **Tipo**  
 O tipo da publicação (somente leitura).  
  
 **Validade da assinatura**  
 Selecione uma das opções para término da assinatura: **Assinaturas nunca expiram** ou **Assinaturas expiram** com um período explícito (**intervalo**).  
  
 Para publicações de instantâneo e transacionais, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você aceite o padrão de **As assinaturas nunca expiram**.  
  
 Para replicação de mesclagem, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda que você aceite o padrão de **As assinaturas nunca expiram** e defina um valor o mais baixo possível para o **Intervalo**. Como o período de validade da assinatura aumenta, o mesmo ocorre com os metadados armazenados, que podem afetar desempenho. Equilibre a necessidade de desconectar os Assinantes ou simplesmente não sincronize por um período estendido em questões de desempenho potencial de armazenamento e processamento de grande quantidade de metadados.  
  
 Para obter mais informações, consulte [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
 **Nível de compatibilidade**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores somente; só publicações de mesclagem. Selecione versão mínima requerida do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Assinantes que sincronizam com essa publicação. Há várias regras associadas com a determinação do nível de compatibilidade.  

## <a name="filter-rows"></a>Filtrar Linhas

  A página **Filtrar Linhas** da caixa de diálogo **Propriedades de Publicação** permite adicionar, editar ou excluir e permite também:  
  
-   Aplicar filtros de linhas estáticos a artigos de tabela em publicações de instantâneo, transacional e de mesclagem.    
-   Aplicar filtros de linha com parâmetros a artigos de tabela em publicações de mesclagem.    
-   Usar filtros de junção para estender filtros em artigos de tabela de mesclagem para artigos de tabela relacionados.  
  
 Para obter mais informações sobre opções de filtragem, consulte [Filter Published Data](publish/filter-published-data.md) (Filtrar dados publicados).  
  
> [!NOTE]  
>  A adição, edição ou exclusão de filtros requer um novo instantâneo para a publicação e requer que todas as assinaturas sejam reiniciadas.  
  
 Para maximizar o desempenho do aplicativo e reduzir a quantidade de uma armazenagem remota requerida ou restringir a disponibilidade de certos dados a Assinantes específicos, somente os dados requeridos devem ser publicados. Sua publicação pode incluir as tabelas filtradas e não filtradas. Por exemplo, você pode incluir a tabela completa (não filtrada) de produtos da empresa e usar filtros de linha para fornecer uma tabela filtrada aos clientes de uma região específica. Filtrando dados publicados, você pode:  
  
-   Minimizar a quantidade de dados enviada pela rede.    
-   Reduzir a quantidade de espaço de armazenamento requerida no Assinante.    
-   Personalizar publicações e aplicativos com base em requisitos de Assinante individuais.    
-   Evitar ou reduzir conflitos se o Assinante estiver atualizando dados, porque partições diferentes de dados podem ser enviadas a Assinantes diferentes (dois Assinantes não estarão atualizando os mesmos valores de dados).    
-   Evitar transmitir dados confidenciais. Podem ser usados filtros de linha e filtros de coluna para restringir um acesso de Assinante aos dados. Para a replicação de mesclagem, haverá considerações de segurança se você usar um filtro com parâmetros que inclua HOST_NAME(). Para obter mais informações, consulte a seção "Filtrando com HOST_NAME()" em [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md).  
  
### <a name="options"></a>Opções  
 **Tabelas Filtradas**  
 Esse painel é populado com filtros à medida que são adicionados a artigos de tabela na publicação. Tabelas com filtros de linha são mostradas como nós de alto nível no painel. Para publicações de mesclagem, tabelas para as quais a filtragem foi estendida através de um filtro de junção são mostradas como nós filhos.  
  
 **Adicionar**  
 Clique em **Adicionar** para iniciar uma caixa de diálogo que permite filtrar artigos de tabela. Clicar em **Adicionar** para um instantâneo ou uma publicação transacional inicia imediatamente uma caixa de diálogo. Clicar em **Adicionar** para uma publicação de mesclagem exibe três opções: **Adicionar Filtro**; **Adicionar junção para estender o filtro selecionado**; **Gerar filtros automaticamente**.  
  
-   Selecione **Adicionar Filtro** para iniciar a caixa de diálogo **Adicionar filtro** . Essa caixa de diálogo permite aplicar filtros de linha a um artigo de tabela. Na caixa de diálogo **Adicionar Filtro** você pode, por exemplo, especificar que uma tabela com dados de cliente só contenha dados de clientes franceses quando for replicada para Assinantes.  
  
-   Selecione **Adicionar Junção para Estender o Filtro Selecionado** para iniciar a caixa de diálogo **Adicionar Junção** . A caixa de diálogo **Adicionar Junção** permite estender um filtro de linha para que filtre linhas em tabelas relacionadas à tabela com filtro de linha. Por exemplo, se uma tabela de cliente for filtrada para que contenha apenas dados de clientes franceses e houver uma tabela relacionada para pedidos de clientes, você pode definir uma junção entre as duas tabelas para que a tabela de pedidos só inclua pedidos de clientes franceses.  
  
    > [!NOTE]  
    >  Essa opção só estará disponível se você selecionar primeiro  a tabela base da junção no painel de filtro.  
  
-   Selecione **Gerar Filtros Automaticamente** para iniciar a caixa de diálogo **Gerar Filtros** . Essa caixa de diálogo permite definir um filtro de linha em uma tabela em uma publicação de mesclagem para que a replicação se estenda automaticamente a outras tabelas relacionadas por relações de chave estrangeira. Por exemplo, uma publicação pode incluir três tabelas: uma tabela de cliente, uma tabela de pedidos (com uma chave estrangeira para a tabela de cliente), e uma tabela de detalhes do pedido (com uma chave estrangeira para a tabela de pedidos). Defina um filtro de linha na tabela de cliente e replicação o estenderá às outras tabelas.  
  
    > [!NOTE]  
    >  Quando os filtros são gerados automaticamente por replicação, qualquer filtro existente na publicação é excluído. Para incluir os filtros gerados automaticamente e um especificado manualmente, gere os filtros primeiro. Você só pode especificar um conjunto de filtros gerado automaticamente para cada publicação.  
  
 **Editar**  
 Selecione um filtro de linha ou um filtro de junção no painel de filtros e clique em **Editar** para iniciar a caixa de diálogo **Editar Filtro** ou **Editar Junção** .  
  
 **Delete (excluir)**  
 Selecione um filtro de linha ou um filtro de junção no painel de filtro e clique em **Excluir** para excluir o filtro.  
  
 **Localizar Tabela**  
 Somente publicações de mesclagem. Clique em **Localizar Tabela** para localizar uma tabela em uma árvore de filtro complexa. Em um banco de dados com relações complexas, pode haver junção de uma tabela com várias tabelas e, portanto, ela pode aparecer em mais de um lugar na árvore de filtro.  
  
 A tabela real só aparece em um lugar na árvore; em outros lugares a tabela é representada por um atalho. Um atalho para uma tabela é somente uma referência à tabela; ele não mostra os nós filhos da tabela. Um nó de atalho é marcado com uma seta de atalho e expandir esse nó mostra o texto **Clique em localizar tabela para ver a tabela \<tablename>** .  
  
 Selecione um nó de atalho no painel e clique em **Localizar Tabela** . O painel é expandido e a tabela é destacada. Se você clicar em **Localizar Tabela** sem um nó de atalho selecionado, uma caixa de diálogo **Localizar Tabela** será ativada.  
  
 **Filter**  
 Contém a definição [!INCLUDE[tsql](../../includes/tsql-md.md)] para o filtro selecionado no painel de filtro.  

## <a name="ftp-snapshot-and-internet"></a>Instantâneo de FTP e Internet
  
Essa página permite:  
  
-   Definir propriedades de entrega do instantâneo por FTP (File Transfer Protocol). Para obter mais informações, consulte [transferir instantâneos por meio](transfer-snapshots-through-ftp.md) da documentação do Windows FTP para obter mais informações.  
  
    > [!NOTE]  
    >  Alterações em qualquer configuração do FTP exigem que um novo instantâneo seja gerado.  
  
-   Definir propriedades de sincronização da Web para replicação de mesclagem no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, que permite que as assinaturas sejam sincronizadas pelo HTTPS (protocolo de transferência segura de hipertexto). Para usar sincronização da Web, você deve configurar um servidor IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
### <a name="options"></a>Opções  
 **Acessar arquivos de instantâneo via FTP**  
 Selecione **Permitir que os Assinantes baixem os arquivos de instantâneo usando FTP**e especifique **Nome do servidor FTP**, **Número da porta**, **Caminho da pasta raiz de FTP**, **Logon**e **Senha**, para permitir que os Assinantes usem o FTP para entrega de instantâneo.  
  
 Essa opção permite que os Assinantes usem o FTP para recuperar arquivos de instantâneo, mas não exige que isso seja feito. Se você selecionar essa opção, o Assistente para Nova Assinatura será padronizado para que o Assinante recupere arquivos de instantâneo pelo FTP. Para alterar a configuração, use a caixa de diálogo **Propriedades da Assinatura** . Se você permitir que os Assinantes acessem arquivos de instantâneo pelo FTP, especifique a pasta de FTP como o local de arquivos de instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades da Assinatura** . Essa ação fará com que o Agente de Instantâneo atualize os arquivos na pasta do FTP automaticamente quando um novo instantâneo for gerado. Se o local para a pasta do FTP não for definido, você terá de atualizar os arquivos manualmente quando novos instantâneos forem gerados. Para obter mais informações, consulte [Deliver a Snapshot Through FTP](publish/deliver-a-snapshot-through-ftp.md) (Entregar um instantâneo por meio de FTP).  
  
 **Sincronização da Web**  
 Somente replicação de mesclagem. Selecione **Permitir que os Assinantes sincronizem por meio da conexão com um servidor Web**e especifique um endereço de servidor Web para permitir que Assinantes de mesclagem usem a sincronização da Web. O servidor Web deve usar protocolo SSL (Secure Sockets Layer) e o endereço Web precisa ser totalmente qualificado, como `https://server.domain.com/synchronize`. Para obter mais informações, consulte [Configurar sincronização da Web](configure-web-synchronization.md).  

## <a name="publication-access-list"></a>Lista de acesso à publicação

  A página **Lista de Acesso à Publicação** da caixa de diálogo **Propriedades de Publicação** permite adicionar e remover logons, contas e grupos da PAL (Lista de Acesso à Publicação). A PAL é o mecanismo primário de segurança do Publicador. Quando você cria uma publicação, a replicação cria uma PAL para a publicação. A PAL, cuja função é semelhante à lista de controle de acesso do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, contém uma lista de logons, contas e grupos com acesso garantido à publicação.  
  
 Quando um Assinante se conecta ao Publicador ou ao Distribuidor e solicita acesso à publicação, o logon do Assinante é comparado com as informações de autenticação na PAL. Isso fornece segurança adicional ao Publicador, impedindo que o logon do Publicador e do Distribuidor seja usado por uma ferramenta cliente para executar modificações no Publicador diretamente. Para obter mais informações, consulte [Secure the Publisher](security/secure-the-publisher.md) (Proteger o publicador).  
  
### <a name="options"></a>Opções  
 **Adicionar**  
 Adicione uma nova entrada à lista. Você só pode adicionar os nomes de logon, conta ou grupo já definidos no Publicador e no Distribuidor Eles serão definidos em ambos os servidores se as contas de domínio ou contas locais tiverem sido criadas em ambos.  
  
 **Remover**  
 Remova a entrada selecionada da lista.  
  
 **Remover Tudo**  
 Remova todas as entradas da lista. 


  Essa página permite:  
  
-   Definir propriedades de entrega do instantâneo por FTP (File Transfer Protocol). Para obter mais informações, consulte [transferir instantâneos por meio](transfer-snapshots-through-ftp.md) da documentação do Windows FTP para obter mais informações.  
  
    > [!NOTE]  
    >  Alterações em qualquer configuração do FTP exigem que um novo instantâneo seja gerado.  
  
-   Definir propriedades de sincronização da Web para replicação de mesclagem no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, que permite que as assinaturas sejam sincronizadas pelo HTTPS (protocolo de transferência segura de hipertexto). Para usar sincronização da Web, você deve configurar um servidor IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
### <a name="options"></a>Opções  
 **Acessar arquivos de instantâneo via FTP**  
 Selecione **Permitir que os Assinantes baixem os arquivos de instantâneo usando FTP**e especifique **Nome do servidor FTP**, **Número da porta**, **Caminho da pasta raiz de FTP**, **Logon**e **Senha**, para permitir que os Assinantes usem o FTP para entrega de instantâneo.  
  
 Essa opção permite que os Assinantes usem o FTP para recuperar arquivos de instantâneo, mas não exige que isso seja feito. Se você selecionar essa opção, o Assistente para Nova Assinatura será padronizado para que o Assinante recupere arquivos de instantâneo pelo FTP. Para alterar a configuração, use a caixa de diálogo **Propriedades da Assinatura** . Se você permitir que os Assinantes acessem arquivos de instantâneo pelo FTP, especifique a pasta de FTP como o local de arquivos de instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades da Assinatura** . Essa ação fará com que o Agente de Instantâneo atualize os arquivos na pasta do FTP automaticamente quando um novo instantâneo for gerado. Se o local para a pasta do FTP não for definido, você terá de atualizar os arquivos manualmente quando novos instantâneos forem gerados. Para obter mais informações, consulte [Deliver a Snapshot Through FTP](publish/deliver-a-snapshot-through-ftp.md) (Entregar um instantâneo por meio de FTP).  
  
 **Sincronização da Web**  
 Somente replicação de mesclagem. Selecione **Permitir que os Assinantes sincronizem por meio da conexão com um servidor Web**e especifique um endereço de servidor Web para permitir que Assinantes de mesclagem usem a sincronização da Web. O servidor Web deve usar protocolo SSL (Secure Sockets Layer) e o endereço Web precisa ser totalmente qualificado, como `https://server.domain.com/synchronize`. Para obter mais informações, consulte [Configurar sincronização da Web](configure-web-synchronization.md).  

## <a name="agent-security"></a>Segurança do agente
  A página **Segurança do Agente** da caixa de diálogo **Propriedades de Publicação** permite acessar as configurações das contas nas quais os seguintes agentes executam e fazem conexões com computadores em uma topologia de replicação:  
  
-   O Agente de Instantâneo para todas as publicações.    
-   O Agente de Leitor de Log para todas as publicações transacionais. Há um Agente de Leitor de Log para cada banco de dados publicado para replicação transacional. A alteração das configurações do Agente de Leitor de Log afeta todas as publicações transacionais em um banco de dados.    
-   O Agente de Leitor de Fila para publicações transacionais, que permite assinaturas de atualização enfileiradas. Há um Agente de Leitor de Fila para cada banco de dados de distribuição. A alteração das configurações do Agente de Leitor de Fila afeta todas as publicações transacionais com assinaturas de atualização em fila que usam o mesmo banco de dados de distribuição. Para obter mais informações sobre as configurações de segurança do Queue Reader Agent, consulte [Exibir e modificar configurações de segurança de replicação](security/view-and-modify-replication-security-settings.md).  
  
 Para obter mais informações sobre configurações de segurança e permissões exigidas para cada agente, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
### <a name="options"></a>Opções  
 **Configurações de segurança** ou **Criar Agente**  
 Se um trabalho de agente tiver sido criado, clique em **Configurações de segurança** para acessar a caixa de diálogo que permite alterar as configurações de segurança de um agente. Se um trabalho de agente não tiver sido criado, clique em **Criar Agente** para criar um e especificar as configurações de segurança.  

## <a name="data-partitions"></a>Partições de Dados
  A página **Partições de Dados** da caixa de diálogo **Propriedades de Publicação** permite definir partições de dados para publicações de mesclagem que usam filtragem com parâmetros. Depois de definir as partições, você pode gerar instantâneos para essas partições, fornecendo conjuntos de dados iniciais diferentes para Assinantes diferentes, com base nas propriedades de conexão (logon e/ou nome de computador) dos Assinantes. Você pode também selecionar para permitir aos Assinantes solicitarem a entrega e a geração de instantâneo, se não tiverem um instantâneo disponível para a partição, na primeira vez em que sincronizarem. Para obter mais informações, consulte [Criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
### <a name="options"></a>Opções  
 **Adicionar**  
 Clique em **Adicionar** para definir uma partição. Na caixa de diálogo **Adicionar Partição de Dados** especifique os valores para **HOST_NAME()** e/ou **SUSER_SNAME()** e defina um agendamento de atualização de instantâneos.  
  
 **Editar**  
 Selecione uma partição existente na grade e clique em **Editar** para editar a partição.  
  
 **Delete (excluir)**  
 Selecione uma partição existente na grade e clique em **Excluir** para excluir a partição.  
  
 **Gerar os instantâneos selecionados agora**  
 Selecione uma ou mais partições na grade e clique em **Gerar os instantâneos selecionados agora** para gerar os instantâneos para essas partições.  
  
 **Limpar os instantâneos existentes**  
 Selecione uma ou mais partições na grade e clique em **Limpar os instantâneos existentes** para limpar os instantâneos para essas partições.  
  
 **Definir automaticamente uma partição e gerar um instantâneo, se necessário, quando um novo Assinante tentar sincronizar**  
 Selecione essa opção se quiser permitir que os Assinantes solicitem geração e aplicação de  instantâneo. Os Assinantes podem exigir essa opção, se não tiverem um instantâneo disponível para a partição, na primeira vez em que sincronizarem.  

## <a name="snapshot"></a>Instantâneo

 A página **Instantâneo** da caixa de diálogo **Propriedades de Publicação** permite que você defina o formato do instantâneo, o local da pasta de instantâneo e os scripts a serem executados antes e depois da aplicação do instantâneo. A pasta de instantâneo deve ser designada como compartilhada e ter permissões adequadas para os agentes que leem e gravam arquivos na pasta. Para obter mais informações sobre como proteger a pasta adequadamente, consulte [Secure the Snapshot Folder](security/secure-the-snapshot-folder.md) (Proteger a pasta de instantâneo).  
  
> [!NOTE]  
>  As alterações exigem um novo instantâneo para a publicação. Para obter mais informações, consulte [Alterar propriedade da publicação e do artigo](publish/change-publication-and-article-properties.md).  
  
### <a name="options"></a>Opções  
 **Formato do instantâneo**  
 Selecione modo nativo ou modo de caractere para o formato do instantâneo.  
  
-   Selecione **Native SQL Server – todos os Assinantes devem ser servidores executando o SQL Server** se todos os Assinantes forem instâncias do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. O formato de instantâneo nativo fornece o melhor desempenho.    
-   Selecione **Caractere - necessário se um Publicador ou Assinante não estiver executando o SQL Server** se nenhum Assinante estiver executando o [!INCLUDE[ssEW](../../includes/ssew-md.md)] ou forem Assinantes não[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Local dos arquivos de instantâneo**  
 Selecione o local para armazenar arquivos de instantâneo. Eles podem ser armazenados no local padrão; e também, em vez disso, podem ser armazenados em um local alternativo ou em outro local além do local padrão. Arquivos armazenados em um local alternativo podem ser compactados.  
  
-   Selecione **Colocar os arquivos na pasta padrão** para usar a pasta de instantâneo padrão para o Publicador. O local da pasta de instantâneo é somente leitura nessa caixa de diálogo porque ele só pode ser alterado para o Publicador na caixa de diálogo **Propriedades do Distribuidor** . Para obter mais informações, consulte [especificar o local do instantâneo padrão](snapshot-options.md#snapshot-folder-locations).   
-   Selecione **Colocar os arquivos nesta pasta** para especificar, em vez disso, um local alternativo ou outro local além do padrão. Insira em um caminho na caixa de texto ou clique em **Procurar** e navegue até um local. Selecione **Compactar arquivos de instantâneo nesta pasta** para compactar os arquivos no local de instantâneo alternativo. O local alternativo pode ser em outro servidor, em uma unidade de rede ou em uma mídia removível, como um CD-ROM ou disco removível. Para obter mais informações, consulte [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md) e [Compressed Snapshots](compressed-snapshots.md).  
  
 **Executar scripts adicionais**  
 Especifique scripts a serem executados antes e depois que o instantâneo for aplicado ao Assinante. Não poderão ser especificados scripts se o **Formato do instantâneo** for **Caractere**.  
  
 Os scripts são opcionais, mas fornecem um modo conveniente de executar comandos e aplicar alterações administrativas nos Assinantes. Para obter mais informações sobre a execução de scripts, consulte [Execute Scripts Before and After the Snapshot Is Applied](snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied) (Executar scripts antes e após a aplicação do instantâneo).  
  
-   Insira um caminho na caixa de texto **Depois de aplicar o instantâneo, executar este script** ou clique em **Procurar** para especificar um local para o script.   
-   Insira um caminho na caixa de texto **Após aplicar o instantâneo, executar este script** ou clique em **Procurar** para especificar um local para o script.  



## <a name="see-also"></a>Consulte Também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Publicar objetos de banco de dados e](publish/publish-data-and-database-objects.md)   
 [Práticas recomendadas de segurança de replicação](security/replication-security-best-practices.md)   
 [Segurança de Replicação do SQL Server](security/view-and-modify-replication-security-settings.md)  
 [Inicializar uma assinatura com um instantâneo](initialize-a-subscription-with-a-snapshot.md)   
  
  
