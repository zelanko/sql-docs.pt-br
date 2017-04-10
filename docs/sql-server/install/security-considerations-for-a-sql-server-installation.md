---
title: "Considera&#231;&#245;es sobre seguran&#231;a para uma instala&#231;&#227;o do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sistemas de firewall [SQL Server]"
  - "protocolo SMB [SQL Server]"
  - "desabilitando protocolos"
  - "segurança [SQL Server], instalações"
  - "protocolos [SQL Server], desabilitando"
  - "NetBIOS [SQL Server]"
  - "serviços [SQL Server], segurança"
  - "SMB [SQL Server]"
  - "isolando serviços [SQL Server]"
  - "Configuração [SQL Server], segurança"
  - "poucos privilégios para instalação do SQL Server"
  - "NTFS [SQL Server]"
  - "segurança física [SQL Server]"
  - "segurança do sistema de arquivos [SQL Server]"
  - "Instalando o SQL Server, segurança"
ms.assetid: cf96155f-30a8-48b7-8d6b-24ce90dafdc7
caps.latest.revision: 48
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 48
---
# Considera&#231;&#245;es sobre seguran&#231;a para uma instala&#231;&#227;o do SQL Server
  A segurança é importante para todo produto e todo negócio. Seguindo práticas recomendadas simples, você pode evitar muitas vulnerabilidades de segurança. Este tópico discute algumas práticas recomendadas de segurança que você deve considerar antes de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e depois de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Está incluída orientação de segurança para recursos específicos nos tópicos de referência para esses recursos.  
  
## Antes de instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Siga estas práticas recomendadas quando você configurar o ambiente do servidor:  
  
-   [Aprimore a segurança física](#physical_security)  
  
-   [Use firewalls](#firewalls)  
  
-   [Isole serviços](#isolated_services)  
  
-   [Configure um sistema de arquivos seguro](#sa_with_least_privileges)  
  
-   [Desabilite os protocolos NetBIOS e SMB](#disabled_protocols)  
  
-   [Instalando o SQL Server em um controlador de domínio](../../sql-server/install/security-considerations-for-a-sql-server-installation.md#Install_DC)  
  
###  <a name="physical_security"></a> Aprimore a segurança física  
 O isolamento físico e lógico compõe a base de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para aprimorar a segurança física da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute as seguintes tarefas:  
  
-   Coloque o servidor em uma sala à qual somente pessoas autorizadas tenham acesso.  
  
-   Coloque os computadores que hospedam um banco de dados em um local fisicamente protegido, idealmente em uma sala de computadores trancada com sistemas de detecção de inundação e detecção ou extinção de incêndio monitorados.  
  
-   Instale os bancos de dados na zona segura da intranet corporativa e não conecte os SQL Servers diretamente à Internet.  
  
-   Faça backup de todos os dados regularmente e proteja os backups em um local externo.  
  
###  <a name="firewalls"></a> Use firewalls  
 Os firewalls são importantes para ajudar a proteger a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os firewalls serão mais efetivos se você seguir estas diretrizes:  
  
-   Coloque um firewall entre o servidor e a Internet. Habilite seu firewall. Se seu firewall estiver desligado, ligue-o. Se seu firewall estiver ligado, não desligue-o.  
  
-   Divida a rede em zonas de segurança separadas por firewalls. Bloqueie todo o tráfego e admita seletivamente apenas o que for necessário.  
  
-   Em um ambiente multicamadas, use vários firewalls para criar sub-redes filtradas.  
  
-   Quando você estiver instalando o servidor dentro de um domínio do Windows, configure firewalls interiores para permitir a Autenticação do Windows.  
  
-   Se o seu aplicativo usar transações distribuídas, talvez seja necessário configurar o firewall para permitir que tráfego do MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)]) flua entre instâncias separadas do MS DTC. Você também precisará configurar o firewall para permitir que o tráfego flua entre o MS DTC e gerenciadores de recursos, como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações sobre as configurações de firewall do Windows padrão e obter uma descrição das portas TCP que afetam o [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
###  <a name="isolated_services"></a> Isole serviços  
 O isolamento de serviços reduz o risco de que um serviço comprometido possa ser usado para comprometer outros. Para isolar serviços, considere as seguintes diretrizes:  
  
-   Execute serviços separados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sob contas separadas do Windows. Sempre que possível, use contas de usuário Local ou do Windows separadas e com poucos direitos para cada serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
###  <a name="sa_with_least_privileges"></a> Configure um sistema de arquivos seguro  
 O uso do sistema de arquivos correto aumenta a segurança. Para instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve executar as seguintes tarefas:  
  
-   Use o sistema de arquivos NTFS. NTFS é o sistema de arquivos preferido para instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] porque ele é mais estável e recuperável que os sistemas de arquivos FAT. O NTFS também habilita opções de segurança, como listas de controle de acesso (ACLs) a arquivos e diretórios e criptografia de arquivos do sistema de arquivos com criptografia (EFS). Durante a instalação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definirá ACLs apropriadas em chaves do Registro e arquivos se ele detectar NTFS. Essas permissões não devem ser alteradas. As versões futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem não dar suporte à instalação em computadores com sistemas de arquivos FAT.  
  
    > [!NOTE]  
    >  Se você usar EFS, os arquivos de banco de dados serão criptografados sob a identidade da conta que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Apenas essa conta poderá descriptografar os arquivos. Se você precisar alterar a conta que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], primeiro deverá descriptografar os arquivos sob a conta antiga e criptografá-los novamente sob a nova conta.  
  
-   Use um RAID (Redundant Array of Independent Disks) para arquivos de dados críticos.  
  
###  <a name="disabled_protocols"></a> Desabilite os protocolos NetBIOS e SMB  
 Todos os servidores na rede de perímetro devem ter os protocolos desnecessários desabilitados, incluindo NetBIOS e SMB.  
  
 O NetBIOS usa as seguintes portas:  
  
-   UDP/137 (serviço de nome do NetBIOS)  
  
-   UDP/138 (serviço de datagrama do NetBIOS)  
  
-   TCP/139 (serviço de sessão do NetBIOS)  
  
 O SMB usa as seguintes portas:  
  
-   TCP/139  
  
-   TCP/445  
  
 Os servidores Web e DNS (Sistema de Nome de Domínio) não requerem NetBIOS ou SMB. Nesses servidores, desabilite os dois protocolos para reduzir a ameaça de enumeração de usuário.  
  
###  <a name="Install_DC"></a> Instalando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio  
 Por motivos de segurança, é recomendável não instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um controlador de domínio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não bloqueará a instalação em um computador que seja um controlador de domínio, mas as seguintes limitações se aplicam:  
  
-   Você não pode executar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio sob uma conta de serviço local.  
  
-   Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalado em um computador, você não poderá alterar o computador de um membro do domínio para um controlador de domínio. Você deve desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de alterar o computador host para um controlador de domínio.  
  
-   Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalado em um computador, você não poderá alterar o computador de um controlador de domínio para um membro do domínio. Você deve desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de alterar o computador host para um membro do domínio.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde os nós de agrupamento sejam controladores de domínio.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação não pode criar grupos de segurança nem provisionar contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um controlador de domínio somente leitura. Nesse cenário, haverá falha na Instalação.  
  
## Durante ou após a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Após a instalação, você pode aprimorar a segurança da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguinte estas práticas recomendadas relativas a contas e modos de autenticação:  
  
 **Contas de serviço**  
  
-   Execute os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as menores permissões possíveis.  
  
-   Associe os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a contas de usuário locais do Windows ou contas de usuário do domínio com pouco privilégio.  
  
-   Para obter mais informações, veja [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
 **Modo de autenticação**  
  
-   Requeira Autenticação do Windows para conexões com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Usar a autenticação Kerberos. Para obter mais informações, veja [Registrar um nome de entidade de serviço para conexões de Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
 **Senhas fortes**  
  
-   Sempre atribua uma senha forte à conta **sa**.  
  
-   Sempre habilite a verificação de política de senha sobre nível de segurança e expiração de senhas.  
  
-   Use sempre senhas fortes para todos os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Durante instalação do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], é adicionado um logon para o grupo BUILTIN\Users. Assim, todos os usuários autenticados do computador podem acessar a instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] como membros da função pública. O logon BUILTIN\Users pode ser removido com segurança para restringir o acesso a [!INCLUDE[ssDE](../../includes/ssde-md.md)] aos usuários do computador que têm logons individuais ou que são membros de outros grupos do Windows com logons.  
  
## Consulte também  
 [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [Protocolos de rede e bibliotecas de rede](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [Registrar um nome de entidade de serviço para conexões de Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
  