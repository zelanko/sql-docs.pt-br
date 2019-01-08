---
title: Listas de verificação de configuração - Analytics Platform System | Microsoft Docs
description: Fornece listas de verificação para as tarefas necessárias para configurar o Analytics Platform System para seu próprio ambiente. Essas tarefas de configuração são necessárias antes de usar o dispositivo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ada3d2f782a33caf5334361a9682c53cf7cdec95
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398599"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Listas de verificação de configuração de dispositivo para o Analytics Platform System
Fornece listas de verificação para as tarefas necessárias para configurar o Analytics Platform System para seu próprio ambiente. Essas tarefas de configuração são necessárias antes de usar o dispositivo.  
  
> [!WARNING]  
> Usando o Analytics Platform System**Configuration Manager** é a melhor maneira e a única com suporte a forma, para executar as tarefas disponíveis na ferramenta.  
  
## <a name="BeforeTasks"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
  
1.  O dispositivo deve ser instalado no data center e ligado.  
  
2.  Verifique se que você tem as informações a seguir, que são fornecidas pelo IHV:  
  
    -   Endereço IP externo para o nó de controle do PDW (*PDW_region -* CTL01)  
  
    -   Nome de domínio do dispositivo  
  
    -   Nome de usuário e senha para o administrador de domínio do dispositivo  
  
3.  Obtenha um certificado confiável. Você vai importar isso em uma etapa posterior para permitir que os clientes se conectem-se para o **Console de administração** com conexões seguras. Salve o certificado para o nó de controle em um arquivo PFX protegido por senha.  
  
4.  Inicie o **Configuration Manager**, usando as seguintes etapas:  
  
    1.  Use **área de trabalho remota** para se conectar ao nó de controle do PDW (*PDW_region*-CTL01). (Talvez seja necessário conectar-se com o endereço IP externo para CTL01.)  
  
    2.  Inicie o **Configuration Manager** da **iniciar** menu do nó de controle do PDW. A primeira tela do Gerenciador de configurações exibe a topologia de dispositivo, que foi criada por IHV. É uma lista de nós de hardware reconhecidas pelo software do SQL Server PDW como parte do seu dispositivo. Não será preciso alterar as configurações na tela de topologia de aplicativo.  
  
## <a name="CMTasks"></a>Executar tarefas do Configuration Manager  
O SQL Server PDW**Configuration Manager** (PDWCM) é uma ferramenta de administração do dispositivo que os administradores de sistema do SQL Server PDW usarem para executar operações no nível do dispositivo e para alterar as configurações no nível do dispositivo. Por exemplo, use PDWCM para redefinir senhas, defina o fuso horário, alterem os endereços IP, configurar certificados SSL, habilitar o acesso remoto por meio do firewall, iniciar ou parar o dispositivo e definir a inicialização instantânea de arquivo.  
  
Use **Configuration Manager** para executar as seguintes tarefas de configuração.  
  
|Tarefa de configuração|Descrição|  
|----------------------|---------------|  
|Se familiarizar com os nomes de componente físico|[Malha de dispositivo e PDW componentes físicos &#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Inicie o Gerenciador de configuração do SQL Server PDW|[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)|  
|Alterar a senha de administrador de domínio|O dispositivo tem uma privada Windows Active Directory Domain Services que é usado para autenticar nós no dispositivo.<br /><br />IHV ao configurar o dispositivo com uma senha de administrador de domínio padrão. Isso precisa ser alterada para uma senha que é segura.<br /><br />O **Configuration Manager** é a única forma suportada para alterar a senha de administrador de domínio.<br /><br />Para obter mais informações, consulte [redefinição de senha &#40;Analytics Platform System&#41;](password-reset.md).|  
|Alterar a senha para o **sa** logon|SQL Server PDW tem um logon de administrador de sistema nomeado **sa**. O **sa** logon que tenha todos os privilégios. Ele pode conceder, negar ou revogar qualquer permissão. Ele também pode ver todas as exibições do sistema.<br /><br />Para obter mais informações, consulte [redefinição de senha &#40;Analytics Platform System&#41;](password-reset.md).|  
|Definir o fuso horário de dispositivo|Defina o tempo (local ou outro tempo desejado) para todos os nós de dispositivo.<br /><br />Para obter mais informações, consulte [configuração de fuso horário do dispositivo &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md).|  
|Especifique as configurações de rede voltado para o exterior para o dispositivo de PDW do SQL Server|[Configuração de dispositivo de rede &#40;Analytics Platform System&#41;](appliance-network-configuration.md)|  
|Importar um certificado de segurança para o Console de administração|Um certificado pode fornecer conexões Secure Sockets Layer (SSL) por HTTPS para o [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). Por padrão, o **Console de administração** inclui um certificado autoassinado que fornece privacidade, mas não a autenticação do servidor. Esse certificado também retorna um erro no Internet Explorer informando: "Há um problema com o certificado de segurança do site" quando o usuário se conecta. Embora essa conexão criptografa os dados em trânsito entre o cliente e o servidor, a conexão é ainda ameaçado por invasores.<br /><br />Os administradores do SQL Server PDW imediatamente devem adquirir um certificado que se encadeie a uma autoridade de certificação confiável reconhecido pelos clientes, para ter uma conexão segura e remover o erro que informa do Internet Explorer. Isso requer um nome de domínio totalmente qualificado que mapeia o endereço IP virtual do nó de controle (recomendado) ou barras de um nome de certificado que corresponde ao valor que os usuários digitam em seus endereços do navegador para acessar o Console de administração.<br /><br />Use o **Configuration Manager** para adicionar ou remover certificados confiáveis. Diretamente usando a ferramenta de configuração do Microsoft Windows HTTP Services certificado (`winHttpCertCfg.exe`) gerenciar certificados não tem suporte.<br /><br />Para obter mais informações, consulte [provisionamento de certificado do PDW &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md).|
|Comutador de recurso|Exibe informações sobre opções de recursos que foram introduzidos no Analytics Platform System AU7. Use esta página para atualizar ou ativar/desativar configurações no Analytics Platform System e os recursos. Alterando os valores de comutador de recurso exige uma reinicialização do serviço.<br /><br />Para obter mais informações, consulte [comutador de recurso do PDW &#40;Analytics Platform System&#41;](appliance-feature-switch.md).|
|Habilitar ou desabilitar regras de Firewall do Windows que permitem ou impedir o acesso a portas específicas no dispositivo de PDW do SQL Server.|IHV irá configurar e habilitar as regras de firewall são necessárias para o dispositivo operar corretamente. Na maioria dos casos você não habilitar ou desabilitar as regras de firewall.<br /><br />Para obter mais informações, consulte [configuração do Firewall PDW &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md).|  
|Iniciar e parar o dispositivo de PDW do SQL Server|Interrompe ou inicia o dispositivo de PDW do SQL Server. Para obter mais informações, consulte [Status de serviços do PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).|  
|Examine as opções de inicialização instantânea de arquivo usando o **privilégios** caixa de diálogo|Inicialização instantânea de arquivo é um recurso do SQL Server que permite que operações de arquivo de dados ser executado mais rapidamente. Ela é habilitada no SQL Server PDW somente se a conta de serviço de rede recebeu o privilégio SE_MANAGE_VOLUME_NAME. Ele é desativado por padrão.<br /><br />Para obter mais informações, consulte [configuração de inicialização de arquivo instantânea &#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md).|  
|Restaurar o banco de dados mestre de um backup|Exclui o atual **mestre** de banco de dados e a substitui por um backup. Para obter mais informações, consulte [restaurar o banco de dados mestre &#40;Analytics Platform System&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Executar tarefas de configuração adicionais  
Depois de executar o **Configuration Manager** tarefas, execute a seguinte lista de tarefas de configuração adicionais. Algumas dessas tarefas são opcionais.  
  
|Tarefa de configuração|Descrição|  
|----------------------|---------------|  
|Software antivírus de terceiros pode ser instalado e configurado no dispositivo de PDW do SQL Server para nós com face externa.<br /><br />(opcional)|Para obter mais informações, consulte [Software antivírus &#40;Analytics Platform System&#41;](antivirus-software.md).|  
|Pode ser alterada a senha do DSRM.<br /><br />(opcional)|Para obter mais informações, consulte [definir senha de administrador para fazer logon em nós no modo de restauração de serviços de diretório do AD &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Configurar o dispositivo para receber atualizações de software<br /><br />(Recomendado)|O dispositivo precisa ser configurado para receber atualizações para o SQL Server PDW e o software subjacente.<br /><br />Para obter mais informações, consulte [configurar o Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md). Para obter informações sobre o WSUS, consulte [manutenção de Software &#40;Analytics Platform System&#41;](software-servicing.md).|  
|Configure a conectividade a dados externos, como o armazenamento de BLOBs do Azure ou Hadoop.<br /><br />(opcional)|Para obter mais informações, consulte [configurar a conectividade do PolyBase para dados externos &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md).|  
|Configure o Software antivírus<br /><br />(opcional)|Soluções de antivírus de terceiros pode ser usado para proteger os nós voltado para o exterior, mas não é necessárias. Siga as diretrizes.|  
|Configurar adaptadores de rede InfiniBand no Backup e servidores de carregamento<br /><br />(opcional)|Para configurar o Backup e carregamento de servidores para se conectar ao SQL Server PDW, usando a rede InfiniBand, você precisará configurar os adaptadores de rede para permitir que o dispositivo de DNS para resolver a conexão de InfiniBand para rede InfiniBand ativa no momento.|  
|Configurar para enviar dados de telemetria à Microsoft<br /><br />(opcional)|Para configurar o Analytics Platform System para enviar dados de telemetria à Microsoft, você precisará executar um script do PowerShell no nó de controle. Para obter instruções específicas, consulte [enviar comentários de telemetria à Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Consulte também  
[Software antivírus &#40;Analytics Platform System&#41;](antivirus-software.md)  
[Configurar adaptadores de rede InfiniBand &#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
