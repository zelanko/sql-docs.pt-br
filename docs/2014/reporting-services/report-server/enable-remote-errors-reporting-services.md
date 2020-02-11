---
title: Habilitar erros remotos (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- remote data source [Reporting Services]
- EnableRemoteError server property
ms.assetid: 5f05022b-d557-43e0-b50a-f5e2a1846b83
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e2d239dfc3d094f72d40ce6d020610fe1c0eabbc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103805"
---
# <a name="enable-remote-errors-reporting-services"></a>Habilitar erros remotos (Reporting Services)
  É possível configurar propriedades do servidor de relatório em um [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para retornar informações adicionais sobre as condições de erro que ocorrem em servidores remotos. Se uma mensagem de erro contiver o texto "Para obter mais informações sobre este erro, navegue até o servidor de relatório na máquina de servidor local ou habilite erros remotos", você poderá configurar a propriedade `EnableRemoteErrors` para acessar informações adicionais que podem ajudá-lo a resolver o problema. Para obter mais informações, consulte [Propriedades de sistema do servidor de relatório](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Neste tópico:**  
  
-   [Habilitar erros remotos para o modo do SharePoint](#bkmk_sharepoint)  
  
-   [Habilitar erros remotos por meio de SQL Server Management Studio (modo nativo)](#bkmk_mgtStudio)  
  
-   [Habilitar erros remotos por meio de script (modo nativo)](#bkmk_script)  
  
-   [Modificando a tabela ConfigurationInfo (modo nativo)](#bkmk_ConfigurationInfo)  
  
##  <a name="bkmk_sharepoint"></a>Habilitar erros remotos para o modo do SharePoint  
 Há dois procedimentos diferentes para habilitar erros remotos para o modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O procedimento é diferente para as duas arquiteturas de servidor de relatório distintas. A mais nova arquitetura baseada no serviço do SharePoint, que foi apresentada na versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , utiliza uma configuração que pode ser definida para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A arquitetura mais antiga utiliza uma única configuração em nível de site.  
  
#### <a name="enable-remote-errors-for-a-reporting-services-service-application"></a>Habilitar erros remotos para um aplicativo de serviço do Reporting Services  
  
1.  Para um servidor de relatório de modo do SharePoint instalado com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou uma versão mais nova do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], habilite a configuração de aplicativo de serviço **Habilitar erros remotos**. A configuração pode ser definida para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Na administração central do SharePoint, clique em **gerenciar aplicativos de serviço** no grupo **Gerenciamento de aplicativos** .  
  
3.  Localize seu aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique no nome do aplicativo de serviço.  
  
4.  Clique em **Configurações do Sistema**.  
  
5.  Clique em **Habilitar Erros Remotos** , na seção **Segurança** .  
  
6.  Clique em **OK**.  
  
#### <a name="enable-remote-errors-for-a-sharepoint-site"></a>Habilitar erros remotos para um site do SharePoint  
  
1.  Para um servidor de relatório de modo do SharePoint instalado com uma versão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anterior ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], habilite a configuração de site **Habilitar erros remotos no modo local**.  
  
2.  Em **Site Ações** , clique em **Configurações de Site** para o site a ser modificado.  
  
3.  Clique em **Configurações do Reporting Services** , no grupo **Reporting Services** .  
  
4.  Clique em **Habilitar erros remotos em modo local**.  
  
5.  Clique em **OK**  
  
##  <a name="bkmk_mgtStudio"></a>Habilitar erros remotos por meio de SQL Server Management Studio (modo nativo)  
  
1.  Inicie o Management Studio e conecte-se a uma instância de servidor de relatório. Para obter mais informações, consulte [Conectar-se a um servidor de relatório no Management Studio](../tools/connect-to-a-report-server-in-management-studio.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Clique com o botão direito do mouse no nó do servidor de relatório e selecione **Propriedades**.  
  
3.  Clique em **Avançado** para abrir a página de propriedades. Para obter mais informações, consulte [Propriedades do Servidor &#40;página Avançado&#41; – Reporting Services](../tools/server-properties-advanced-page-reporting-services.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Em `EnableRemoteErrors`, selecione `True`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_script"></a>Habilitar erros remotos por meio de script (modo nativo)  
  
1.  Crie um arquivo de texto e copie o seguinte script no arquivo.  
  
    ```  
    Public Sub Main()  
      Dim P As New [Property]()  
      P.Name = "EnableRemoteErrors"  
      P.Value = True  
      Dim Properties(0) As [Property]  
      Properties(0) = P  
      Try  
        rs.SetSystemProperties(Properties)  
        Console.WriteLine("Remote errors enabled.")  
      Catch SE As SoapException  
        Console.WriteLine(SE.Detail.OuterXml)  
      End Try  
    End Sub  
    ```  
  
2.  Salve o arquivo como EnableRemoteErrors.rss.  
  
3.  Clique em **Iniciar**, aponte para **Executar**, digite **cmd**e clique em **OK** para abrir uma janela do prompt de comando.  
  
4.  Navegue até o diretório que contém o arquivo .rss recém-criado.  
  
5.  Digite a seguinte linha de comando, substituindo *servername* pelo nome atual de seu servidor:  
  
    ```  
    rs -i EnableRemoteErrors.rss -s http://servername/ReportServer  
    ```  
  
6.  Para obter mais informações, consulte [utilitário RS. exe &#40;SSRS&#41;](../tools/rs-exe-utility-ssrs.md)  
  
##  <a name="bkmk_ConfigurationInfo"></a>Modificando a tabela ConfigurationInfo (modo nativo)  
  
1.  > [!NOTE]  
    >  Você pode editar a tabela **ConfigurationInfo** no banco de dados do servidor de `EnableRemoteErrors` relatório `True`para definir como, mas se o servidor de relatório for usado ativamente, você deverá usar SQL Server Management Studio ou script para modificar as configurações. Se você modificar a configuração no banco de dados, precisará reiniciar o serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] antes de as alterações entrarem em vigor.  
  
  
