---
title: Listas de verificação de configuração - Analytics Platform System | Microsoft Docs
description: Fornece listas de verificação para as tarefas necessárias para configurar o Analytics Platform System para seu ambiente. Essas tarefas de configuração são necessárias antes de usar o dispositivo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 17099af36994f24d182c7465bcbdc3f82e670328
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Listas de verificação de configuração de dispositivo para Analytics Platform System
Fornece listas de verificação para as tarefas necessárias para configurar o Analytics Platform System para seu ambiente. Essas tarefas de configuração são necessárias antes de usar o dispositivo.  
  
> [!WARNING]  
> Usando o Analytics Platform System**do Configuration Manager** é a melhor maneira e a única com suporte a maneira de executar as tarefas disponíveis na ferramenta.  
  
## <a name="BeforeTasks"></a>Antes de começar  
  
### <a name="prerequisites"></a>Prerequisites  
  
1.  O dispositivo deve ser instalado no data center e ligado.  
  
2.  Verifique se que você tem as seguintes informações, que são fornecidas pelo seu IHVS:  
  
    -   Endereço IP externo para o nó de controle do PDW (*PDW_region -* CTL01)  
  
    -   Nome de domínio do dispositivo  
  
    -   Nome de usuário e senha para o administrador de domínio do dispositivo  
  
3.  Obter um certificado confiável. Você vai importar isso em uma etapa posterior para permitir que clientes se conectem a **Console de administração** com conexões seguras. Salve o certificado para o nó de controle em um arquivo PFX protegido por senha.  
  
4.  Inicie o **do Configuration Manager**, usando as seguintes etapas:  
  
    1.  Use **área de trabalho remota** para conectar-se ao nó de controle do PDW (*PDW_region*-CTL01). (Talvez seja necessário conectar-se com o endereço IP externo para CTL01.)  
  
    2.  Inicie o **do Configuration Manager** do **iniciar** menu do nó de controle do PDW. A primeira tela do Configuration Manager exibe a topologia de aplicativo, que foi criada por seu IHVS. É uma lista de nós de hardware reconhecido pelo software PDW do SQL Server como parte do seu dispositivo. Você não precisa alterar as configurações na tela de topologia de aplicativo.  
  
## <a name="CMTasks"></a>Executar tarefas do Configuration Manager  
O SQL Server PDW**do Configuration Manager** (PDWCM) é uma ferramenta de administração de utilitário que os administradores de sistema do SQL Server PDW usam para executar operações no nível do dispositivo e para alterar as configurações no nível do dispositivo. Por exemplo, use PDWCM para redefinir senhas, definir o fuso horário, altere os endereços IP, configurar certificados SSL, habilitar o acesso remoto através do firewall, iniciar ou interromper o dispositivo e definir a inicialização instantânea de arquivo.  
  
Use **do Configuration Manager** para executar as seguintes tarefas de configuração.  
  
|Tarefa de configuração|Description|  
|----------------------|---------------|  
|Familiarize-se com os nomes de componente físico|[Malha de dispositivo e PDW componentes físicos &#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Inicie o Gerenciador de configuração do SQL Server PDW|[Inicie o Gerenciador de configuração &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)|  
|Alterar a senha de administrador de domínio|O dispositivo tem um privada Windows Active Directory Domain Services que é usado para autenticar nós no dispositivo.<br /><br />Seu IHVS configurar o dispositivo com uma senha de administrador de domínio padrão. Isso precisa ser alterada para uma senha segura.<br /><br />O **do Configuration Manager** é o único com suporte para alterar a senha de administrador de domínio.<br /><br />Para obter mais informações, consulte [de redefinição de senha &#40;Analytics Platform System&#41;](password-reset.md).|  
|Alterar a senha para o **sa** logon|SQL Server PDW tem um logon de administrador do sistema chamado **sa**. O **sa** logon que tenha todos os privilégios. Ele pode conceder, negar ou revogar qualquer permissão. Ele também pode ver todas as exibições do sistema.<br /><br />Para obter mais informações, consulte [de redefinição de senha &#40;Analytics Platform System&#41;](password-reset.md).|  
|Definir o fuso horário do dispositivo|Defina a hora (local ou outros desejado) para todos os nós de dispositivo.<br /><br />Para obter mais informações, consulte [configuração de fuso horário do dispositivo &#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md).|  
|Especifique as configurações de rede externamente para o dispositivo de PDW do SQL Server|[Configuração de rede do dispositivo &#40;Analytics Platform System&#41;](appliance-network-configuration.md)|  
|Importar um certificado de segurança para o Console de administração|Um certificado pode fornecer conexões de Secure Sockets Layer (SSL) sobre HTTPS para o [monitorar o dispositivo usando o Console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). Por padrão, o **Console de administração** inclui um certificado autoassinado que fornece privacidade, mas não a autenticação do servidor. Este certificado também retornará um erro no Internet Explorer informando: "Há um problema com o certificado de segurança do site" quando o usuário se conecta. Embora essa conexão criptografa os dados em trânsito entre o cliente e o servidor, a conexão é ainda ameaçado por invasores.<br /><br />Os administradores do SQL Server PDW imediatamente devem adquirir um certificado que se conecte a uma autoridade de certificação confiável reconhecida por clientes, para ter uma conexão segura e remover o erro que os relatórios do Internet Explorer. Isso requer um nome de domínio totalmente qualificado que mapeia o endereço IP virtual do nó de controle (recomendado) ou barras de um nome de certificado que corresponde ao valor que os usuários digitam em seus endereços do navegador para acessar o Console de administração.<br /><br />Use o **do Configuration Manager** para adicionar ou remover certificados confiáveis. Diretamente usando a ferramenta de configuração de certificado Microsoft Windows HTTP Services (`winHttpCertCfg.exe`) gerenciar os certificados não tem suporte.<br /><br />Para obter mais informações, consulte [provisionamento de certificados do PDW &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md).|
|Opção de recurso|Exibe informações sobre as opções de recurso que foram introduzidos no AU7 de sistema de plataforma de análise. Use esta página para atualizar ou habilitar/desabilitar recursos e configurações no sistema de plataforma de análise. Alterando os valores de chave de recurso requer uma reinicialização do serviço.<br /><br />Para obter mais informações, consulte [opção PDW &#40;Analytics Platform System&#41;](appliance-feature-switch.md).|
|Habilitar ou desabilitar as regras de Firewall do Windows que permitem ou impedem o acesso a portas específicas da solução SQL Server PDW.|Seu IHVS irá configurar e habilitar as regras de firewall que são necessárias para o dispositivo operar corretamente. Na maioria dos casos você não habilitar ou desabilitar as regras de firewall.<br /><br />Para obter mais informações, consulte [configuração de Firewall PDW &#40;Analytics Platform System&#41;](pdw-firewall-configuration.md).|  
|Iniciar e parar o utilitário do SQL Server PDW|Interrompe ou inicia o utilitário do SQL Server PDW. Para obter mais informações, consulte [Status de serviços PDW &#40;Analytics Platform System&#41;](pdw-services-status.md).|  
|Opções de inicialização imediata de arquivo de revisão usando o **privilégios** caixa de diálogo|A inicialização instantânea de arquivo é um recurso do SQL Server que permite operações de arquivo de dados ser executado mais rapidamente. Ele é habilitado no SQL Server PDW somente se a conta de serviço de rede recebeu o privilégio SE_MANAGE_VOLUME_NAME. Ele é desativado por padrão.<br /><br />Para obter mais informações, consulte [configuração de inicialização de arquivo instantânea &#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md).|  
|Restaure o banco de dados mestre de um backup|Exclui o atual **mestre** de banco de dados e o substitui por um backup. Para obter mais informações, consulte [restaurar o banco de dados mestre &#40;Analytics Platform System&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Executar tarefas de configuração adicionais  
Depois de executar o **do Configuration Manager** tarefas, execute a seguinte lista de tarefas de configuração adicionais. Algumas dessas tarefas são opcionais.  
  
|Tarefa de configuração|Description|  
|----------------------|---------------|  
|Software antivírus de terceiros pode ser instalado e configurado no dispositivo para nós de interface externa do SQL Server PDW.<br /><br />(opcional)|Para obter mais informações, consulte [Software antivírus &#40;Analytics Platform System&#41;](antivirus-software.md).|  
|A senha do DSRM pode ser alterada.<br /><br />(opcional)|Para obter mais informações, consulte [definir senha de administrador para fazer logon em nós do AD no modo de restauração de serviços de diretório &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Configurar o dispositivo para receber atualizações de software<br /><br />(Recomendado)|O dispositivo precisa ser configurado para receber atualizações para o software subjacente e o SQL Server PDW.<br /><br />Para obter mais informações, consulte [configurar o Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md). Para obter informações sobre o WSUS, consulte [Software manutenção &#40;Analytics Platform System&#41;](software-servicing.md).|  
|Configure a conectividade a dados externos, como o armazenamento de BLOBs do Azure ou Hadoop.<br /><br />(opcional)|Para obter mais informações, consulte [configurar conectividade do PolyBase para dados externos &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md).|  
|Configure o Software antivírus<br /><br />(opcional)|Soluções de antivírus de terceiros podem ser usadas para proteger nós externamente, mas não é necessárias. Siga as diretrizes.|  
|Configurar adaptadores de rede InfiniBand no Backup e servidores de carregamento<br /><br />(opcional)|Para configurar o Backup e o carregamento de servidores para se conectar ao SQL Server PDW pela rede InfiniBand, você precisa configurar os adaptadores de rede para permitir que o dispositivo de DNS para resolver o InfiniBand conexão à rede InfiniBand ativa no momento.|  
|Configurar para enviar dados de telemetria à Microsoft<br /><br />(opcional)|Para configurar o Analytics Platform System para enviar dados de telemetria à Microsoft, você precisa executar um script do PowerShell no nó de controle. Para obter instruções específicas, consulte [enviar comentários de telemetria à Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Consulte também  
[O Software antivírus &#40;Analytics Platform System&#41;](antivirus-software.md)  
[Configurar adaptadores de rede InfiniBand &#40;do SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
