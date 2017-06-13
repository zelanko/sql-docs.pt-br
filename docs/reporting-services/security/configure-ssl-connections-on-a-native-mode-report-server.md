---
title: "Configurar conexões SSL em um servidor de relatório do modo nativo | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Secure Sockets Layer (SSL)
ms.assetid: 212f2042-456a-4c0a-8d76-480b18f02431
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4f973faa65ed34695804de0815331f562b7a24f4
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="configure-ssl-connections-on-a-native-mode-report-server"></a>Configurar conexões SSL em um servidor de relatórios de modo nativo
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O modo Nativo usa o serviço HTTP SSL (protocolo SSL) para estabelecer conexões criptografadas com um servidor de relatório. Se você tiver um arquivo de certificado (.cer) instalado em um repositório de certificados local no computador do servidor de relatório, poderá associá-lo a uma reserva de URL do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para dar suporte a conexões do servidor de relatório por meio de um canal criptografado.  
  
> [!TIP]  
>  Se você estiver usando o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte a documentação do SharePoint para obter mais informações. Por exemplo [Como habilitar o SSL em um aplicativo Web do SharePoint 2010 (http://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx)](http://blogs.msdn.com/b/sowmyancs/archive/2010/02/12/how-to-enable-ssl-on-a-sharepoint-web-application.aspx).  
  
 Como o IIS (Serviços de Informações da Internet) também usa HTTP SSL, existem problemas de interoperabilidade consideráveis que você deve considerar se executa o IIS e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no mesmo computador. Leia a seção Problemas de interoperabilidade com IIS para obter orientação sobre como lidar com esses problemas.  
  
## <a name="server-certificate-requirements"></a>Requisitos de certificado de servidor  
 Deve haver um certificado de servidor instalado no computador (não há suporte para certificados de cliente). O Reporting Services não fornece funcionalidade de solicitação, geração, download ou instalação de um certificado. [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] fornece um snap-in de Certificados que pode ser usado para solicitar um certificado de uma autoridade de certificação confiável.  
  
 Para fins de teste, você pode gerar um certificado localmente. Se você usar o utilitário **MakeCert** e o comando de exemplo como modelo, especifique o nome do seu servidor como o host e remova todas as quebras de linha antes de executar o comando. Caso execute o comando em uma janela do DOS, poderá ser necessário aumentar o tamanho do buffer da janela para acomodar o comando inteiro.  
  
 Se você estiver executando o IIS e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em conjunto no mesmo computador, poderá usar o aplicativo de console [!INCLUDE[iismgr](../../includes/iismgr-md.md)] para obter o certificado instalado em seu computador. [!INCLUDE[iismgr](../../includes/iismgr-md.md)] inclui opções para criar e empacotar um arquivo de solicitação de certificado (.crt) para processamento posterior por uma autoridade de certificação confiável. A autoridade de certificação que você está usando irá gerar um arquivo de certificado (.cer) e o enviará de volta para você. Você pode usar o Console de Gerenciamento do IIS para instalar o arquivo de certificado no repositório local. Para obter mais informações, consulte o tópico sobre [como usar SSL para criptografar dados confidenciais](http://go.microsoft.com/fwlink/?LinkId=71123) no Technet.  
  
## <a name="interoperability-issues-with-iis"></a>Problemas de interoperabilidade com o IIS  
 A presença do IIS no mesmo computador que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] afetará significativamente as conexões SSL com um servidor de relatório:  
  
-   Se o IIS estiver instalado, o serviço World Wide Web (W3SVC) sempre deverá estar em execução. O serviço HTTP SSL criará uma dependência do IIS caso detecte que ele está em execução. Isso significa que o serviço W3SVC (World Wide Web) deverá estar em execução sempre que o IIS e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estiverem instalados no mesmo computador e que você deve configurar URLs de servidor de relatório para conexões SSL.  
  
-   A desinstalação do IIS pode interromper o serviço temporariamente em uma URL de servidor de relatório associada por SSL. Por esse motivo, é estritamente recomendável que você reinicie o computador após a desinstalação do IIS.  
  
     A reinicialização do computador é necessária para apagar todas as sessões SSL do cache. Alguns sistemas operacionais armazenam as sessões SSL em cache por até 10 horas, fazendo com que uma URL https:// continue a funcionar mesmo depois que a associação SSL tenha sido removida da reserva de URL em HTTP.SYS. A reinicialização do computador fecha todas as conexões abertas que usam o canal.  
  
## <a name="bind-ssl-to-a-reporting-services-url-reservation"></a>Associar o SSL a uma reserva de URL do Reporting Services  
 As etapas a seguir não incluem instruções sobre como solicitar, gerar, baixar ou instalar um certificado. Você deve ter um certificado instalado e disponível para uso. As propriedades do certificado especificadas, a autoridade de certificação da qual ele é obtido e as ferramentas e os utilitários que você usa para instalar o certificado são os de sua preferência.  
  
 Você pode usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para associar o certificado. Se o certificado estiver instalado corretamente no repositório do computador local, a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o detectará e exibirá na lista **Certificados SSL** das páginas **URL do Serviço da Web** e **URL do Gerenciador de Relatórios** .  
  
### <a name="to-configure-a-report-server-url-for-ssl"></a>Para configurar a URL de um servidor de relatório para SSL  
  
1.  Inicie a ferramenta Configuração do Reporting Services e conecte-se ao servidor de relatório.  
  
2.  Clique em **URL do Serviço Web**.  
  
3.  Expanda a lista de certificados SSL. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] detecta certificados de autenticação de servidor no repositório local. Se você instalou um certificado mas ele não aparece na lista, talvez seja necessário reiniciar o serviço. Para reiniciar o serviço, use os botões **Parar** e **Iniciar** da página **Status do Servidor de Relatório** na ferramenta Configuração do Reporting Services.  
  
4.  Selecione o certificado.  
  
5.  Clique em **Aplicar**.  
  
6.  Clique na URL para verificar se está funcionando.  
  
 A configuração de banco de dados do servidor de relatório é um requisito para testar a URL. Se você ainda não criou o banco de dados do servidor de relatório, faça-o antes de testar a URL.  
  
 As reservas de URL para o Gerenciador de Relatórios e o serviço Web Servidor de Relatórios são configuradas de maneira independente. Se você também quiser configurar o acesso ao Gerenciador de Relatórios por meio de um canal criptografado por SSL, continue com as próximas etapas:  
  
1.  Clique em **URL do Gerenciador de Relatórios**.  
  
2.  Clique em **Avançado**.  
  
3.  Em **Multiplicar Identidades SSL para o Gerenciador de Relatórios**, clique em **Adicionar**.  
  
4.  Selecione o certificado, clique em **OK**e, depois, em **Aplicar**.  
  
5.  Clique na URL para verificar se está funcionando.  
  
## <a name="how-certificate-bindings-are-stored"></a>Como são armazenadas as associações de certificado  
 As associações de certificado serão armazenadas em HTTP.SYS. Uma representação das associações definidas também será armazenada na seção **URLReservations** do arquivo RSReportServer.config. As configurações no arquivo de configuração são apenas uma representação dos valores reais especificados em outros lugares. Não modifique os valores diretamente no arquivo de configuração. Os parâmetros de configuração só serão exibidos no arquivo depois que você usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou o provedor WMI do Servidor de Relatório para associar um certificado.  
  
> [!NOTE]  
>  Se você configurar uma associação com um certificado SSL no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e depois quiser remover o certificado do computador, não se esqueça de remover a associação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , antes de remover o certificado do computador. Caso contrário, você não poderá remover a associação usando a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou WMI, e receberá um erro de "Parâmetro inválido". Caso você já tenha removido o certificado do computador, use a ferramenta Httpcfg.exe para remover a associação de HTTP.SYS. Para obter mais informações sobre Httpcfg.exe, consulte a documentação de produto do Windows.  
  
 As associações SSL são um recurso compartilhado no Microsoft Windows. As alterações feitas pelo Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou outras ferramentas como o Gerenciador do IIS podem afetar outros aplicativos no mesmo computador. É uma prática recomendada usar a mesma ferramenta para editar associações que você usou para criar as associações.  Por exemplo se você criou associações de SSL usando o Gerenciador de Configurações, então é recomendado que você use o Gerenciador de Configurações para gerenciar o ciclo de vida das associações. Se você usar o Gerenciador do IIS para criar associações, é recomendado usar o Gerenciador do IIS para gerenciar o ciclo de vida das associações. Se o IIS estiver instalado no computador antes de o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ser instalado, será uma prática recomendada revisar a configuração do SSL no IIS antes de configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Se você remover as associações do SSL do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando o Gerenciador de Configurações do Reporting Services, o SSL poderá não mais funcionar para sites em um servidor que está executando o IIS (Serviços de Informações da Internet) ou em outro servidor de HTTP.SYS. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] remove a chave do Registro a seguir. Quando esta chave do Registro é removida, a associação do SSL para o IIS também é removida. Sem esta associação, o SSL não é fornecido para o protocolo HTTP. Para diagnosticar este problema, use o Gerenciador do IIS ou o utilitário da linha de comando HTTPCFG.exe. Para resolver o problema, restaure a associação SSL para seus sites usando o Gerenciador do IIS. Para impedir este problema no futuro, use o Gerenciador do IIS para remover as associações SSL e em seguida use o Gerenciador do IIS para restaurar a associação para os sites desejados. Para obter mais informações, consulte o artigo da base de dados de conhecimento [O SSL não funciona mais depois de remover uma associação SSL (http://support.microsoft.com/kb/956209/n)](http://support.microsoft.com/kb/956209/n).  
  
## <a name="see-also"></a>Consulte também  
 [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
