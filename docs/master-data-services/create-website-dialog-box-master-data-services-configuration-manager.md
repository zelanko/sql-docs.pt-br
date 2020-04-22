---
title: Caixa de diálogo Criar Site
ms.custom: seo-lt-2019
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createsite.f1
ms.assetid: 179c9c1e-3b06-421b-b71b-1cb64d104f5e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: dea7da40c1c82b855f4290f104c0b2d4f8462a38
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728278"
---
# <a name="create-website-dialog-box-master-data-services-configuration-manager"></a>Caixa de diálogo Criar Site (Gerenciador de Configuração do Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use a caixa de diálogo **Criar Site** para criar um novo site no computador local. Quando você cria um site no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], o site é adicionado ao IIS (Serviços de Informações da Internet) no computador local com um aplicativo raiz configurado como o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Um novo pool de aplicativos também é criado e o aplicativo Web é colocado nesse pool de aplicativos.  
  
## <a name="web-site"></a>Site  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Nome do site**|Digite um nome para o site ou use o nome padrão. Esse nome é um nome amigável que é usado apenas para identificar o site no IIS. Ele não é usado para acessar o site em um navegador da Web.<br /><br /> O nome deve ser exclusivo entre todos os sites do IIS no computador local.|  
|**Protocolo**|Exibe **http**. Use o protocolo HTTP quando a comunicação entre cliente e servidor não precisar ocorrer em um canal criptografado.<br /><br /> **Observação**: não é possível criar um site HTTPS no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. HTTPS é o protocolo HTTP usando O TLS (Transport Layer Security), anteriormente conhecido como Secure Sockets Layer (SSL), e é útil ao trocar dados confidenciais ou pessoais, ou quando você deseja que os usuários confirmem a identidade do servidor antes de transmitir informações pessoais. Se você precisar transferir informações entre o servidor e um cliente usando um canal criptografado, terá que usar uma ferramenta do IIS, como o Gerenciador do IIS, para configurar o site com uma associação HTTPS e vincular a associação do site a um certificado do servidor; isso é necessário para que o site seja aberto com êxito em um navegador da Web. Para obter mais informações sobre certificados do servidor, consulte [Configuring Server Certificates in IIS 7](https://go.microsoft.com/fwlink/?LinkId=163220) (em inglês) no [!INCLUDE[msCoName](../includes/msconame-md.md)] TechNet.|  
|**Endereço IP**|Selecione um endereço IP que os usuários possam usar para acessar o site. Por padrão, a opção **Nenhum Atribuído** está selecionada. A menos que você tenha uma razão para usar um endereço IPv4 ou IPv6 específico, use o valor padrão.<br /><br /> Com **Nenhum Atribuído**, esse site responde a solicitações de todos os endereços IP na porta e no nome de host opcional que você especifica. Se outro site no servidor tiver uma associação na mesma porta, mas com um endereço IP específico, aquele site receberá solicitações HTTP para aquela porta e endereço IP específico, e o site com o endereço IP **Nenhum Atribuído** receberá todas as outras solicitações HTTP para aquela porta e para os outros endereços IP.|  
|**Porta**|Digite a porta para solicitações feitas para este site. Se você selecionar o protocolo HTTP, a porta padrão será 80. Se você especificar uma porta diferente das portas padrão, os clientes deverão especificar o número da porta para conectar-se ao site.<br /><br /> **Observação**: o **Site Padrão** no IIS é configurado para usar o protocolo HTTP na porta 80 com todos os endereços IP não atribuídos. Se tentar criar o site no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] com as informações de associação padrão, você receberá um erro indicando que existe uma associação duplicada. Você deve alterar as informações de associação do site no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]ou alterar as informações de associação do Site Padrão usando uma ferramenta do IIS, como o Gerenciador do IIS. Como alternativa, você pode especificar um cabeçalho de host para habilitar o IIS a identificar o site exclusivamente. Verifique se o seu firewall está configurado para aceitar tráfego pela porta especificada.|  
|**Cabeçalho do host**|Valor opcional. Digite um nome de cabeçalho do host. Use essa opção quando desejar atribuir um nome de host, também conhecido como um nome de domínio, para um computador que usa um único endereço IP ou porta. Quando você especifica um nome de host, os clientes devem usar esse nome em vez do endereço IP para acessar o site. Quando configurar um nome de host, você não poderá abrir o site em um navegador da Web até que seu servidor DNS tenha uma entrada para esse nome de host.<br /><br /> Por exemplo, se você desejar que os usuários acessem seu site no endereço `https://www.contoso.com/`, deverá especificar www.contoso.com como o nome do host e o servidor DNS deverá ter uma entrada para ele.<br /><br /> Se seu site estiver disponível em uma intranet, você não precisará especificar um nome de host se os usuários digitarem o nome do servidor em um navegador, por exemplo, `https://server_name`. No entanto, se o servidor DNS em seu ambiente estiver configurado para armazenar outros nomes para esse servidor Web, você poderá criar uma associação separada para cada nome de host de forma que os usuários possam usar os outros nomes armazenados pelo servidor DNS. Se você precisar configurar mais de um nome de host para seu site, use uma ferramenta do IIS, como o Gerenciador do IIS, para adicionar associações de site adicionais.|  
  
## <a name="application-pool"></a>Pool de Aplicativos  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Nome**|Digite um nome amigável e exclusivo para um novo pool de aplicativos ou use o nome padrão que é fornecido. O aplicativo Web raiz desse site executa nesse pool de aplicativos.<br /><br /> Os pools de aplicativos fornecem limites que impedem que os aplicativos em um pool de aplicativos afetem aplicativos em outro pool de aplicativos.|  
|**Nome de usuário**|Digite um domínio e nome de usuário do Active Directory. Essa conta de serviço é a identidade do pool de aplicativos no qual o aplicativo Web é executado.<br /><br /> Essa conta é adicionada à função de banco de dados mds_exec no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para acesso ao banco de dados. Para obter mais informações, veja [Logons, usuários e funções de banco de dados &#40;Master Data Services&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md). Também é adicionada a um grupo do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] no Windows, **MDS_ServiceAccounts**, que recebe permissão para o diretório temporário de compilação, **MDSTempDir**, no sistema de arquivos. Para obter mais informações, veja [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Senha**|Digite a senha da conta de usuário especificada.|  
|**Confirmar senha**|Digite novamente a senha da conta de usuário especificada. Os campos **Senha** e **Confirmar senha** devem conter a mesma senha.|  
  
## <a name="see-also"></a>Consulte Também  
 [Página de configuração da Web &#40;gerente de configuração de serviços de dados master&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[Instalação e configuração do Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md) [Requisitos do aplicativo Web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
