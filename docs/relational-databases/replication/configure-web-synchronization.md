---
title: Configure a sincronização da Web | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- SQL10.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
helpviewer_keywords:
- Web synchronization, security best practices
- Web synchronization, configuring
ms.assetid: 21f8e4d4-cd07-4856-98f0-9c9890ebbc82
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: da05c6156a401eee4eaba87c6888281b2f28c773
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773969"
---
# <a name="configure-web-synchronization"></a>Configurar Sincronização da Web
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A opção de sincronização da Web da Replicação de Mesclagem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilita a replicação de dados usando o protocolo HTTP pela Internet. Para usar a sincronização da Web, primeiro você precisa executar as ações de configuração a seguir:  
  
1.  Crie novas contas de domínio e mapeie logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Configure o computador que está executando o Serviços de Informações da Internet (IIS) do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para sincronizar assinaturas.  
  
3.  Configure uma publicação de mesclagem para permitir a sincronização da Web.  
  
4.  Configure uma ou mais assinaturas para usar a sincronização da Web.  

> [!NOTE]  
>  Se você planeja replicar grandes volumes de dados ou usar tipos de dados grandes, como **varchar(max)** , leia a seção "Replicando grandes volumes de dados" neste tópico.  
  
 Para configurar a sincronização da Web com êxito, você deve decidir como configurará a segurança para atender a seus requisitos e políticas específicos. É melhor tomar essas decisões e criar as contas necessárias antes de tentar configurar o IIS, a publicação e as assinaturas.  
  
 Nos procedimentos a seguir, uma configuração de segurança simplificada que usa contas locais é descrita, para brevidade. Essa configuração simplificada é adequada para instalações onde o IIS e o Publicador e o Distribuidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão em execução no mesmo computador, embora seja muito mais provável (e recomendável) que você use uma topologia de vários servidores para uma instalação de produção. Você pode substituir contas de domínio para as contas locais nos procedimentos.  
  
## <a name="creating-new-accounts-and-mapping-sql-server-logins"></a>Criando novas contas e mapeando logons do SQL Server  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (replisapi.dll) conecta-se ao Publicador representando a conta especificada para o pool de aplicativos que está associado ao site de replicação.  
  
 A conta usada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener deve ter permissões conforme descrito no tópico [Merge Agent Security](../../relational-databases/replication/merge-agent-security.md), na seção "Conectar-se ao publicador ou ao distribuidor". Em resumo, a conta deve:  
  
-   Ser um membro da lista de acesso à publicação (PAL).  
  
-   Ser mapeada para um logon associado a um usuário no banco de dados de publicação.  
  
-   Ser mapeada para um logon associado a um usuário no banco de dados de distribuição.  
  
-   Ter permissões de Leitura no compartilhamento de instantâneos.  
  
 Se esta for a primeira vez que você está usando a Replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você também precisará criar contas e logons para os agentes de replicação. Para obter mais informações, consulte as seções "Configurando a publicação" e "Configurando a assinatura" neste tópico.  
  
 Antes de configurar a sincronização da Web, é recomendável ler a seção "Práticas recomendadas de segurança para sincronização da Web" neste tópico. Para obter mais informações sobre a sincronização da Web, consulte [Security Architecture for Web Synchronization](../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
## <a name="configuring-the-computer-that-is-running-iis"></a>Configurando o computador que está executando o IIS  
 A sincronização da Web exige instalação e configuração do IIS. Você precisará da URL para o site de replicação para poder configurar uma publicação para usar a sincronização da Web.  
  
 Há suporte para sincronização da Web no IIS, a partir da versão 5.0. O Assistente para Configurar a Sincronização da Web não tem suporte no IIS versão 7.0. A partir do SQL Server 2012, para usar o componente de sincronização da Web no servidor IIS, recomendamos instalar o SQL Server com replicação. Essa pode ser a edição gratuita do SQL Server Express.  
  
 O TLS é necessário para a sincronização da Web. Você precisará de um certificado de segurança emitido por uma autoridade de certificação. Apenas para objetivos de teste, é possível usar certificados de segurança emitidos por conta própria.  
   
  
 **Para configurar o IIS para sincronização da Web**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configurar o IIS para sincronização da Web](../../relational-databases/replication/configure-iis-for-web-synchronization.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configurar o IIS 7 para sincronização da Web](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md)  
  
## <a name="creating-a-web-garden"></a>Criando um ambiente Web  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener dá suporte a duas operações de sincronização simultâneas por thread. Exceder esse limite pode fazer com que o Replication Listener pare de responder. O número de threads alocados para replisapi.dll é determinado pela propriedade Máximo de Processos do Operador do pool de aplicativos. Por padrão, essa propriedade é definida como 1.  
  
 É possível dar suporte a um número maior de operações de sincronização simultâneas por CPU aumentando o valor da propriedade Máximo de Processos do Operador. A expansão com o aumento do número de processos do operador por CPU é conhecido como a criação de um "Ambiente Web".  
  
 O ambiente Web permitirá que mais de dois Assinantes sincronizem ao mesmo tempo. Também aumentará a utilização de CPU por replisapi.dll, o que pode afetar negativamente o desempenho global do servidor. É importante balancear essas considerações ao escolher um valor para Máximo de Máximos do Operador.  
  
#### <a name="to-increase-maximum-worker-processes-in-iis-7"></a>Para aumentar Máximo de Processos do Operador no IIS 7  
  
1.  No **Gerenciador dos Serviços de Informações da Internet (IIS)** , expanda o nó do servidor local e clique no nó **Pool de Aplicativos** .  
  
2.  Selecione o pool de aplicativos associado ao site de sincronização da Web e clique em **Configurações Avançadas** no painel **Ações** .  
  
3.  Na caixa de diálogo Configurações Avançadas, sob o título **Modelo de Processo** , clique na linha rotulada como **Máximo de Processos do Operador**. Altere o valor da propriedade e clique em **OK**.  
  
## <a name="configuring-the-publication"></a>Configurando a publicação  
 Para usar a sincronização da Web, primeiro crie uma publicação da mesma forma como o faria para uma topologia de mesclagem padrão. Para obter mais informações, consulte [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 Depois de criar a publicação, habilite a opção para permitir a sincronização da Web usando um dos seguintes métodos: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou Replication Management Objects (RMO). Para habilitar a sincronização da Web, é necessário fornecer o endereço do servidor Web para conexões do Assinante.  
  
 Se você estiver usando um Publicador pela primeira vez, será necessário configurar também um Distribuidor e um compartilhamento de instantâneos. O Agente de Mesclagem, em cada Assinante, precisa ter permissões de leitura no compartilhamento de instantâneo. Para obter mais informações, consulte [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md) e [Proteger uma pasta de instantâneo](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
 **gen** é uma palavra reservada em arquivos XML websync. Não tente publicar tabelas que contêm colunas nomeadas **gen**.  
  
## <a name="configuring-the-subscription"></a>Configurando a assinatura  
 Depois de habilitar uma publicação e configurar o IIS, crie uma assinatura pull e especifique que ela deve ser sincronizada usando o IIS. (A sincronização da Web tem suporte apenas para assinaturas pull.)  
  
## <a name="upgrading-from-an-earlier-version-of-sql-server"></a>Atualizando de uma versão anterior do SQL Server  
 Se houver uma topologia de sincronização da Web existente e você atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], será necessário verificar se a última versão de Replisapi.dll foi copiada para o diretório virtual usado pela sincronização da Web. Por padrão, a última versão de Replisapi.dll está localizada em C:\Arquivos de Programas\Microsoft SQL Server\\<nnn\>\COM.  
  
## <a name="replicating-large-volumes-of-data"></a>Replicando grandes volumes de dados  
 Para ajudar a evitar possíveis problemas de memória em computadores Assinantes, a sincronização da Web usa um tamanho padrão máximo de 100 MB para o arquivo XML usado para transferir alterações. O limite pode ser aumentado definindo a seguinte chave do registro:  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\Replication**  
  
 **WebSyncMaxXmlSize DWORD 2000000**  
  
 O intervalo de valores aceitáveis para esta chave é de 100 MB a 4 GB. O valor é especificado em KB. Definir este parâmetro como um valor alto não garante que você pode sincronizar essa quantidade de dados. O limite efetivo é restringido pela quantidade de memória contígua disponível no computador de Assinante. Se for necessário um valor maior que 100 MB, recomendamos que você aumente o valor de modo incremental e teste o consumo de memória com uma carga de trabalho típica no Assinante.  
  
 O tamanho máximo do arquivo XML é 4 GB, mas a replicação sincroniza as alterações desse arquivo em lotes. O tamanho de lote máximo de dados e metadados é de 25 MB. Você deve garantir que os dados não excedam a aproximadamente 20 MB em cada lote, o que permite metadados e qualquer outra sobrecarga. Esse limite tem as seguintes implicações:  
  
-   Você não pode reproduzir nenhuma coluna que faça com que os dados e metadados excedam 25 MB. Esse poderia ser um assunto quando você estiver reproduzindo linhas que contenham tipos de dados grandes, como **varchar(max)** .  
  
-   Se você reproduzir grandes volumes de dados, talvez tenha que ajustar o tamanho do lote do Agente de Mesclagem.  
  
 O tamanho do lote para replicação de mesclagem é medido em *gerações*, que são coleções de alterações por artigo. O número de gerações em um lote é especificado usando os parâmetros -**DownloadGenerationsPerBatch** e -**UploadGenerationsPerBatch** do Agente de Mesclagem. Para obter mais informações, consulte [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
 Para grandes volumes de dados, especifique um número pequeno para cada um dos parâmetros para envio em lote. É recomendável começar com um valor de 10 e ajustá-lo com base nas necessidades e no desempenho do aplicativo. Normalmente, esses parâmetros são especificados em um perfil de agente. Para obter mais informações sobre perfis, consulte [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="security-best-practices-for-web-synchronization"></a>Práticas recomendadas de segurança para a sincronização da Web  
 Há muitas opções para configurações relacionadas à segurança na sincronização da Web. É recomendável usar a abordagem a seguir:  
  
-   O Distribuidor e o Publicador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem estar no mesmo computador (uma configuração típica da replicação de mesclagem). No entanto, o IIS dever ser instalado em um computador separado.  
  
-   Use o protocolo TLS (Transport Layer Security), antes conhecido como SSL (Secure Sockets Layer), para criptografar a conexão entre o Assinante e o computador que está executando o IIS. Isso é necessário para a sincronização da Web.  
  
-   Use a autenticação básica para conexões do Assinante com o IIS. Usando a Autenticação básica, o IIS pode fazer conexões para o Publicador/Distribuidor em nome do Assinante, sem requerer delegação. A delegação é necessária quando se usa a Autenticação integrada.  
  
    > [!NOTE]  
    >  A autenticação básica é o método pelo qual são passadas credenciais ao IIS. A Autenticação Básica não impede a especificação de contas do domínio do Windows para conexões feitas no IIS.  
  
-   Especifique que o Agente de Instantâneo seja executado em uma conta de domínio do Windows, e especifique que o agente faça conexões de acordo com essa conta. (Essa é a configuração padrão.) Especifique que cada Agente de Mesclagem seja executado na conta de domínio do usuário que utiliza o computador Assinante, e especifique que o agente faça conexões segundo essa conta.  
  
     Para obter mais informações sobre permissões requeridas pelos agentes, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Especifique a mesma conta de domínio usada pelo Agente de Mesclagem quando você especifica uma conta e a senha na página **Informações do Servidor Web** do Assistente para Nova Assinatura ou quando você especifica valores para os parâmetros `@internet_url` e `@internet_login` de [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Essa conta deve ter permissões de leitura para o compartilhamento de instantâneo.  
  
-   Cada publicação deve usar um diretório virtual separado para o IIS.  
  
-   A conta sob a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (Replisapi.dll) executa também é a conta que se conectará ao Publicador e ao Distribuidor durante a sincronização. Essa conta deve ser mapeada para uma conta de logon do SQL no Publicador e no Distribuidor. Para obter mais informações, consulte a seção "Definindo permissões para o SQL Server Replication Listener" no [Configurar IIS para sincronização da Web](../../relational-databases/replication/configure-iis-for-web-synchronization.md).  
  
-   É possível usar FTP para entregar o instantâneo do Publicador ao computador que está executando o IIS. O instantâneo é sempre entregue do computador que está executando o IIS ao Assinante, usando HTTPS. Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
-   Se os servidores da topologia de replicação estiverem protegidos por firewall, poderá ser necessário abrir portas no firewall para habilitar a sincronização da Web.  
  
    -   O computador Assinante conecta-se ao computador que está executando o IIS por HTTPS usando o TLS que, normalmente, é configurado para usar a porta 443. Os assinantes do[!INCLUDE[ssEW](../../includes/ssew-md.md)] também podem ser conectados por HTTP, que é configurado normalmente para usar a porta 80.  
  
    -   O computador que está executando o IIS, em geral, conecta-se ao Publicador ou ao Distribuidor usando a porta 1433 (instância padrão). Quando o Publicador ou o Distribuidor é uma instância nomeada em um servidor com outra instância padrão, a porta 1500 é normalmente usada para conexão à instância nomeada.  
  
    -   Se o computador que está executando o IIS estiver separado do Distribuidor por um firewall, e um compartilhamento de FTP for usado para a entrega de instantâneo, as portas usadas para o FTP precisarão ser abertas. Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
> [!IMPORTANT]  
>  A abertura de portas no firewall pode deixar o servidor exposto a ataques mal-intencionados. Certifique-se de conhecer os sistemas de firewall antes de abrir portas. Para obter mais informações, consulte [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Sincronização da Web para replicação de mesclagem](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
