---
title: Configuração avançada de vários sites da Web (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.advancedmultiplewebsiteconfig.F1
ms.assetid: af4ede43-2225-45b5-ae7e-9202411551ba
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d6860e41991d00e6cd0c2869413dca110422c4e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63226008"
---
# <a name="advanced-multiple-web-site-configuration-ssrs-native-mode"></a>Configuração avançada de vários sites (modo nativo do SSRS)
  Use esta caixa de diálogo para criar e gerenciar as URLs usadas para acessar um servidor de relatório ou um Gerenciador de Relatórios. A caixa de diálogo **Configuração Avançada de Vários Sites** é usada para criar URLs adicionais, URLs personalizadas que incluem um nome de cabeçalho de host ou para especificar um endereço IP no formato IPv4 ou IPv6.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 A criação de várias URLs será útil se você deseja configurar formas diferentes para acessar um servidor de relatório. Por exemplo, o acesso ao servidor de relatório por uma conexão intranet e extranet normalmente requer a existência de URLs diferentes para cada tipo de conexão.  
  
 Para abrir a caixa de diálogo **Configuração Avançada de Vários Sites** , clique em **Avançada** na página **URL do Serviço Web** ou **URL do Gerenciador de Relatórios** no Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Depois que a caixa de diálogo **Configuração Avançada de Vários Sites** for aberta, você poderá clicar em **Adicionar** ou **Editar** para definir novas URLs, ou ainda modificar ou excluir URLs existentes.  
  
 Clique em **OK** para salvar as alterações. Se você adicionar ou remover URLs, mas depois fechar a caixa de diálogo sem primeiro clicar em **OK**, suas alterações serão perdidas.  
  
## <a name="options"></a>Opções  
 **Endereço IP**  
 Identifica o computador do servidor de relatório em uma rede TCP/IP. Os valores válidos incluem:  
  
-   **Todos Atribuídos** especifica que qualquer um dos endereços IP atribuídos ao computador podem ser usados em uma URL que aponta para um aplicativo do servidor de relatório. Esse valor também abrange nomes de host amigáveis (como nomes de computadores) que podem ser resolvidos por um servidor de nome de domínio para um endereço IP que é atribuído ao computador. Esse é o valor padrão para uma URL do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   **Nenhum Atribuído** especifica que o servidor de relatório aceitará qualquer solicitação que não tenha uma correspondência exata para o endereço IP ou o nome do host. Não use esse valor se outro aplicativo Web já o estiver usando. Se isso for feito, você interromperá o serviço para o outro aplicativo.  
  
-   **127.0.0.1** é usado para acessar localhost. Ele dá suporte à administração local no computador do servidor de relatório. Se você selecionar apenas esse valor, somente os usuários que fizerem logon localmente no computador do servidor de relatório terão acesso ao aplicativo.  
  
-   *Nnn.nnn.nnn.nnn* é o endereço IPv4 de uma placa de adaptador de rede em seu computador. Se sua rede usar endereçamento IPv6, o endereço IP será um valor de 128 bits de 8 campos de 4 bytes semelhante ao seguinte formato: \<cabeçalho >:*nnnn:nnnn:nnnn:nnnn*.  
  
     Se você tiver várias placas, verá um endereço IP para cada uma. Se você selecionar apenas esse valor, isso limitará o acesso do aplicativo somente ao endereço IP (e qualquer nome de host que um servidor de nome de domínio mapear para esse endereço). Você não pode usar localhost para acessar um servidor de relatório e não pode usar os endereços IP de outras placas de adaptador de rede que estejam instaladas no computador do servidor de relatório.  
  
 **Porta**  
 Especifica a porta que o servidor de relatório monitora por solicitações. A porta 80 é a padrão. Se você usar a porta 80, não precisará incluí-la na URL. Se você usar qualquer outro número de porta, você sempre deve incluí-lo na URL (por exemplo, http://localhost:8181/reports).  
  
 **Cabeçalho de Host**  
 Se você já tiver um cabeçalho de host definido em um servidor de nome de domínio que seja resolvido para seu computador, poderá especificar esse cabeçalho de host em uma URL que você configure para acesso ao servidor de relatório.  
  
 Um cabeçalho de host é um nome exclusivo que permite que vários sites compartilhem um único endereço IP e porta. Os nomes de cabeçalho de host são mais fáceis de se lembrar e digitar que endereço IP e números de porta. Um exemplo de um nome de cabeçalho de host poderia ser www.adventure-works.com.  
  
 **Porta SSL**  
 Especifica a porta para conexões SSL. A porta padrão para SSL é 443.  
  
 **Certificado SSL**  
 Especifica o nome de um certificado SSL que você instalou neste computador. Se o certificado for mapeado para um curinga, você poderá usá-lo para uma conexão de servidor de relatório.  
  
 Especifica o nome do computador totalmente qualificado para o qual o certificado está registrado. O nome que você especificar deve ser idêntico ao nome para o qual o certificado está registrado.  
  
 Você deve ter um certificado instalado para que possa usar essa opção. Você também deve modificar o parâmetro de configuração UrlRoot no arquivo RSReportServer.config para que ele especifique o nome totalmente qualificado do computador para o qual o certificado está registrado. Para obter mais informações, veja [Configurar conexões SSL em um Servidor de Relatórios do Modo Nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Emitido para**  
 Mostra o nome do computador para o qual o certificado foi criado.  
  
 **Adicionar**  
 Defina uma URL adicional.  
  
 **Editar**  
 Modifique qualquer parte da sintaxe da URL.  
  
 **Remover**  
 Desmarque uma entrada de URL da lista.  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
