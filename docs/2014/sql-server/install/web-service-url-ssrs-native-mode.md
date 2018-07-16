---
title: URL do serviço (modo nativo do SSRS) Web | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.reportservervirtualdirectory.F1
helpviewer_keywords:
- Reporting Services, Web service
ms.assetid: 9d210b5d-2a08-4e56-a4f5-c16715b00d79
caps.latest.revision: 9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 21a9ede5ef83169d312bb59e84bfd3f33619dafb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270232"
---
# <a name="web-service-url-ssrs-native-mode"></a>URL do serviço Web (modo nativo do SSRS)
  Use a página URL do Serviço Web para configurar ou modificar a URL usada para acessar o servidor de relatório. Uma *reserva de URL* será criada com base na URL que você especificar. A reserva de URL define a sintaxe e as regras para todas as URLs que podem ser subsequentemente usadas para acessar o serviço Web Servidor de Relatório. Ela especifica o prefixo, o host, a porta e o diretório virtual do serviço Web Servidor de Relatório. Dependendo de como você especifica o host, várias URLs poderiam ser possíveis para uma única reserva. O valor padrão do host especifica um curinga forte. Um curinga forte permite especificar em uma URL qualquer nome de host que possa ser resolvido para o computador que hospeda o servidor de relatório. Para obter mais informações sobre reservas e a configuração de URL, consulte [configurar uma URL &#40;Configuration Manager do SSRS&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) e [configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41; ](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para abrir essa página, inicie o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager e clique em **URL do serviço Web** no painel de navegação. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 Essa página fornece valores que são geralmente usados em URLs de servidor de relatório. Para criar URLs adicionais, usar cabeçalhos de host ou especificar o endereço IP em um formato específico, clique em **Avançado**.  
  
 Um link para o serviço Web aparecerá nessa página depois que você clicar em **Aplicar**. Se você clicar nesse link antes que o banco de dados do servidor de relatório seja criado, poderá esperar que apareça um erro "Página Não Encontrada". Esse erro não mais aparecerá depois que o banco de dados for configurado. Para obter mais informações, consulte [Criar um banco de dados de servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 Se você tiver reinstalado [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e encontre o que você obtiver erros ao tentar usar o valor do endereço IP padrão todos atribuídos e a porta 80, normalmente poderá resolver o erro recriando a URL depois de reiniciar o serviço.  
  
## <a name="options"></a>Opções  
 **Diretório virtual**  
 Especifica o nome do diretório virtual para o serviço Web Servidor de Relatório. Você pode ter apenas um nome virtual para cada instância do serviço Web Servidor de Relatório no mesmo computador.  
  
 **Endereço IP**  
 Identifica o computador do servidor de relatório em uma rede TCP/IP. Os valores válidos incluem:  
  
-   **Todos Atribuídos** especifica que qualquer um dos endereços IP atribuídos ao computador podem ser usados em uma URL que aponta para um aplicativo do servidor de relatório. Esse valor também abrange nomes de host amigáveis (como nomes de computadores) que podem ser resolvidos por um servidor de nome de domínio para um endereço IP que é atribuído ao computador. Esse é o valor padrão para uma URL do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   **Nenhum Atribuído** especifica que o servidor de relatório aceitará qualquer solicitação que não tenha uma correspondência exata para o endereço IP ou o nome do host. Não use esse valor se outro aplicativo Web já o estiver usando. Se isso for feito, você interromperá o serviço para o outro aplicativo.  
  
-   **127.0.0.1** é usado para acessar localhost. Ele dá suporte à administração local no computador do servidor de relatório. Se você selecionar apenas esse valor, somente os usuários que fizerem logon localmente no computador do servidor de relatório terão acesso ao aplicativo.  
  
-   *Nnn.nnn.nnn.nnn* é o endereço IPv4 de uma placa de adaptador de rede em seu computador. Se sua rede usar endereçamento IPv6, o endereço IP será um valor de 128 bits de 8 campos de 4 bytes semelhante ao seguinte formato: \<cabeçalho >:*nnnn:nnnn:nnnn:nnnn*  
  
     Se você tiver várias placas, verá um endereço IP para cada uma. Se você selecionar apenas esse valor, isso limitará o acesso do aplicativo somente ao endereço IP (e qualquer nome de host que um servidor de nome de domínio mapear para esse endereço). Você não pode usar localhost para acessar um servidor de relatório e não pode usar os endereços IP de outras placas de adaptador de rede que estejam instaladas no computador do servidor de relatório.  
  
 **Porta TCP**  
 Especifica a porta que o servidor de relatório monitora para solicitações HTTP de URLs que incluam o nome do diretório virtual do servidor de relatório.  
  
 **Certificado SSL**  
 Associa um certificado ao endereço IP que você especificou. O certificado deve estar instalado e configurado no computador. O Reporting Services não fornece recursos para o gerenciamento de certificados. O certificado deve ser emitido para um nome de host ou um nome de computador que seja resolvido para o endereço IP. Por exemplo, para usar um certificado que foi emitido para http://salesreports, o endereço IP especificado deve ser resolvido para um servidor denominado "salesreports".  
  
 Se você usar um certificado, você deve modificar o `UrlRoot` arquivo de definição de configuração em rsreportserver. config para que ele especifique o nome totalmente qualificado do computador para o qual o certificado está registrado. Para obter mais informações, veja [Configurar conexões SSL em um Servidor de Relatórios do Modo Nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Porta SSL**  
 Especifica a porta para conexões SSL.  
  
 **URLs**  
 Exibe as URLs definidas para a instância atual do servidor de relatório.  
  
 **Avançado**  
 Clique para criar URLs adicionais para a instância atual do aplicativo.  
  
> [!NOTE]  
>  Se você tiver Associações SSL existentes e Reservas de URL e desejar alterar a Associação de SSL, por exemplo usar um certificado diferente ou cabeçalho de host, é recomendado concluir as etapas a seguir na ordem:  
>   
>  1.  Primeiro remova todas as Reservas de URL.  
> 2.  Em seguida, remova todas as Associações SSL.  
> 3.  Em seguida, recrie as URLs e as associações SSL.  
>   
>  As etapas anteriores podem ser concluídas usando o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
>   
>  A Microsoft Windows dá suporte a uma associação para cada endereço IP para a combinação de porta. Se você configurar um servidor de relatório para usar um valor de cabeçalho de host específico e o certificado na combinação Porta para endereço IP também for emitido para um valor de cabeçalho de host diferente, você verá em seu navegador um aviso indicando que o certificado não corresponde à URL que está sendo usada.  
>   
>  Para corrigir o problema, exclua todas as associações e crie novas associações com configurações exclusivas ou configure os registros de URL do Reporting Services com curingas.  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
