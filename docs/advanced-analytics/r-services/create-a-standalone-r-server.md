---
title: "Criar um R Server Aut&#244;nomo | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# Criar um R Server Aut&#244;nomo
  A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui a opção de instalar o **Microsoft R Server (Autônomo)**. Essa opção permite desenvolver soluções do R de alto desempenho no Windows durante a conexão com o banco de dados ou a fonte de dados de sua escolha. O Microsoft R Server está disponível apenas no Enterprise Edition  
  
 Ao instalar o Microsoft R Server, você obtém os mesmos pacotes avançados do R e ferramentas de conectividade fornecidos no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], mas uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é necessária e a execução de scripts do R é executada no computador autônomo, e não no banco de dados.  
  
> [!NOTE]  
>  Agora o Microsoft R Server também está disponível por meio de uma configuração simplificada que registra a instância na política [Ciclo de Vida Moderno](https://support.microsoft.com/help/447912). Essa oferta de suporte garante que você sempre está usando a versão mais atual do R. Para obter mais informações sobre como usar a configuração simplificada, consulte [Executar o Microsoft R Server para Windows](https://msdnstage.redmond.corp.microsoft.com/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev).
>  
> Se você instalar o Microsoft R Server por meio da instalação simplificada, também poderá converter qualquer instância especificada do R Services para usar a nova política de suporte e obter atualizações mais frequentes dos componentes do R. Para obter mais informações, consulte [Usar sqlBindR.exe para atualizar uma instância do R Services](http://www.bing.com).   
  
##  <a name="a-namebkmkinstallrservicesindatabasea-install-microsoft-r-server-standalone"></a><a name="bkmk_installRServicesInDatabase"></a> Instalar o Microsoft R Server (Autônomo)  
  
1.  Se você tiver instalado uma versão anterior do Microsoft R Server, deverá desinstalá-la primeiro.  Consulte [Atualizando de uma versão anterior do Microsoft R Server](#bkmk_Uninstall). 

2. Execute a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Na guia **Instalação** , clique na instalação **Novo R Server (Autônomo)** .  
  
     ![Setup option for R Server Standalone](../../advanced-analytics/r-services/media/rsql-rstandalonesetup.png "Setup option for R Server Standalone")  
  
3.  Na página **Seleção de recurso** , a seguinte opção já deve estar selecionada:  
  
    -   **R Server (Autônomo)**  
  
         Esta opção instala os recursos compartilhados, incluindo ferramentas do R de software livre, pacotes de base, pacotes avançados do R e ferramentas de conectividade fornecidas pelo Microsoft R.  
  
     Todas as outras opções devem ser ignoradas.  
  
4.  Aceite os termos de licença para baixar e instalar o Microsoft R Open. Quando o botão **Aceitar** não estiver mais disponível, clique em **Avançar**. A instalação desses componentes (e todos os pré-requisitos que possam exigir) pode levar algum tempo.   
  
5.  Na página **Pronto para Instalar**, verifique suas seleções e clique em **Instalar**.  
  
> [!TIP]
> Para obter mais informações sobre a instalação automatizada ou offline, consulte [Instalar o Microsoft R Server por meio da linha de comando](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md).

  
## <a name="what-is-installed-and-where-to-find-r-packages"></a>O que é instalado e em que local encontrar os pacotes do R  
 O Microsoft R Server inclui pacotes de base do R e um conjunto de pacotes avançados do R que dão suporte ao processamento paralelo, a um melhor desempenho e à conectividade com fontes de dados, incluindo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Hadoop.  
  
-   **Pacotes do R**  
  
     As bibliotecas do R são instaladas junto com outras ferramentas e utilitários que são instalados com o Microsoft SQL Server 2016. Por exemplo:  
  
     `C:\Program Files\Microsoft SQL Server\130\R_SERVER`  
  
     Além disso, nessa pasta, você encontrará a documentação dos pacotes de base do R, dados de exemplo e a documentação das ferramentas e do tempo de execução do R.  
  
    > [!NOTE]  
    >  Se você tiver instalado uma instância do SQL Server com R Services (no Banco de Dados) no mesmo computador, as ferramentas e bibliotecas do R serão instaladas em outra pasta: `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`  
    >   
    >  Não use pacotes nem utilitários do R associados à instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Sempre use as ferramentas e os pacotes do R localizados na pasta R_SERVER.  
  
-   **Ferramentas do R**  
  
     Uma IDE de desenvolvimento do R não é instalada como parte da instalação. É possível instalar o RStudio, [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] ou qualquer outro ambiente de desenvolvimento desejado.  
  
     No entanto, não são necessárias ferramentas adicionais. Todas as ferramentas de base padrão do R estão incluídas no `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin`.  
  
     Para obter mais informações, consulte [Instalar ou configurar as ferramentas do R](../../advanced-analytics/r-services/setup-or-configure-r-tools.md).  


 
## <a name="troubleshooting"></a>Solução de problemas  

### <a name="incompatible-version-of-r-client-and-r-server"></a>Versão incompatível do Cliente do R e R Server

Se você instalar a última versão do Cliente do Microsoft R e usá-la para executar o R no SQL Server usando um contexto de computação remota, poderá receber o seguinte erro:

*Você está executando a versão 9.0.0 do cliente do Microsoft R em seu computador, que é incompatível com o Microsoft R Server versão 8.0.3. Baixe e instale uma versão compatível.*

Normalmente, a versão do R instalada com o SQL Server R Services é atualizada quando as versões de serviço são publicadas. Para garantir que você sempre tem as versões mais atualizadas dos componentes do R, instale todos os service packs. Para compatibilidade com o Cliente do Microsoft R 9.0.0, é necessário instalar as atualizações descritas neste [artigo de suporte](https://support.microsoft.com/kb/3210262). 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Instalando o Microsoft R Server em uma instância do SQL Server instalada no Windows Core
Na versão de lançamento do SQL Server 2016, houve um problema conhecido ao adicionar o Microsoft R Server a uma instância no Windows Server Core Edition. Esse problema foi corrigido. 

Se você tiver esse problema, aplique a correção descrita no [KB3164398](https://support.microsoft.com/kb/3164398) para adicionar o recurso do R à instância existente no Windows Server Core.   Para obter mais informações, consulte [Não é possível instalar o Microsoft R Server (Autônomo) em um sistema operacional Windows Server Core](https://support.microsoft.com/kb/3168691).


###  <a name="a-namebkmkuninstalla-upgrading-from-an-older-version-of-microsoft-r-server"></a><a name="bkmk_Uninstall"></a> Atualizando de uma versão anterior do Microsoft R Server  
 Se você tiver instalado uma versão de pré-lançamento do Microsoft R Server, será necessário desinstalá-la antes de atualizar para uma versão mais nova.  
  
**Para desinstalar o R Server (Autônomo)**  
  
1.  No **Painel de Controle**, clique em **Adicionar/Remover Programas** e selecione `Microsoft SQL Server 2016 <version number>`.  
  
2.  Na caixa de diálogo com opções para **Adicionar**, **Reparar** ou **Remover** componentes, selecione **Remover**.  
  
3.  Na página **Selecionar Recursos** em **Recursos Compartilhados**, selecione **R Server (Autônomo)**. Clique em **Avançar** e em **Concluir** para desinstalar apenas os componentes selecionados.  
   
### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>A instalação falha com o erro “Apenas um único produto do Revolution Enterprise pode ser instalado por vez”.  
Você poderá receber esse erro se tiver uma instalação mais antiga dos produtos da Revolution Analytics ou uma versão de pré-lançamento do SQL Server R Services. É necessário desinstalar todas as versões anteriores antes de instalar uma versão mais nova do Microsoft R Server. Não há suporte para a instalação lado a lado com outras versões das ferramentas do Revolution Enterprise.  

No entanto, há suporte para instalações lado a lado ao usar um R Server Autônomo com o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e o 
  
### <a name="unable-to-uninstall-older-components"></a>Não é possível desinstalar os componentes mais antigos   
  
Se você tiver problemas ao remover uma versão mais antiga, talvez será necessário editar o Registro para remover as chaves relacionadas.  

> [!IMPORTANT]
> Esse problema se aplicará somente se você tiver instalado uma versão de pré-lançamento do Microsoft R Server ou uma versão CTP do SQL Server 2016 R Services.
  
1. Abra o Registro do Windows e localize esta chave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.  
2. Exclua as seguintes entradas, se houver, e se a chave contiver apenas o valor `sEstimatedSize2`:  
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (para o 8.0.2)  
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (para o 8.0.1)  
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (para o 8.0.0)  
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (para o 7.5.0)  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)  
  
  