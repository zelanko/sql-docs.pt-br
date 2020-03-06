---
title: Listas de verificação de configuração
description: Fornece listas de verificação para as tarefas necessárias para configurar o sistema de plataforma de análise para seu próprio ambiente. Essas tarefas de configuração são necessárias para que você possa usar o dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 80fc899400be167badaae9d617d43a61e0d346b5
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340459"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Listas de verificação de configuração do dispositivo para o Analytics Platform System
Fornece listas de verificação para as tarefas necessárias para configurar o sistema de plataforma de análise para seu próprio ambiente. Essas tarefas de configuração são necessárias para que você possa usar o dispositivo.  
  
> [!WARNING]  
> O uso da**Configuration Manager** do sistema de plataforma de análise é a melhor maneira e a única maneira com suporte, para executar as tarefas disponíveis na ferramenta.  
  
## <a name="BeforeTasks"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
  
1.  O dispositivo deve ser instalado no data center e ligado.  
  
2.  Verifique se você tem as seguintes informações, que são fornecidas pelo seu IHV:  
  
    -   Endereço IP externo para o nó de controle do PDW (*PDW_region-* CTL01)  
  
    -   Nome de domínio do dispositivo  
  
    -   Nome de usuário e senha para o administrador de domínio do dispositivo  
  
3.  Obtenha um certificado confiável. Você irá importar isso em uma etapa posterior para permitir que os clientes se conectem ao **console de administração** com conexões seguras. Salve o certificado no nó de controle em um arquivo PFX protegido por senha.  
  
4.  Inicie o **Configuration Manager**, usando as seguintes etapas:  
  
    1.  Use **área de trabalho remota** para se conectar ao nó de controle do PDW (*PDW_region*-CTL01). (Talvez você precise se conectar com o endereço IP externo para CTL01.)  
  
    2.  Inicie o **Configuration Manager** no menu **Iniciar** do nó de controle do PDW. A primeira tela da Configuration Manager exibe a topologia do dispositivo, que foi criada pelo seu IHV. É uma lista dos nós de hardware reconhecidos pelo software SQL Server PDW como parte do seu dispositivo. Não é necessário alterar as configurações na tela de topologia do dispositivo.  
  
## <a name="CMTasks"></a>Executar tarefas de Configuration Manager  
O**Configuration Manager** de SQL Server PDW (PDWCM) é uma ferramenta de administração de dispositivo que SQL Server PDW os administradores de sistema usam para executar operações em nível de dispositivo e alterar as configurações de nível de dispositivo. Por exemplo, use PDWCM para redefinir senhas, definir o fuso horário, alterar endereços IP, configurar certificados SSL, habilitar o acesso remoto por meio do firewall, iniciar ou parar o dispositivo e definir a inicialização instantânea de arquivo.  
  
Use **Configuration Manager** para executar as seguintes tarefas de configuração.  
  
|Tarefa de configuração|Descrição|  
|----------------------|---------------|  
|Familiarize-se com os nomes de componentes físicos|[Componentes físicos do PDW e da malha de dispositivos &#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Iniciar SQL Server PDW Configuration Manager|[Inicie o Configuration Manager &#40;o sistema de plataforma de análise&#41;](launch-the-configuration-manager.md)|  
|Alterar a senha do administrador de domínio|O dispositivo tem uma Active Directory Domain Services privada do Windows que é usada para autenticar nós no dispositivo.<br /><br />Seu IHV configurou o dispositivo com uma senha de administrador de domínio padrão. Isso precisa ser alterado para uma senha que seja segura.<br /><br />A **Configuration Manager** é a única maneira com suporte para alterar a senha do administrador de domínio.<br /><br />Para obter mais informações, consulte [redefinição de senha &#40;&#41;do sistema de plataforma de análise ](password-reset.md).|  
|Alterar a senha do logon **SA**|SQL Server PDW tem um logon de administrador do sistema chamado **SA**. O logon **SA** tem todos os privilégios. Ele pode conceder, negar ou revogar qualquer permissão. Ele também pode ver todas as exibições do sistema.<br /><br />Para obter mais informações, consulte [redefinição de senha &#40;&#41;do sistema de plataforma de análise ](password-reset.md).|  
|Definir o fuso horário do dispositivo|Defina a hora (local ou outro horário desejado) para todos os nós de dispositivo.<br /><br />Para obter mais informações, consulte [configuração de fuso horário do dispositivo &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md).|  
|Especifique as configurações de rede externas para o dispositivo SQL Server PDW|[Configuração de rede do dispositivo &#40;Analytics Platform System&#41;](appliance-network-configuration.md)|  
|Importar um certificado de segurança para o console de administração|Um certificado pode fornecer conexões de protocolo SSL (SSL) por HTTPS para [monitorar o dispositivo usando o console de administração &#40;&#41;Analytics Platform System ](monitor-the-appliance-by-using-the-admin-console.md). Por padrão, o **console de administração** do inclui um certificado autoassinado que fornece privacidade, mas não autenticação de servidor. Esse certificado também retorna um erro no Internet Explorer que diz: "há um problema com o certificado de segurança deste site" quando o usuário se conecta. Embora essa conexão criptografe dados em trânsito entre o cliente e o servidor, a conexão ainda está em risco de invasores.<br /><br />SQL Server PDW os administradores devem adquirir imediatamente um certificado que se encadeia a uma autoridade de certificação confiável reconhecida por clientes, a fim de ter uma conexão segura e remover o erro que o Internet Explorer relata. Isso requer um nome de domínio totalmente qualificado que mapeia o endereço IP virtual do nó de controle (recomendado) ou um nome de certificado que corresponda ao valor que os usuários digitam em suas barras de endereço do navegador para acessar o console de administração.<br /><br />Use o **Configuration Manager** para adicionar ou remover certificados confiáveis. Não há suporte para o uso direto da ferramenta de configuração`winHttpCertCfg.exe`de certificado do Microsoft Windows http Services () para gerenciar certificados.<br /><br />Para obter mais informações, consulte [provisionamento de certificados do PDW &#40;&#41;do sistema de plataforma de análise ](pdw-certificate-provisioning.md).|
|Opção de recurso|Exibe informações sobre opções de recursos que são introduzidas no Analytics Platform System AU7. Use esta página para atualizar ou habilitar/desabilitar recursos e configurações no Analytics Platform System. A alteração dos valores de opção de recurso requer uma reinicialização do serviço.<br /><br />Para obter mais informações, consulte [switch de recursos do PDW &#40;Analytics Platform System&#41;](appliance-feature-switch.md).|
|Habilite ou desabilite as regras de firewall do Windows que permitem ou impedem o acesso a portas específicas no dispositivo SQL Server PDW.|Seu IHV configurará e habilitará as regras de firewall necessárias para que o dispositivo opere corretamente. Na maioria dos casos, você não habilitará nem desabilitará as regras de firewall.<br /><br />Para obter mais informações, consulte [configuração do firewall do PDW &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md).|  
|Iniciar e parar o dispositivo SQL Server PDW|Interrompe ou inicia o dispositivo SQL Server PDW. Para obter mais informações, consulte [status dos serviços do PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).|  
|Examinar as opções de inicialização de arquivo instantânea usando a caixa de diálogo **privilégios**|A inicialização instantânea de arquivo é um recurso SQL Server que permite que as operações de arquivo de dados sejam executadas mais rapidamente. Ela será habilitada em SQL Server PDW somente se a conta de serviço de rede tiver recebido o privilégio de SE_MANAGE_VOLUME_NAME. Ela é desativada por padrão.<br /><br />Para obter mais informações, consulte [configuração de inicialização de arquivo instantâneo &#40;&#41;do sistema de plataforma de análise ](instant-file-initialization-configuration.md).|  
|Restaurar o banco de dados mestre de um backup|Exclui o banco de dados **mestre** atual e o substitui por um backup. Para obter mais informações, consulte [restaurar o banco de dados mestre &#40;o sistema de plataforma de análise&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Executar tarefas de configuração adicionais  
Depois de executar as tarefas de **Configuration Manager** , execute a lista de tarefas de configuração adicionais a seguir. Algumas dessas tarefas são opcionais.  
  
|Tarefa de configuração|Descrição|  
|----------------------|---------------|  
|Softwares antivírus de terceiros podem ser instalados e configurados no dispositivo SQL Server PDW para nós voltados para o público.<br /><br />(Opcional)|Para obter mais informações, consulte [software antivírus &#40;Analytics Platform System&#41;](antivirus-software.md).|  
|A senha do DSRM pode ser alterada.<br /><br />(Opcional)|Para obter mais informações, consulte [Definir senha de administrador para fazer logon em nós do AD no Modo de Restauração dos Serviços de Diretório &#40;DSRM&#41; &#40;&#41;do sistema de plataforma de análise ](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Configurar o dispositivo para receber atualizações de software<br /><br />(Recomendado)|O dispositivo precisa ser configurado para receber atualizações para o SQL Server PDW e software subjacente.<br /><br />Para obter mais informações, consulte [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md). Para obter informações sobre o WSUS, consulte [software servicing &#40;Analytics Platform System&#41;](software-servicing.md).|  
|Configure a conectividade com dados externos, como o Hadoop ou o armazenamento de BLOBs do Azure.<br /><br />(Opcional)|Para obter mais informações, consulte [Configurar a conectividade do polybase com dados externos &#40;o sistema de plataforma de análise&#41;](configure-polybase-connectivity-to-external-data.md).|  
|Configurar o software antivírus<br /><br />(Opcional)|Soluções antivírus de terceiros podem ser usadas para proteger nós voltados externamente, mas não são necessárias. Siga as diretrizes em.|  
|Configurar adaptadores de rede InfiniBand em servidores de backup e de carregamento<br /><br />(Opcional)|Para configurar servidores de backup e de carregamento para se conectarem ao SQL Server PDW usando a rede InfiniBand, você precisa configurar os adaptadores de rede para permitir que o DNS do dispositivo resolva a conexão InfiniBand para a rede InfiniBand ativa no momento.|  
|Configurar o para enviar dados de telemetria à Microsoft<br /><br />(Opcional)|Para configurar o sistema de plataforma de análise para enviar dados de telemetria à Microsoft, você precisa executar um script do PowerShell no nó de controle. Para obter instruções específicas, consulte [enviar comentários de telemetria para o Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Consulte Também  
[Software antivírus &#40;Analytics Platform System&#41;](antivirus-software.md)  
[Configurar os adaptadores de rede InfiniBand &#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
