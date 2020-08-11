---
title: Configurar um servidor de relatório em um cluster com balanceamento de carga de rede | Microsoft Docs
description: Saiba como configurar uma expansão do servidor de relatório para ser executada em um NLB. Implemente uma solução de cluster NLB para dar suporte a uma implantação de expansão do Reporting Services.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.date: 12/11/2019
ms.openlocfilehash: b8bd6d8e99549cb6228a46f04b1532bbf872a066
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545568"
---
# <a name="configure-a-report-server-on-a-network-load-balancing-cluster"></a>Configurar um servidor de relatório em um cluster com balanceamento de carga de rede

  Se você estiver configurando uma expansão do servidor de relatório a ser executada em um cluster NLB (Balanceamento de Carga de Rede), deverá fazer o seguinte:  
  
- Verifique se o cluster NLB pode ser acessado através de um nome de servidor virtual que mapeia para o endereço IP do servidor virtual. Um nome de servidor virtual é necessário para que você possa configurar um único ponto de entrada para o cluster NLB. Quando você configurar uma URL para cada instância do servidor de relatório, especificará o nome do servidor virtual como host.  
  
- Configure a validação do estado de exibição para permitir a exibição de relatórios interativos. Esses relatórios costumam ser renderizados inúmeras vezes durante uma única sessão de usuário para exibir dados novos ou diferentes em resposta a ações do usuário. Quando você configura a validação do estado de exibição, a continuidade é preservada na sessão de usuário, independentemente dos serviços do servidor de relatório solicitados.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece a funcionalidade para balancear a carga de uma implantação em expansão ou para definir um único ponto de acesso através de uma URL compartilhada. Você deve implementar uma solução separada de software ou hardware de cluster NLB para dar suporte a uma implantação em expansão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Você pode instalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em nós que já fazem parte de um cluster NLB ou pode configurar primeiro uma implementação em expansão e, depois, instalar o software de cluster.  
  
## <a name="steps-for-report-server-deployment-on-an-nlb-cluster"></a>Etapas da implantação do servidor de relatório em um cluster NLB

 Use as seguintes diretrizes para instalar e configurar sua implantação:  
  
|Etapa|Descrição|Mais informações|  
|----------|-----------------|----------------------|  
|1|Antes de instalar o Reporting Services em nós de servidor em um cluster NLB, verifique os requisitos de implantação em expansão.|[Configurar uma implantação escalável do servidor de relatório em modo nativo](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)|  
|2|Configure o cluster NLB e verifique se ele está funcionando corretamente.<br /><br /> Mapeie um nome de cabeçalho de host para o IP de servidor virtual do cluster NLB. O nome de cabeçalho de host é usado na URL do servidor de relatório e é mais fácil de lembrar e digitar do que um endereço IP.|Para obter mais informações, consulte a documentação do produto do Windows Server para a versão do sistema operacional Windows que você executa.|  
|3|Adicionar o NetBIOS e um Nome de Domínio Totalmente Qualificado (FQDN) para o cabeçalho do host para a lista de **BackConnectionHostNames** armazenada no Registro do Windows.<br /><br /> Por exemplo, se o nome do cabeçalho de host \<MyServer> for um nome virtual para o nome do computador do Windows "contoso", provavelmente, você poderá referenciar o formato FQDN como "contoso.domain.com". Você precisará adicionar o nome do cabeçalho de host (MyServer) e nome FQDN (contoso.domain.com) à lista em **BackConnectionHostNames**.  <br /><br /> Em seguida, reinicie o computador para garantir que as alterações entrem em vigor.|Esta etapa é necessária se seu ambiente de servidor envolver autenticação de NTLM no computador local, criando uma conexão de loopback.<br /><br /> Se este for o caso, você verá que as solicitações entre o Gerenciador de Relatórios e Servidor de relatório falharão com 401 (Sem autorização).|  
|4|Instale o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo somente arquivos nos nós que já fazem parte de um cluster NLB e configure as instâncias do servidor de relatório para a implantação escalável.<br /><br /> A expansão configurada poderá não responder às solicitações dirigidas ao IP do servidor virtual. A configuração da expansão para usar o IP do servidor virtual ocorre em uma etapa posterior, depois que você configura a validação do estado de exibição.|[Configurar uma implantação de expansão do servidor de relatório no modo nativo &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)|  
|5|Configure a validação do estado de exibição.<br /><br /> Para obter os melhores resultados, execute esta etapa depois de configurar a implantação em expansão e antes de configurar as instâncias do servidor de relatório que usarão o IP do servidor virtual. Ao configurar primeiro a validação do estado de exibição, você evitará exceções sobre falha na validação do estado quando usuários tentarem acessar relatórios interativos.|[Como configurar a validação do estado de exibição](#ViewState) neste tópico.|  
|6|Configure o **Hostname** e o **UrlRoot** para usar o IP do servidor virtual do cluster NLB.|[Como configurar Hostname e UrlRoot](#SpecifyingVirtualServerName) neste tópico.|  
|7|Verifique se é possível acessar os servidores através do nome do host especificado.|[Verificar o acesso ao servidor de relatório](#Verify) neste tópico.|  
  
## <a name="how-to-configure-view-state-validation"></a><a name="ViewState"></a> Como configurar a validação do estado de exibição

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Para executar uma implantação em expansão em um cluster NLB, você deve configurar a validação do estado de exibição para que os usuários possam exibir relatórios HTML interativos.  Você precisa fazer isso para o serviço Web do servidor de relatório.
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Para executar uma implantação em expansão em um cluster NLB, você deve configurar a validação do estado de exibição para que os usuários possam exibir relatórios HTML interativos.
::: moniker-end
  
 A validação do estado de exibição é controlada pelo ASP .NET. Por padrão, ela fica habilitada e usa a identidade do serviço Web para efetuar a validação. Porém, em um cenário de cluster NLB, existem várias instâncias de serviço e identidades de serviço Web que são executadas em computadores diferentes. Como a identidade do serviço varia para cada nó, não é possível usar uma única identidade de processo para efetuar a validação.  
  
 Para contornar esse problema, você pode gerar uma chave de validação arbitrária para dar suporte à validação do estado de exibição e, depois, configurar manualmente cada nó do servidor de relatório para usar a mesma chave. É possível usar qualquer sequência hexadecimal gerada aleatoriamente. O algoritmo de validação (como SHA1) determina o comprimento da sequência hexadecimal.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

1. Gere uma chave de validação e uma chave de descriptografia usando a funcionalidade de geração automática fornecida pelo [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. No final, você precisa ter uma única entrada <`machineKey`> que possa ser colada no arquivo Web.config de cada instância do servidor de relatório na implantação escalável.  
  
    O exemplo a seguir mostra uma ilustração do valor a ser obtido. Não copie o exemplo nos seus arquivos de configuração; os valores de chave não são válidos.  
  
    ```xml
    <machineKey ValidationKey="123455555" DecryptionKey="678999999" Validation="SHA1" Decryption="AES"/>  
    ```  
  
2. Abra o arquivo Web.config do servidor de relatório e, na seção <`system.web`>, cole o elemento <`machineKey`> gerado por você. Por padrão, o arquivo Web.config do Gerenciador de Relatórios está localizado em \Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\Reportserver\Web.config.  
  
3. Salve o arquivo.  
  
4. Repita a etapa anterior para cada servidor de relatório na implantação em expansão.  
  
5. Verifique se todos os arquivos Web.config das pastas \Reporting Services\Reportserver contêm elementos <`machineKey`> idênticos na seção <`system.web`>.  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

1. Gere uma chave de validação e uma chave de descriptografia usando a funcionalidade de geração automática fornecida pelo [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. No final, você deve ter uma entrada \<**MachineKey**> que pode ser colada no arquivo RSReportServer.config de cada instância do servidor de relatório na implantação de expansão.

    O exemplo a seguir mostra uma ilustração do valor a ser obtido. Não copie o exemplo nos seus arquivos de configuração; os valores de chave não são válidos. O servidor de relatório requer o uso de maiúsculas e minúsculas correto.

    ```xml
    <MachineKey ValidationKey="123455555" DecryptionKey="678999999" Validation="SHA1" Decryption="AES"/>
    ```

2. Salve o arquivo.

3. Repita a etapa anterior para cada servidor de relatório na implantação em expansão.  

4. Verifique se todos os arquivos RSReportServer.config das pastas \Reporting Services\Servidor de Relatório contêm elementos \<**MachineKey**> idênticos.

::: moniker-end

## <a name="how-to-configure-hostname-and-urlroot"></a><a name="SpecifyingVirtualServerName"></a> Como configurar Hostname e UrlRoot

 Para configurar uma implantação em expansão do servidor de relatório em um cluster NLB, é necessário definir um único nome de servidor virtual que forneça um único ponto de acesso ao cluster de servidores. Então registre esse nome de servidor virtual com o DNS (Domain Name Server, servidor de nomes de domínio) em seu ambiente.  
  
 Depois de definir o nome do servidor virtual, você poderá configurar as propriedades **Hostname** e as **UrlRoot** no arquivo RSReportServer.config para incluir o nome do servidor virtual na URL do servidor de relatório.  
  
 Configure a propriedade **Hostname** quando você estiver usando reservas curinga de URL em seu ambiente de relatório. Quando você especifica a propriedade **Hostname** para ser o nome do servidor virtual do servidor NLB, o tráfego de rede para o ambiente de relatório é direcionado ao servidor NLB. O NLB, em seguida, distribui solicitações entre os nós de servidor de relatório.  
  
 Além disso, configure a propriedade **UrlRoot** de forma que os links de relatório funcionem nos relatórios que foram exportados para relatórios estáticos, como no formato Excel ou PDF, ou em relatórios que são gerados por assinaturas, como as assinaturas de email.  
  
 Se você integrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com o [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 ou [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007, ou hospedar relatórios em um aplicativo Web personalizado, poderá ser necessário configurar somente a propriedade **UrlRoot** . Nesse caso, configure a propriedade **UrlRoot** para ser a URL do site do SharePoint ou do aplicativo Web. Isso direcionará o tráfego de rede para o ambiente de relatório para o aplicativo que trata dos relatórios e não para o servidor de relatório ou cluster NLB.  
  
 Não modifique **ReportServerUrl**. Se você modificar essa URL, introduzirá uma viagem de ida e volta a mais no servidor virtual sempre que uma solicitação interna for tratada. Para obter mais informações, consulte [URLs em arquivos de configuração &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md). Para obter mais informações sobre como editar o arquivo de configuração, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
1. Abra o RSReportServer.config em um editor de texto.  
  
2. Localize a seção **\<Service>** e adicione as seguintes informações ao arquivo de configuração, substituindo o valor **Hostname** pelo nome do servidor virtual do servidor NLB:  
  
    ```xml
    <Hostname>virtual_server</Hostname>  
    ```  
  
3. Localize **UrlRoot**. O elemento não é especificado no arquivo de configuração, mas o valor padrão usado é uma URL neste formato: https:// ou `https://<computername>/<reportserver>`, em que \<*reportserver*> corresponde ao nome do diretório virtual do serviço Web do Servidor de Relatório.  
  
4. Digite um valor para **UrlRoot** que inclui o nome virtual do cluster neste formato: https:// ou `https://<virtual_server>/<reportserver>`.  
  
5. Salve o arquivo.  
  
6. Repita estas etapas em cada arquivo RSReportServer.config de cada servidor de relatório na implantação em expansão.  
  
## <a name="verify-report-server-access"></a><a name="Verify"></a> Verificar o acesso ao servidor de relatório

 Verifique se você pode acessar a implantação escalável por meio do nome do servidor virtual (por exemplo, `https://MyVirtualServerName/reportserver` e `https://MyVirtualServerName/reports`).  
  
 Você pode verificar que nó efetivamente processa relatórios examinando os arquivos de log do servidor de relatório ou verificando o log de execução do RS (a tabela do log de execução contém uma coluna denominada **InstanceName** que mostra qual instância processou uma determinada solicitação). Para obter mais informações, confira [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
 Se não for possível se conectar ao servidor de relatório, verifique o NLB para assegurar que as solicitações sejam enviadas para o servidor de relatório e visualize o log do HTTP do servidor de relatório para assegurar que o servidor esteja recebendo as solicitações.  
  
### <a name="troubleshooting-failed-requests"></a>Solucionando problemas de solicitações falhas

 Se as solicitações não chegarem até as instâncias do servidor de relatório, verifique no arquivo RSReportServer.config se o nome do servidor virtual está especificado como o nome do host para as URLs do servidor de relatório:  
  
1. Abra o arquivo RSReportServer.config em um editor de texto.  
  
2. Localize \<**Hostname**>, \<**ReportServerUrl**> e \<**UrlRoot**> e verifique o nome do host para cada configuração. Se o valor não for o nome de host esperado, substitua-o pelo nome de host correto.  
  
 Se você iniciar a ferramenta Configuração do Reporting Services depois de fazer essas alterações, a ferramenta poderá alterar as configurações de \<**ReportServerUrl**> com o valor padrão. Sempre tenha uma cópia de backup dos arquivos de configuração caso seja necessário substituí-los pela versão que contém as configurações desejadas.  
  
## <a name="see-also"></a>Consulte Também

 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Configurar uma implantação escalável do servidor de relatório no modo nativo &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [Gerenciar um servidor de relatórios de Modo Nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)
