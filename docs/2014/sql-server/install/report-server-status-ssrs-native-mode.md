---
title: Status do servidor de relatório (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serverstatus.F1
ms.assetid: 2f63ad1c-1bc2-449d-b451-fb39a0060838
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 15a177080792eb26273399f41aad577962885376
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952464"
---
# <a name="report-server-status-ssrs-native-mode"></a>Status do Servidor de Relatórios (modo nativo do SSRS)
  Use esta página para exibir informações sobre a instância do servidor de relatório à qual você está conectado atualmente. Essa é a página inicial para a configuração do servidor de relatórios. Estão disponíveis páginas adicionais para configurar URLs, a conta de serviço, o banco de dados do servidor de relatórios, a entrega de email do servidor de relatórios, a implantação de expansão e chaves de criptografia.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para abrir essa página, inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se à instância do servidor de relatórios. Para obter mais informações, [consulte &#40;Gerenciador de configurações do Reporting Services&#41;del](reporting-services-configuration-manager-native-mode.md).  
  
> [!TIP]  
>  O Configuration Manager @ no__t-0 (RSConfigTool. exe) é instalado com um nível de privilégio de "highestAvailable". Este comportamento ocorre por design. O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige a comunicação com APIs do WMI do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Algumas comunicações de WMI do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exigem um nível mais alto ou administrativo de privilégios.  
  
 Se você estabelecer conexão com o servidor de relatórios e todos os links da página estiverem esmaecidos, verifique se o serviço Servidor de Relatórios foi iniciado. O **status do serviço de relatório:** Deve ser "iniciado". Você também pode usar o aplicativo de console Serviços em Ferramentas do Administrador para verificar o status do serviço.  
  
## <a name="options"></a>Opções  
 **Instância de SQL Server**  
 Exibe informações sobre a instância do servidor de relatórios à qual você está atualmente conectado. Os nomes de instância do servidor de relatórios têm como base as instâncias nomeadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A instância padrão é MSSQLSERVER. Uma instância nomeada será um valor que você especificou durante a instalação. Para obter mais informações sobre instâncias, consulte [trabalhar com várias versões e instâncias do SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  No SQL Server Express with Advanced Services, a instância padrão é SQLExpress.  
  
 **ID da Instância**  
 Corresponde a uma pasta do sistema de arquivos que armazena arquivos de programas para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual você estabeleceu conexão. O valor **ID da Instância** é atribuído na Instalação no formato *componente*.*instância*, onde *componente* é um valor que indica um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente e *instância* é o nome da instância. O nome de instância padrão é MSSQLSERVER. Por exemplo, se você instalar instâncias padrão dos componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , os nomes de pastas correspondentes serão os seguintes:  
  
-   MSSQL12.MSSQLSERVER  
  
-   MSAS12.MSSQLSERVER  
  
-   MSRS12.MSSQLSERVER  
  
 Se você instalar uma segunda instância de um componente já instalado, como o [!INCLUDE[ssDE](../../includes/ssde-md.md)], e nomear a instância como Contoso, a **ID da Instância** será MSSQL12.Contoso.  
  
 **Edição**  
 Exibe informações de edição. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server](https://go.microsoft.com/fwlink/?linkid=232473).  
  
 **Versão do Produto**  
 Exibe a versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que você instalou.  
  
 **Banco de dados do Servidor de Relatório**  
 Exibe o nome do banco de dados do servidor de relatórios que armazena dados de aplicativo para a instância atual do servidor de relatórios.  
  
 **Modo do servidor de relatório**  
 Isso sempre deve mostrar um valor **Nativo**. O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oferece suporte apenas a servidores de relatório no modo Nativo. Se você vir o valor **modo integrado do SharePoint**, isso poderá indicar que sua implantação de modo nativo não está configurada corretamente e que você precisa conectar-se a um catálogo de relatório no modo nativo. Use a página **Banco de Dados** do Configuration Manager para alterar o banco de dados e criar um novo banco de dados ou conectar-se a um catálogo de banco de dados de servidor de relatório no modo nativo existente.  
  
 **Status do servidor**  
 Mostra se o serviço Servidor de Relatórios está em execução.  
  
 **Iniciar**  
 Inicia o serviço Servidor de Relatórios. O reinício do serviço será necessário depois de algumas alterações na configuração (por exemplo, ao reconfigurar um servidor de relatórios depois da alteração de um nome de computador). Se você reconfigurar as reservas de URL, o serviço será reiniciado automaticamente. O reinício é necessário para obter as alterações.  
  
 **Parar**  
 Para o serviço Servidor de Relatórios. Parar o serviço faz com que o servidor de relatórios pare de funcionar. Para obter mais informações, consulte [Iniciar e parar o serviço servidor de relatório](../../reporting-services/report-server/start-and-stop-the-report-server-service.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de configurações do Reporting Services F1 tópicos &#40;de ajuda sobre o&#41;modo nativo do SSRS](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Gerenciador de configurações do Reporting Services &#40;del&#41;](/sql/sql-server/install/reporting-services-configuration-manager-native-mode)   
 [Inicializar um servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
