---
title: Sobre reservas e registro de URL (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.date: 06/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dba8913c5aa5fa0aa8d93dd1c4dd639f85ac3081
ms.sourcegitcommit: 3f2936e727cf8e63f38e5f77b33442993ee99890
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67314034"
---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>Sobre reservas e registro de URL (Gerenciador de configurações do SSRS)
  As URLs para aplicativos do Reporting Services são definidas como reservas de URL em HTTP.SYS. Uma reserva de URL define a sintaxe de um ponto de extremidade de URL para um aplicativo Web. As reservas de URL são definidas para o serviço Web Servidor de Relatórios e para o portal da Web quando você configura os aplicativos no servidor de relatório. As reservas de URL são criadas automaticamente quando você configura URLs através da instalação ou da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   A instalação criará reservas de URL usando valores padrão. Se ela instalar a configuração padrão, reservará duas URLs: uma do serviço Web Servidor de Relatórios e outra do portal da Web. Você pode usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para adicionar mais URLs ou modificar as URLs padrão criadas pela instalação.  
  
-   A ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] criará uma reserva de URL com base na URL que você especificar nas páginas **URL do Serviço Web** ou **URL do Portal da Web** da ferramenta.  
  
 A instalação e a ferramenta também irão atribuir permissões na URL para o serviço Servidor de Relatório, verificar se existem instâncias duplicadas e adicionar a reserva de URL a HTTP.SYS. Nunca crie ou modifique diretamente uma reserva de URL do Reporting Services usando HttpCfg.exe ou outra ferramenta. Se você pular uma etapa ou definir um valor inválido, ocorrerão problemas difíceis de diagnosticar ou corrigir.  
  
> [!NOTE]  
> HTTP.SYS é um componente do sistema operacional que escuta solicitações de rede e as roteia para uma fila de solicitações. Nesta versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], HTTP.SYS estabelece e mantém a fila de solicitações para o serviço Web Servidor de Relatórios e o portal da Web. O IIS (Serviços de Informações da Internet) não mais é usado para hospedar ou acessar aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para saber mais sobre a funcionalidade HTTP.SYS, confira [HTTP Server API](https://go.microsoft.com/fwlink/?LinkId=92652).  
  
##  <a name="ReportingServicesURLs"></a> URLs no Reporting Services  
 Em uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você pode acessar as seguintes ferramentas, aplicativos e itens usando URLs:  
  
-   serviço Web Servidor de Relatórios  
  
-   Portal da Web  
  
-   Relatórios que foram publicados em um servidor de relatório  
  
 Outros itens endereçáveis por URL publicados, como fontes de dados compartilhadas, não devem ser acessados por meio de URLs como itens autônomos. O servidor de relatório não exibe esses itens em um formato significativo quando vistos em uma janela do navegador.  
  
> [!NOTE]  
> Este artigo não descreve o acesso de URL a relatórios específicos armazenados no servidor de relatório. Para saber mais sobre o acesso de URL a esses itens, veja [Acessar itens do servidor de relatório usando o acesso de URL](../../reporting-services/access-report-server-items-using-url-access.md).  
  
##  <a name="URLreservation"></a> Reserva e registro de URLs  
 Uma reserva de URL define as URLs que podem ser usadas para acessar um aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] reservará uma ou mais URLs para o serviço Web do Servidor de Relatório e o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] no HTTP.SYS e os registrará quando o servidor for iniciado. Ao acrescentar parâmetros à URL, você poderá abrir relatórios usando o serviço Web. As reservas e o registro são fornecidos por HTTP.SYS. Para saber mais, confira [Reservas, registro e roteamento de namespace](https://go.microsoft.com/fwlink/?LinkId=92653).  
  
 *Reserva de URL* consiste em um processo através do qual um ponto de extremidade de URL para um aplicativo Web é criado e armazenado em HTTP.SYS. HTTP.SYS é o repositório comum de todas as reservas de URL que estão definidas em um computador e define um conjunto de regras comuns que garantem reservas de URL exclusivas.  
  
 O*registro de URL* ocorre quando o serviço é iniciado. A fila de solicitações é criada, e HTTP.SYS começa a rotear solicitações para essa fila. Um ponto de extremidade de URL deve ser registrado antes que as solicitações direcionadas a ele sejam adicionadas à fila. Quando o serviço Servidor de Relatório for iniciado, ele registrará todas as URLs reservadas para todos os aplicativos habilitados. Isso significa que o serviço Web deve ser habilitado para que o registro ocorra. Se você definir a propriedade **WebServiceAndHTTPAccessEnabled** como **False** na Configuração da Área da Superfície para a faceta Reporting Services do Gerenciamento Baseado em Políticas, a URL do serviço Web não será registrada quando o serviço for iniciado.  
  
 As URLs terão o registro cancelado se você interromper o serviço ou reciclar o serviço Web ou o domínio do aplicativo do [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] . Se você modificar uma reserva de URL enquanto o serviço estiver em execução, o servidor de relatório reciclará o domínio do aplicativo imediatamente para que o registro da antiga URL seja cancelado e a nova URL possa ser usada.  
  
 Alguns exemplos simples ilustram o conceito de uma reserva de URL e como ela está relacionada aos endereços de URL usados para aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Um ponto importante a ser observado é que a reserva de URL tem sintaxe diferente da URL usada para acessar o aplicativo:  
  
|Reserva de URL em HTTP.SYS|URL|Explicação|  
|---------------------------------|---------|-----------------|  
|`https://+:80/reportserver`|`https://<computername>/reportserver`<br /><br /> `https://<IPAddress>/reportserver`<br /><br /> `https://localhost/reportserver`|A reserva de URL especifica um curinga (+) na porta 80. Esse procedimento coloca na fila do servidor de relatório qualquer solicitação de entrada que especifique um host que seja resolvido para o computador do servidor de relatório na porta 80. Observe que, com essa reserva de URL, pode ser usado qualquer número de URLs para acessar o servidor de relatório.<br /><br /> Essa é a reserva de URL padrão para um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na maioria dos sistemas operacionais.|  
|`https://123.45.67.0:80/reportserver`|`https://123.45.67.0/reportserver`|Essa reserva de URL especifica um endereço IP e é bem mais restritiva do que a reserva de URL curinga. Somente URLs que incluem o endereço IP podem ser usadas para conexão com o servidor de relatório. Devido a essa reserva de URL, uma solicitação a um servidor de relatório em `https://<computername>/reportserver` ou `https://localhost/reportserver` falhará.|  
  
##  <a name="DefaultURLs"></a> URLs padrão  
 Se você instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na configuração padrão, a instalação reservará URLs para o serviço Web Servidor de Relatório e o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Você também pode aceitar esses valores padrão ao definir reservas de URL na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As URLs padrão incluirão um nome de instância se você instalar o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] ou se instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como uma instância nomeada.  
  
> [!IMPORTANT]  
> O caractere de instância é um caractere de sublinhado ( **_** ).  
  
 As reservas de URL incluem um número de porta. Os sistemas operacionais a seguir permitirão que vários aplicativos Web compartilhem uma porta:  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|Tipo de instância|Aplicativo|URL padrão|Reserva de URL real em HTTP.SYS|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|Instância padrão|serviço Web Servidor de Relatórios|`https://\<servername>/reportserver`|`https://<servername>:80/reportserver`|  
|Instância padrão|Portal da Web|`https://<servername>/reportserver`|`https://<servername>:80/reportserver`|  
|Instância nomeada|serviço Web Servidor de Relatórios|`https://<servername>/reportserver_<instancename>`|`https://<servername>:80/reportserver_<instancename>`|  
|Instância nomeada|Portal da Web|`https://<servername>/reports_<instancename>`|`https://<servername>:80/reports_<instancename>`|  
|SQL Server Express|serviço Web Servidor de Relatórios|`https://<servername>/reportserver_SQLExpress`|`https://<servername>:80/reportserver_SQLExpress`|  
|SQL Server Express|Portal da Web|`https://<servername>/reports_SQLExpress`|`https://<servername>:80/reports_SQLExpress`|  
  
##  <a name="URLPermissionsAccounts"></a> Autenticação e identidade de serviço para URLs do Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] As reservas de URL exibem a conta de reserva de URL. A conta do serviço virtual é usada para todas as URLs criadas para os aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] executados na mesma instância.
  
 
 O acesso anônimo é desabilitado porque a segurança padrão é **RSWindowsNegotiate**. Para acesso de intranet, as URLs do servidor de relatório usam nomes de computadores da rede. Para configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para conexões com a Internet, você deve usar configurações diferentes. Para obter mais informações sobre autenticação, veja [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md).  
  
##  <a name="URLlocalAdmin"></a> URLs para administração local  
 Use `https://localhost/reportserver` ou `https://localhost/reports` se tiver especificado um curinga forte ou fraco para a reserva de URL.  
  
 A URL `https://localhost` é interpretada como `https://127.0.0.1`. Se você tiver delimitado a reserva de URL para um nome de computador ou endereço IP único, não poderá usar localhost, a menos que crie uma reserva adicional para 127.0.0.1 no computador local. Da mesma forma, se localhost ou 127.0.0.1 for desabilitado no computador, você não poderá usar essa URL.  
  
 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)], [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] e posterior incluem novos recursos de segurança que minimizam o risco da execução acidental de programas com privilégios elevados. Etapas adicionais são necessárias para habilitar a administração local nesses sistemas operacionais. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="see-also"></a>Confira também  
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Sintaxe de reserva de URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
  