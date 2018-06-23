---
title: Sobre reservas e registro de URL (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 9bffc090c98e1adc507ba55fc856fb166ebd2187
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005643"
---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>Sobre reservas e registro de URL (Gerenciador de configurações do SSRS)
  As URLs para aplicativos do Reporting Services são definidas como reservas de URL em HTTP.SYS. Uma reserva de URL define a sintaxe de um ponto de extremidade de URL para um aplicativo Web. As reservas de URL são definidas para o serviço Web Servidor de Relatório e o Gerenciador de Relatórios quando você configura os aplicativos no servidor de relatório. As reservas de URL são criadas automaticamente quando você configura URLs através da instalação ou da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   A instalação criará reservas de URL usando valores padrão. Se ela instalar a configuração padrão, reservará duas URLs: uma do serviço Web Servidor de Relatório e outra do Gerenciador de Relatórios. Você pode usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para adicionar mais URLs ou modificar as URLs padrão criadas pela instalação.  
  
-   A ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] criará uma reserva de URL com base na URL que você especificar nas páginas **URL do Serviço da Web** ou **URL do Gerenciador de Relatórios** da ferramenta.  
  
 A instalação e a ferramenta também irão atribuir permissões na URL para o serviço Servidor de Relatório, verificar se existem instâncias duplicadas e adicionar a reserva de URL a HTTP.SYS. Nunca crie ou modifique diretamente uma reserva de URL do Reporting Services usando HttpCfg.exe ou outra ferramenta. Se você pular uma etapa ou definir um valor inválido, ocorrerão problemas difíceis de diagnosticar ou corrigir.  
  
> [!NOTE]  
>  HTTP.SYS é um componente do sistema operacional que escuta solicitações de rede e as roteia para uma fila de solicitações. Nesta versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], HTTP.SYS estabelece e mantém a fila de solicitações para o serviço Web Servidor de Relatório e o Gerenciador de Relatórios. O IIS (Serviços de Informações da Internet) não mais é usado para hospedar ou acessar aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre a funcionalidade HTTP.SYS, consulte [HTTP Server API](http://go.microsoft.com/fwlink/?LinkId=92652) no MSDN.  
  
##  <a name="ReportingServicesURLs"></a> URLs no Reporting Services  
 Em uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você pode acessar as seguintes ferramentas, aplicativos e itens usando URLs:  
  
-   serviço Web Servidor de Relatórios  
  
-   Gerenciador de Relatórios  
  
-   Construtor de Relatórios  
  
-   Relatórios que foram publicados em um servidor de relatório  
  
 Outros itens endereçáveis por URL publicados, como modelos e fontes de dados compartilhadas, não devem ser acessados por meio de URLs como itens autônomos. O servidor de relatório não exibe esses itens em um formato significativo quando vistos em uma janela do navegador.  
  
> [!NOTE]  
>  Este tópico não descreve o acesso de URL ao Construtor de Relatórios ou a relatórios específicos armazenados no servidor de relatório. Para obter mais informações sobre o acesso à URL a esses itens, veja [Acessar itens do Servidor de Relatório usando o acesso à URL](../access-report-server-items-using-url-access.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="URLreservation"></a> Reserva e registro de URLs  
 Uma reserva de URL define as URLs que podem ser usadas para acessar um aplicativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] reservará uma ou mais URLs para o serviço Web do servidor de relatório e o Gerenciador de relatório em HTTP. SYS e, em seguida, registrá-los quando o serviço é iniciado. As URLs para o Construtor de Relatórios e os relatórios se baseiam na reserva de URL do serviço Web Servidor de Relatório. Ao anexar parâmetros à URL, você pode abrir o Construtor de Relatórios ou os relatórios usando o serviço Web. As reservas e o registro são fornecidos por HTTP.SYS. Para obter mais informações, consulte [Namespace Reservations, Registration, and Routing](http://go.microsoft.com/fwlink/?LinkId=92653) no MSDN.  
  
 *Reserva de URL* consiste em um processo através do qual um ponto de extremidade de URL para um aplicativo Web é criado e armazenado em HTTP.SYS. HTTP.SYS é o repositório comum de todas as reservas de URL que estão definidas em um computador e define um conjunto de regras comuns que garantem reservas de URL exclusivas.  
  
 O*registro de URL* ocorre quando o serviço é iniciado. A fila de solicitações é criada, e HTTP.SYS começa a rotear solicitações para essa fila. Um ponto de extremidade de URL deve ser registrado antes que as solicitações direcionadas a ele sejam adicionadas à fila. Quando o serviço Servidor de Relatório for iniciado, ele registrará todas as URLs reservadas para todos os aplicativos habilitados. Isso significa que o serviço Web deve ser habilitado para que o registro ocorra. Se você definir a propriedade **WebServiceAndHTTPAccessEnabled** como **False** na Configuração da Área da Superfície para a faceta Reporting Services do Gerenciamento Baseado em Políticas, a URL do serviço Web não será registrada quando o serviço for iniciado.  
  
 As URLs terão o registro cancelado se você interromper o serviço ou reciclar o serviço Web ou o domínio do aplicativo do Gerenciador de Relatórios. Se você modificar uma reserva de URL enquanto o serviço estiver em execução, o servidor de relatório reciclará o domínio do aplicativo imediatamente para que o registro da antiga URL seja cancelado e a nova URL possa ser usada.  
  
 Alguns exemplos simples ilustram o conceito de uma reserva de URL e como ela está relacionada aos endereços de URL usados para aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Um ponto importante a ser observado é que a reserva de URL tem sintaxe diferente da URL usada para acessar o aplicativo.  
  
|Reserva de URL em HTTP.SYS|URL|Explicação|  
|---------------------------------|---------|-----------------|  
|http://+:80/reportserver|http://\<computername > / reportserver<br /><br /> http://\<IPAddress > / reportserver<br /><br /> http://localhost/reportserver|A reserva de URL especifica um curinga (+) na porta 80. Esse procedimento coloca na fila do servidor de relatório qualquer solicitação de entrada que especifique um host que seja resolvido para o computador do servidor de relatório na porta 80. Observe que, com essa reserva de URL, pode ser usado qualquer número de URLs para acessar o servidor de relatório.<br /><br /> Essa é a reserva de URL padrão para um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na maioria dos sistemas operacionais.|  
|http://123.45.67.0:80/reportserver|http://123.45.67.0/reportserver|Essa reserva de URL especifica um endereço IP e é bem mais restritiva do que a reserva de URL curinga. Somente URLs que incluem o endereço IP podem ser usadas para conexão com o servidor de relatório. Devido a essa reserva de URL, uma solicitação para um servidor de relatório em http://\<computername > / reportserver ou http://localhost/reportserver falharia.|  
  
##  <a name="DefaultURLs"></a> URLs padrão  
 Se você instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na configuração padrão, a instalação reservará URLs para o serviço Web Servidor de Relatório e o Gerenciador de Relatórios. Você também pode aceitar esses valores padrão ao definir reservas de URL na ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As URLs padrão incluirão um nome de instância se você instalar o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] ou se instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como uma instância nomeada.  
  
> [!IMPORTANT]  
>  O caractere de instância é um caractere de sublinhado (`_`).  
  
 As reservas de URL incluem um número de porta. Os sistemas operacionais a seguir permitirão que vários aplicativos Web compartilhem uma porta:  
  
1.  [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
2.  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
3.  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
4.  [!INCLUDE[win7](../../includes/win7-md.md)]  
  
5.  [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|Tipo de instância|Aplicativo|URL padrão|Reserva de URL real em HTTP.SYS|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|Instância padrão|serviço Web Servidor de Relatórios|http://\<servername > / reportserver|http://\<servername >: 80/reportserver|  
|Instância padrão|Gerenciador de Relatórios|http://\<servername > / reportserver|http://\<servername >: 80/reportserver|  
|Instância nomeada|serviço Web Servidor de Relatórios|http://\<servername > / ReportServer _\<instancename >|http://\<servername >: 80/ReportServer _\<instancename >|  
|Instância nomeada|Gerenciador de Relatórios|http://\<servername > / Reports _\<instancename >|http://\<servername >: 80/Reports _\<instancename >|  
|SQL Server Express|serviço Web Servidor de Relatórios|http://\<servername > / reportserver_SQLExpress|http://\<servername >: 80/reportserver_SQLExpress|  
|SQL Server Express|Gerenciador de Relatórios|http://\<servername > / reports_SQLExpress|http://\<servername >: 80/reports_SQLExpress|  
  
##  <a name="URLPermissionsAccounts"></a> Autenticação e identidade de serviço para URLs do Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] especificam a conta de serviço do Servidor de Relatório. A conta com a qual o serviço é executado é usada para todas as URLs criadas para os aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] executados na mesma instância. A identidade de serviço da instância do servidor de relatório é armazenada no arquivo RSReportServer.config.  
  
 A conta de serviço não tem valor padrão. Entretanto, é necessário especificar uma conta de serviço durante a instalação em `URLReservation` no arquivo RSReportServer.config, mesmo que você instale o servidor no modo somente arquivos. Os valores válidos para a conta de serviço incluem uma conta de usuário de domínio, `LocalSystem` ou `NetworkService`.  
  
 Acesso anônimo é desabilitado porque a segurança padrão é `RSWindowsNegotiate`. Para acesso de intranet, as URLs do servidor de relatório usam nomes de computadores da rede. Para configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para conexões com a Internet, você deve usar configurações diferentes. Para obter mais informações sobre autenticação, veja [Autenticação com o Servidor de Relatório](../security/authentication-with-the-report-server.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="URLlocalAdmin"></a> URLs para administração local  
 Use http://localhost/reportserver ou http://localhost/reports se tiver especificado um curinga forte ou fraco para a reserva de URL.  
  
 A URL http://localhost é interpretada como http://127.0.0.1. Se você tiver delimitado a reserva de URL para um nome de computador ou endereço IP único, não poderá usar localhost, a menos que crie uma reserva adicional para 127.0.0.1 no computador local. Da mesma forma, se localhost ou 127.0.0.1 for desabilitado no computador, você não poderá usar essa URL.  
  
 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] e [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] incluem novos recursos de segurança para minimizar o risco de acidentalmente executar programas com privilégios elevados. Etapas adicionais são necessárias para habilitar a administração local nesses sistemas operacionais. Para obter instruções, veja [Configure a Native Mode Report Server for Local Administration &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
##  <a name="URLSharePoint"></a> URLs para o servidor de relatório no modo integrado do SharePoint  
 Se um servidor de relatório autônomo for configurado para ser executado em uma implantação maior de um produto ou tecnologia do SharePoint, a construção da URL e do diretório virtual será afetada das seguintes maneiras:  
  
-   As URLs de relatórios e outros itens são endereçadas pela URL do aplicativo Web do SharePoint. Para o acesso de URL a relatórios específicos, sempre use uma URL totalmente qualificada que inclua o caminho do site, a biblioteca de documentos, o nome do item e uma extensão de nome de arquivo (como .rdl de um relatório). Você deve especificar URLs totalmente qualificadas quando fizer referência a fontes de dados compartilhadas e modelos em relatórios e quando especificar um servidor de destino e pastas para operações de publicação em um servidor de relatório.  
  
-   A extensão de nome de arquivo é usada para distinguir entre tipos diferentes de itens de servidor de relatório. As extensões válidas incluem .rdl para definições de relatório, .smdl para modelos de relatório e .rsds para fontes de dados compartilhadas criadas para um site do SharePoint.  
  
-   Embora os produtos e as tecnologias do SharePoint tenham reservas de URL definidas para eles, você pode ignorar a reserva quando publicar no servidor. Para aplicativos Web do SharePoint, a reserva de URL é uma operação interna.  
  
-   Para implantações de servidor único em que um servidor de relatório integrado e uma instância de tecnologia do SharePoint estão instalados no mesmo computador, você não pode usar http://localhost/reportserver. Se http://localhost é usado para acessar o aplicativo Web do SharePoint, você deve usar um site diferente do padrão ou uma atribuição de porta exclusivos para acessar um servidor de relatório. Além disso, se o servidor de relatório for integrado a um farm do SharePoint, o acesso de localhost a um servidor de relatório não será resolvido para nós da implantação que estejam instalados em computadores remotos.  
  
-   A reserva de URL e o ponto de extremidade do Gerenciador de Relatórios não podem ser configurados para um servidor de relatório executado no modo integrado do SharePoint. Se você configurá-lo, ele não funcionará mais depois que você implantar um servidor de relatório no modo integrado do SharePoint. O Gerenciador de Relatórios não tem suporte nesse modo.  
  
 Se você tiver integrado uma implantação em expansão do servidor de relatório para ser executada em uma implantação maior de um produto ou tecnologia do SharePoint, balanceie a carga dos nós do servidor de relatório e defina uma única URL do servidor virtual para a implantação em expansão. As configurações de integração do Servidor de Relatório permitem especificar uma única URL do servidor de relatório. No caso de uma implantação em expansão, a URL deve ser o ponto de acesso dos nós do servidor na implantação em expansão.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](configure-a-url-ssrs-configuration-manager.md)   
 [Sintaxe de reserva de URL &#40;SSRS Configuration Manager&#41;](url-reservation-syntax-ssrs-configuration-manager.md)  
  
  