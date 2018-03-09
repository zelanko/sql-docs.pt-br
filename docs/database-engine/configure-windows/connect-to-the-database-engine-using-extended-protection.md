---
title: "Conectar-se ao Mecanismo de Banco de Dados usando a Proteção Estendida | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- spoofing attacks
- service binding
- luring attacks
- Schannel
- channel binding
- Extended Protection
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5bf850e985baccb1d16d77697ea7cd2611af222
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="connect-to-the-database-engine-using-extended-protection"></a>Conectar-se ao mecanismo de banco de dados usando proteção estendida
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à **Proteção Estendida** desde o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. A**Proteção Estendida para Autenticação** é um recurso dos componentes de rede implementado pelo sistema operacional. Há suporte para a**Proteção Estendida** no Windows 7 e no Windows Server 2008 R2. **Proteção Estendida** é incluída em pacotes de serviço para sistemas operacionais [!INCLUDE[msCoName](../../includes/msconame-md.md)] mais antigos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é mais seguro quando as conexões são efetuadas usando a **Proteção Estendida**.  
  
> [!IMPORTANT]  
>  O Windows não habilita a **Proteção Estendida** por padrão. Para obter informações sobre como habilitar a **Proteção Estendida** no Windows, consulte [Proteção Estendida para Autenticação](http://support.microsoft.com/kb/968389).  
  
## <a name="description-of-extended-protection"></a>Descrição da Proteção Estendida  
 A**Proteção Estendida** usa a associação de serviço e de canal para ajudar a evitar ataques de retransmissão de autenticação. Em um ataque de retransmissão de autenticação, um cliente que pode executar autenticação NTLM (por exemplo, Windows Explorer, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook, um aplicativo .NET SqlClient, etc.), se conecta a um invasor (por exemplo, um servidor de arquivos CIFS mal-intencionado). O invasor usa as credenciais do cliente para se passar pelo cliente e se autenticar em um serviço (por exemplo, uma instância do serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)] ).  
  
 Há duas variações deste ataque:  
  
-   Em um ataque de atração, o cliente é atraído para se conectar voluntariamente ao invasor.  
  
-   Em um ataque de falsificação, o cliente pretende se conectar a um serviço válido, mas não sabe que o DNS e/ou o roteamento IP foram adulterados para redirecionar a conexão para o invasor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte para a associação de serviço e canal para ajudar a reduzir esses ataques em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="service-binding"></a>associação de serviço  
 A associação de serviço lida com ataques de atração exigindo que um cliente envie um SPN (nome da entidade de serviço) assinado do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual o cliente pretende se conectar. Como parte da resposta de autenticação, o serviço verifica se o SPN recebido no pacote corresponde a seu próprio SPN. Se um cliente for atraído para se conectar a um invasor, esse cliente incluirá o SPN assinado do invasor. O invasor não pode retransmitir o pacote para autenticação no serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] real como o cliente, porque isso incluiria o SPN do invasor. A associação de serviço incorre em um custo único insignificante, mas não lida com ataques de falsificação. A Associação de Serviço ocorre quando um aplicativo cliente não usa criptografia para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="channel-binding"></a>associação de canal  
 A associação de canal estabelece um canal seguro (Schannel) entre um cliente e uma instância do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O serviço verifica a autenticidade do cliente comparando o CBT (token da associação de canal) do cliente específico a esse canal com seu próprio CBT. A associação de canal lida com ataques de atração e falsificação. No entanto, ela incorre em um custo de tempo real maior, porque requer a criptografia TLS de todo o tráfego da sessão. A Associação de Canal ocorre quando um aplicativo cliente usa criptografia para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independentemente de a criptografia ser imposta pelo cliente ou pelo servidor.  
  
> [!WARNING]  
>  Os provedores de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte ao TLS 1.0 e SSL 3.0. Se você impor um protocolo diferente (como TLS 1.1 ou TLS 1.2) fazendo alterações na camada de sistema operacional SChannel, suas conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderão falhar.  
  
### <a name="operating-system-support"></a>Suporte do sistema operacional  
 Os seguintes links fornecem mais informações sobre o modo como o Windows dá suporte à **Proteção Estendida**:  
  
-   [Autenticação Integrada do Windows com Proteção Estendida](http://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [Microsoft Security Advisory (973811), Proteção Estendida para Autenticação](http://www.microsoft.com/technet/security/advisory/973811.mspx)  
  
## <a name="settings"></a>Configurações  
 Há três configurações de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que afetam a associação de serviço e de canal. As configurações podem ser definidas com o uso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou da WMI e podem ser exibidas usando-se a faceta **Configurações de Protocolo de Servidor** do Gerenciamento Baseado em Diretivas.  
  
-   **Forçar criptografia**  
  
     Os valores possíveis são **Ativa** e **Inativa**. Para usar a associação de canal, a opção **Forçar Criptografia** deve ser definida como **Ativa**e todos os clientes serão forçados a criptografar. Se for **Inativa**, somente a associação de serviço será garantida. A opção**Forçar Criptografia** está localizada em **Protocolos para Propriedades MSSQLSERVER (Guia Snoalizadores)** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   **Proteção estendida**  
  
     Os valores possíveis são **Ativa**, **Permitida**e **Obrigatória**. A variável de **Proteção Estendida** permite que os usuários configurem o nível de **Proteção Estendida** para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A**Proteção Estendida** está localizada em **Protocolos para Propriedades MSSQLSERVER (Guia Avançado)** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
    -   Quando definida como **Ativada**, a **Proteção Estendida** está desabilitada. A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceitará conexões de qualquer cliente, independentemente de o cliente estar protegido ou não. A opção**Desativada** é compatível com sistemas operacionais mais antigos e sem patches, mas é menos segura. Use essa configuração se você souber que os sistemas operacionais cliente não têm suporte para proteção estendida.  
  
    -   Quando definida como **Permitida**, a **Proteção Estendida** é necessária para conexões de sistemas operacionais com suporte para a **Proteção Estendida**. A**Proteção Estendida** é ignorada para conexões de sistemas operacionais que não têm suporte para **Proteção Estendida**. As conexões de aplicativos cliente desprotegidos que estejam sendo executados em sistemas operacionais cliente protegidos são rejeitadas. Essa configuração é mais segura que **Desativada**, mas não é a configuração mais segura. Use essa configuração em ambientes mistos, onde alguns sistemas operacionais dão suporte à **Proteção Estendida** e outros não.  
  
    -   Quando definida como **Obrigatória**, somente conexões de aplicativos protegidos em sistemas operacionais protegidos são aceitas. Essa configuração é a mais segura dentre as três, mas conexões de sistemas operacionais ou aplicativos sem suporte para **Proteção Estendida** não poderão ser estabelecidas com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **SPNs NTLM aceitos**  
  
     A variável **SPNs NTLM Aceitos** é necessária quando um servidor é conhecido por mais de um SPN. Quando um cliente tentar se conectar ao servidor usando um SPN válido que o servidor não conhece, a associação de serviço falhará. Para evitar esse problema, os usuários poderão especificar vários SPNs que representam o servidor usando **SPNs NTLM Aceitos**. A opção**SPNs NTLM Aceitos** corresponde a uma série de SPNs separados por ponto-e-vírgulas. Por exemplo, para permitir os SPNs **MSSQLSvc/ HostName1.Contoso.com** e **MSSQLSvc/ HostName2.Contoso.com**, digite **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** na caixa **SPNs NTLM Aceitos** . Essa variável tem um tamanho máximo de 2.048 caracteres. A opção**SPNs NTLM Aceitos** está localizada em **Protocolos para Propriedades MSSQLSERVER (Guia Avançado)** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
## <a name="enabling-extended-protection-for-the-database-engine"></a>Habilitando a Proteção Estendida para o mecanismo de banco de dados  
 Para usar a **Proteção Estendida**, o servidor e o cliente devem ter um sistema operacional com suporte para **Proteção Estendida**e a **Proteção Estendida** deve estar habilitada no sistema operacional. Para obter mais informações sobre como habilitar a **Proteção Estendida** para o sistema operacional, consulte [Proteção Estendida para Autenticação](http://support.microsoft.com/kb/968389).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte para a **Proteção Estendida** desde o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. A**Proteção Estendida** para algumas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será disponibilizada em atualizações futuras. Depois de habilitar a **Proteção Estendida** no computador servidor, siga estas etapas para habilitar a **Proteção Estendida**:  
  
1.  No menu **Iniciar** , escolha **Todos os Programas**, aponte para **Microsoft SQL Server** e clique em **SQL Server Configuration Manager**.  
  
2.  Expanda **Configuração de Rede do SQL Server**e clique com o botão direito do mouse em **Protocolos do** *\<*InstanceName*>*e clique em **Propriedades**.  
  
3.  Para associação de canal e associação de serviço, na guia **Avançado** , defina a **Proteção Estendida** com a configuração apropriada.  
  
4.  Se desejar, quando um servidor for conhecido por mais de um SPN, na guia **Avançado** , configure o campo **SPNs NTLM Aceitos** conforme descrito na seção "Configurações".  
  
5.  Para associação de canal, na guia **Sinalizadores** , defina **Forçar Criptografia** como **Ativa**.  
  
6.  Reinicie o serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="configuring-other-sql-server-components"></a>Configurando outros componentes do SQL Server  
 Para obter mais informações sobre como configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], veja [Proteção estendida para autenticação com o Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
 Ao usar o IIS para acessar dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando uma conexão HTTP ou HTTPS, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode aproveitar a Proteção Estendida fornecida pelo IIS. Para obter mais informações sobre como configurar o IIS para usar a Proteção Estendida, consulte [Configure Extended Protection in IIS 7.5](http://go.microsoft.com/fwlink/?LinkId=181105)(em inglês).  
  
## <a name="see-also"></a>Consulte Também  
 [Configuração de rede do servidor](../../database-engine/configure-windows/server-network-configuration.md)   
 [Configuração de rede do cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Visão geral sobre a Proteção Estendida para Autenticação](http://go.microsoft.com/fwlink/?LinkID=177943)   
 [Autenticação Integrada do Windows com Proteção Estendida](http://go.microsoft.com/fwlink/?LinkId=179922)  
  
  
