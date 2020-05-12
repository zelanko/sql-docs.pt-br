---
title: Configurar conexões TLS em um servidor de relatório no modo nativo | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Secure Sockets Layer (SSL)
ms.assetid: 212f2042-456a-4c0a-8d76-480b18f02431
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8c2bd66eacb5a91def2a9f6c9f7cb2e807e404f1
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886493"
---
# <a name="configure-tls-connections-on-a-native-mode-report-server"></a>Configurar conexões TLS em um servidor de relatório no modo nativo
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O modo Nativo usa o serviço HTTP SSL (protocolo SSL) para estabelecer conexões criptografadas com um servidor de relatório. O protocolo TLS era anteriormente conhecido como protocolo SSL. Se você tiver um arquivo de certificado (.cer) instalado em um repositório de certificados local no computador do servidor de relatório, poderá associá-lo a uma reserva de URL do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para dar suporte a conexões do servidor de relatório por meio de um canal criptografado.  
  
> [!TIP]  
>  Se você estiver usando o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte a documentação do SharePoint para obter mais informações. Por exemplo, [Como habilitar o TLS em um aplicativo Web do SharePoint 2010](https://docs.microsoft.com/archive/blogs/sowmyancs/how-to-enable-ssl-on-a-sharepoint-2010-web-application).  
  
 Como o IIS (Serviços de Informações da Internet) também usa HTTP SSL, existem problemas de interoperabilidade consideráveis que você deve considerar se executa o IIS e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no mesmo computador. Leia a seção Problemas de interoperabilidade com IIS para obter orientação sobre como lidar com esses problemas.  
  
## <a name="server-certificate-requirements"></a>Requisitos de certificado do servidor  
 Deve haver um certificado de servidor instalado no computador (não há suporte para certificados de cliente). O Reporting Services não fornece funcionalidade de solicitação, geração, download ou instalação de um certificado. O Windows Server 2012 e posterior fornece um snap-in de Certificados que pode ser usado para solicitar um certificado de uma autoridade de certificação confiável.  
  
 Para fins de teste, você pode gerar um certificado localmente. Se você usar o utilitário **MakeCert** e o comando de exemplo como modelo, especifique o nome do seu servidor como o host e remova todas as quebras de linha antes de executar o comando. Caso execute o comando em uma janela do DOS, poderá ser necessário aumentar o tamanho do buffer da janela para acomodar o comando inteiro.  
  
 Se você estiver executando o IIS e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em conjunto no mesmo computador, poderá usar o aplicativo de console Gerenciador do IIS para obter o certificado instalado em seu computador. O Gerenciador do IIS inclui opções para criar e empacotar um arquivo de solicitação de certificado (.crt) para processamento posterior por uma autoridade de certificação confiável. A autoridade de certificação que você está usando irá gerar um arquivo de certificado (.cer) e o enviará de volta para você. Você pode usar o Console de Gerenciamento do IIS para instalar o arquivo de certificado no repositório local. Para obter mais informações, consulte o tópico sobre [como usar SSL para criptografar dados confidenciais](https://go.microsoft.com/fwlink/?LinkId=71123) no Technet.  
  
## <a name="interoperability-issues-with-iis"></a>Problemas de interoperabilidade com o IIS  
 A presença do IIS no mesmo computador que o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] afetará significativamente as conexões TLS com um servidor de relatório:  
  
-   Se o IIS estiver instalado, o serviço World Wide Web (W3SVC) sempre deverá estar em execução. O serviço HTTP SSL criará uma dependência do IIS caso detecte que ele está em execução. Isso significa que o serviço W3SVC (World Wide Web) deverá estar em execução sempre que o IIS e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estiverem instalados no mesmo computador e que você deve configurar URLs de servidor de relatório para conexões TLS.  
  
-   A desinstalação do IIS pode interromper o serviço temporariamente em uma URL de servidor de relatório associada por TLS. Por esse motivo, recomendamos que você reinicie o computador após a desinstalação do IIS.  
  
     A reinicialização do computador é necessária para apagar todas as sessões TLS do cache. Alguns sistemas operacionais armazenam as sessões TLS em cache por até 10 horas, fazendo com que uma URL https:// continue a funcionar mesmo depois que a associação TLS tenha sido removida da reserva de URL em HTTP.SYS. A reinicialização do computador fecha todas as conexões abertas que usam o canal.  
  
## <a name="bind-tls-to-a-reporting-services-url-reservation"></a>Associar o TLS a uma reserva de URL dos serviços de relatório  
 As etapas a seguir não incluem instruções sobre como solicitar, gerar, baixar ou instalar um certificado. Você deve ter um certificado instalado e disponível para uso. As propriedades do certificado especificadas, a autoridade de certificação da qual ele é obtido e as ferramentas e os utilitários que você usa para instalar o certificado são os de sua preferência.  
  
 Você pode usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para associar o certificado. Se o certificado estiver instalado corretamente no repositório do computador local, a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o detectará e exibirá na lista **Certificados SSL** das páginas **URL do Serviço da Web** e **URL do Portal da Web**.  
  
### <a name="to-configure-a-report-server-url-for-tls"></a>Para configurar a URL de um servidor de relatório para TLS  
  
1.  Inicie a ferramenta Configuração do Reporting Services e conecte-se ao servidor de relatório.  
  
2.  Selecione **URL do Serviço Web**.  
  
3.  Expanda a lista de certificados TLS/SSL. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] detecta certificados de autenticação de servidor no repositório local. Se você instalou um certificado mas ele não aparece na lista, talvez seja necessário reiniciar o serviço. Para reiniciar o serviço, use os botões **Parar** e **Iniciar** da página **Status do Servidor de Relatório** na ferramenta Configuração do Reporting Services (página superior).  
  
4.  Selecione o certificado.  
  
5.  Clique em **Aplicar**.  
  
6.  Clique na URL para verificar se está funcionando.  
  
 A configuração de banco de dados do servidor de relatório é um requisito para testar a URL. Se você ainda não criou o banco de dados do servidor de relatório, faça-o antes de testar a URL.  
  
 As reservas de URL da URL do Portal da Web e da URL dos Serviços Web do Servidor de Relatórios são configuradas de maneira independente. Se você também quiser configurar o acesso ao portal da Web por meio de um canal criptografado por TLS, continue com as próximas etapas:  
  
1.  Acesse a **URL do portal da Web**.
  
2.  Selecione **Avançado**.  
  
3.  Em **Múltiplas Identidades HTTPS para o recurso Reporting Services atual**, selecione **Adicionar**.  
  
4.  Selecione o certificado, selecione **OK** e selecione **Aplicar**.  
  
5.  Teste a URL para verificar se está funcionando.  
  
## <a name="how-certificate-bindings-are-stored"></a>Como as associações de certificado são armazenadas  
 As associações de certificado serão armazenadas em HTTP.SYS. Uma representação das associações definidas também será armazenada na seção **URLReservations** do arquivo RSReportServer.config. As configurações no arquivo de configuração são apenas uma representação dos valores reais especificados em outros lugares. Não modifique os valores diretamente no arquivo de configuração. Os parâmetros de configuração só serão exibidos no arquivo depois que você usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou o provedor WMI do Servidor de Relatório para associar um certificado.  
  
> [!NOTE]  
>  Se você configurar uma associação com um certificado TLS/SSL no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e depois quiser remover o certificado do computador, não se esqueça de remover a associação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes de remover o certificado do computador. Caso contrário, você não poderá remover a associação usando a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou WMI, e receberá um erro de "Parâmetro inválido". Caso você já tenha removido o certificado do computador, use a ferramenta Httpcfg.exe para remover a associação de HTTP.SYS. Para obter mais informações sobre Httpcfg.exe, consulte a documentação de produto do Windows.  
  
 As associações TLS são um recurso compartilhado no Microsoft Windows. As alterações feitas pelo Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou outras ferramentas como o Gerenciador do IIS podem afetar outros aplicativos no mesmo computador. É uma prática recomendada usar a mesma ferramenta para editar associações que você usou para criar as associações.  Por exemplo, se você criou associações TLS usando o Configuration Manager, recomendamos usar o Configuration Manager para gerenciar o ciclo de vida das associações. Se você usar o Gerenciador do IIS para criar associações, é recomendado usar o Gerenciador do IIS para gerenciar o ciclo de vida das associações. Se o IIS estiver instalado no computador antes da instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], será uma prática recomendada revisar a configuração do TLS no IIS antes de configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Se você remover as associações TLS do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando o Gerenciador de Configurações do Reporting Services, o TLS poderá não mais funcionar para sites em um servidor que está executando o IIS (Serviços de Informações da Internet) ou em outro servidor de HTTP.SYS. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] O Configuration Manager remove a seguinte chave do Registro: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters\SslBindingInfo\0.0.0.0:443** Quando essa chave do Registro é removida, o mesmo ocorre com a associação TLS para o IIS. Sem essa associação, o TLS não é fornecido para o protocolo HTTPS. Para diagnosticar esse problema, use o Gerenciador do IIS ou o utilitário de linha de comando HTTPCFG.exe. Para resolver o problema, restaure a associação TLS de seus sites usando o Gerenciador do IIS. Para evitar esse problema no futuro, use o Gerenciador do IIS para remover as associações TLS e, em seguida, use o Gerenciador do IIS para restaurar a associação dos sites desejados. Para saber mais, veja o artigo da base de dados de conhecimento [O SSL não funciona mais depois de remover uma associação SSL (https://support.microsoft.com/kb/956209/n)](https://support.microsoft.com/kb/956209/n).  
  
## <a name="see-also"></a>Confira também  
 [Autenticação com o servidor de relatório](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
