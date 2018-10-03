---
title: Distributed Replay Security | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 7e2e586d-947d-4fe2-86c5-f06200ebf139
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1e85883fa9b772d132cc5f6aaa75f7d46539244
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717024"
---
# <a name="distributed-replay-security"></a>Segurança do Distributed Replay
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Antes de instalar e usar o recurso Distributed Replay do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , revise as informações de segurança importantes neste tópico. Este tópico descreve as etapas de configuração de segurança pós-instalação que são necessárias antes de usar o Distributed Replay. Este tópico também descreve considerações importantes referentes à proteção de dados e etapas de remoção importantes.  
  
## <a name="user-and-service-accounts"></a>Contas de usuário e serviço  
 A tabela a seguir descreve as contas usadas no Distributed Replay. Depois da instalação do Distributed Replay, atribua as entidades de segurança com que as contas de controlador e serviço cliente serão executadas. Portanto, é recomendável configurar as contas de usuário de domínio correspondentes antes de instalar os recursos do Distributed Replay.  
  
|Conta de usuário|Requisitos|  
|------------------|------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay|Pode ser uma conta de usuário de domínio ou uma conta de usuário local. Se você usar uma conta de usuário local, a ferramenta de administração, o controlador e o cliente deverão estar em execução no mesmo computador.<br /><br /> **\*\* Observação de Segurança \*\*** É recomendável que a conta não seja membro do grupo Administradores local no Windows.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Conta de serviço do cliente do Distributed Replay|Pode ser uma conta de usuário de domínio ou uma conta de usuário local. Se você usar uma conta de usuário local, o controlador, o cliente e o SQL Server de destino deverão estar em execução no mesmo computador.<br /><br /> **\*\* Observação de Segurança \*\*** É recomendável que a conta não seja membro do grupo Administradores local no Windows.|  
|Conta de usuário interativa que é usada para executar a ferramenta de administração do Distributed Replay|Pode ser uma conta de usuário local ou uma conta de usuário de domínio. Para usar uma conta de usuário local, a ferramenta de administração e o controlador devem estar em execução no mesmo computador.|  
  
 **Importante**: Quando você configura o controlador Distributed Replay, pode especificar uma ou mais contas de usuário que serão usadas para executar os serviços de cliente do Distributed Replay. Esta é a lista das contas com suporte:  
  
-   Conta de usuário do domínio  
  
-   Conta de usuário local criada pelo usuário  
  
-   Administrador  
  
-   Conta virtual e MSA (Conta de Serviço Gerenciada)  
  
-   Serviços de rede, serviços locais e sistema  
  
 Não são aceitas contas de grupo (local ou domínio) e outras contas internas (como Todos).  
  
 Para definir as contas de serviço ou suas senhas depois de instalar o Distributed Replay, você pode usar a ferramenta Serviços do Windows. Para alterar as contas de serviço associadas com serviços de controlador ou cliente do Distributed Replay, siga estas etapas:  
  
1.  Execute um destes procedimentos, dependendo do sistema operacional:  
  
    -   Clique em **Iniciar**, digite **services.msc** na caixa **Pesquisar** e pressione ENTER.  
  
    -   Clique em **Iniciar**, clique em **Executar**, digite **services.msc**e pressione ENTER.  
  
2.  Na caixa de diálogo **Serviços** , clique com o botão direito do mouse no serviço a ser configurado e clique em **Propriedades**.  
  
3.  Na guia **Fazer Logon** , clique em **Esta conta**.  
  
4.  Configure a conta de usuário a ser usada.  
  
## <a name="file-and-folder-permissions"></a>Permissões de arquivo e pasta  
 Depois que as contas de serviço forem especificadas, conceda as permissões necessárias de arquivo e pasta a essas contas de serviço. Configure permissões de arquivo e pasta de acordo com a seguinte tabela:  
  
|Conta|Permissões de pasta|  
|-------------|------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay|`<Controller_Installation_Path>\DReplayController` (Leitura, Gravação, Exclusão)<br /><br /> `DReplayServer.xml` arquivo (Leitura, Gravação)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Conta de serviço do cliente do Distributed Replay|`<Client_Installation_Path>\DReplayClient` (Leitura, Gravação, Exclusão)<br /><br /> `DReplayClient.xml` arquivo (Leitura, Gravação)<br /><br /> Os diretórios de trabalho e resultado, conforme especificado no arquivo de configuração de cliente pelos elementos `WorkingDirectory` e `ResultDirectory` , respectivamente. (Leitura, Gravação)|  
  
## <a name="dcom-permissions"></a>Permissões DCOM  
 O DCOM é usado na RPC (chamada de procedimento remoto) entre o controlador e a ferramenta de administração, e entre o controlador e todos os clientes. Você deve configurar permissões DCOM específicas do aplicativo no computador inteiro no controlador após a instalação de recursos do Distributed Replay.  
  
 Para configurar permissões do controlador DCOM, siga estas etapas:  
  
1.  **Abrir dcomcnfg.exe, o snap-in de Serviços de Componentes**: esta é a ferramenta que é usada para configurar permissões DCOM.  
  
    1.  No computador do controlador, clique em **Iniciar**.  
  
    2.  Tipo **dcomcnfg.exe** na caixa **Pesquisa** .  
  
    3.  Pressione ENTER.  
  
2.  **Configurar permissões DCOM no computador inteiro**: conceda as permissões DCOM correspondentes no computador inteiro para cada conta listada na tabela a seguir. Para obter mais informações sobre como definir permissões no computador inteiro, veja [Lista de verificação: Gerenciar aplicativos DCOM](http://go.microsoft.com/fwlink/?LinkId=185842).  
  
3.  **Configurar permissões DCOM específicas do aplicativo**: conceda as permissões DCOM correspondentes específicas do aplicativo para cada conta listada na tabela a seguir. O nome do aplicativo DCOM para o serviço do controlador é **DReplayController**. Para obter mais informações sobre como definir permissões específicas do aplicativo, veja [Lista de verificação: Gerenciar aplicativos DCOM](http://go.microsoft.com/fwlink/?LinkId=185842).  
  
 A seguinte tabela descreve quais permissões DCOM são necessárias para a conta de usuário interativa da ferramenta de administração e para as contas de serviço cliente:  
  
|Recurso|Conta|Permissões DCOM necessárias no controlador|  
|-------------|-------------|---------------------------------------------|  
|Ferramenta de administração Distributed Replay|A conta de usuário interativa|Acesso local<br /><br /> Acesso remoto<br /><br /> Inicialização local<br /><br /> Inicialização remota<br /><br /> Ativação local<br /><br /> Ativação remota|  
|Cliente Distributed Replay|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Conta de serviço do cliente do Distributed Replay|Acesso local<br /><br /> Acesso remoto<br /><br /> Inicialização local<br /><br /> Inicialização remota<br /><br /> Ativação local<br /><br /> Ativação remota|  
  
> [!IMPORTANT]  
>  Para ajudar a proteger contra consultas mal-intencionadas ou ataques de negação de serviço, verifique se está usando apenas uma conta de usuário de confiança para a conta de serviço do cliente. Esta conta poderá se conectar e reproduzir cargas de trabalho na instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="sql-server-permissions"></a>Permissões do SQL Server  
 As contas de serviço de cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay são usadas na conexão à instância de destino da carga de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Apenas o modo de Autenticação do Windows tem suporte para essas conexões.  
  
 Depois de instalar o serviço de cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay em um conjunto de computadores, conceda à entidade de segurança usada para essas contas de serviço a função de servidor sysadmin na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você pretende reproduzir a carga de trabalho de rastreamento. Esta etapa não é executada automaticamente durante a Instalação do Distributed Replay.  
  
## <a name="data-protection"></a>Proteção de dados  
 No ambiente do Distributed Replay, é concedido total acesso das seguintes contas de usuário à instância de servidor de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aos dados de rastreamento de entrada e aos arquivos de rastreamento de resultado:  
  
-   A conta de usuário interativa que é usada para executar a ferramenta de administração.  
  
-   A conta de serviço do controlador.  
  
-   A conta de serviço do cliente.  
  
-   Membros do grupo Administradores local no controlador.  
  
-   Membros do grupo Administradores local nos clientes.  
  
    > [!IMPORTANT]  
    >  Estas contas têm total acesso a PII (informações pessoalmente identificáveis) ou a informações confidenciais que estão contidas nos arquivos de rastreamento, intermediários, de distribuição ou de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foram usados pelo Distributed Replay.  
  
 É recomendável adotar estas medidas de segurança:  
  
-   Armazene os dados de rastreamento de entrada, os resultados de rastreamento de saída e os arquivos de banco de dados em um local que use o NTFS (sistema de arquivos NTFS) e aplique as ACLs (listas de controle de acesso) apropriadas. Se for preciso, criptografe os dados que são armazenados no computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Lembre-se de que ACLs não são aplicados aos arquivos de rastreamento e não há mascaramentos ou ofuscamentos de dados. Você deve excluir estes arquivos rapidamente após usá-los.  
  
-   Aplique as ACLs apropriadas e a política de retenção a todos os arquivos intermediários e de distribuição gerados através do Distributed Replay.  
  
-   Use o Protocolo SSL para ajudar a proteger o transporte de rede.  
  
## <a name="important-removal-steps"></a>Etapas de remoção importantes  
 É recomendável usar o Distributed Replay apenas em um ambiente de teste. Após concluir os testes, e antes de provisionar esses computadores para uma tarefa diferente, siga estes procedimentos:  
  
-   Desinstale recursos do Distributed Replay e remova os arquivos de configuração relacionados do controlador e de todos os clientes.  
  
-   Exclua qualquer arquivo de rastreamento, intermediário, de distribuição e de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenham sido usados em testes. Os arquivos intermediários e de distribuição são armazenados no diretório de trabalho no controlador e no cliente, respectivamente.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Instalar o Distributed Replay – Visão geral](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
  
