---
title: Implantar a web part do Visualizador de Relatórios do SQL Server Reporting Services em um site do SharePoint | Microsoft Docs
description: Para o SQL Server Reporting Services, você pode adicionar manualmente a web part personalizada do Visualizador de Relatórios para um produto do SharePoint.
ms.date: 11/15/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 49ac20b46c5453c431cb856ad060512b48315262
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83767017"
---
# <a name="deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-site"></a>Implantar a web part do Visualizador de Relatórios do SQL Server Reporting Services em um site do SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]  [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-and-later](../../includes/ssrs-appliesto-sharepoint-2013-and-later.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

A web part do Visualizador de Relatórios é uma web part personalizada que pode ser usada para exibir relatórios do SQL Server Reporting Services (modo nativo) no site do SharePoint. Você pode usar a web part para exibir, navegar, imprimir e exportar relatórios em um servidor de relatório. A web part do Visualizador de Relatórios está associada a arquivos de definição de relatório (.rdl) que são processados por um servidor de relatório do SQL Server Reporting Services ou um Servidor de Relatórios do Power BI. Essa web part do Visualizador de Relatórios não pode ser usada com relatórios do Power BI hospedados no Servidor de Relatórios do Power BI.

Use as instruções a seguir para implantar manualmente o pacote de solução que adiciona a Web part do Visualizador de Relatórios a um ambiente do SharePoint Server 2013, SharePoint Server 2016 ou SharePoint Server 2019. A implantação da solução é uma etapa necessária para configurar a web part.

**A web part do Visualizador de Relatórios é um pacote de solução autônoma e não está associada ao modo integrado do SharePoint para SQL Server Reporting Services.**

## <a name="requirements"></a>Requisitos

> [!IMPORTANT]
> Da versão "15.X.X.X" em diante, você pode instalar o ReportViewerWebPart lado a lado com os aplicativos de serviço compartilhado do modo integrado do SharePoint do Reporting Services.
> Com essa atualização da solução .wsp, apresentamos novos arquivos. A solução anterior precisa ser retirada e o novo .wsp reimplantado usando os cmdlets Uninstall-SPSolution e Install-SPSolution, respectivamente.
>

**Dar suporte a versões do SharePoint Server:**
* SharePoint Server 2019
* SharePoint Server 2016
* SharePoint Server 2013

**Dar suporte a versões do Reporting Services:**  
* SQL Server 2008 Reporting Services (modo nativo) e posterior.
* Servidor de Relatórios do Power BI

## <a name="download-the-report-viewer-web-part-solution-package"></a>Baixar o pacote de solução da web part do Visualizador de Relatórios

A web part do Visualizador de Relatórios está disponível no Centro de Download da Microsoft.

[Baixar o pacote de solução da web part do Visualizador de Relatórios](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>Implantar a solução de farm

Esta seção mostra como implantar o pacote de solução no farm do SharePoint. Essa tarefa só precisa ser realizada uma vez.

1. Em um servidor do SharePoint, abra um Shell de Gerenciamento do SharePoint usando a opção **Executar como Administrador**.

2. Execute [Add-SPSolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx) para adicionar a solução de farm.

    ```
    Add-SPSolution -LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.

3. Execute o cmdlet [Install-SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) para implantar a solução de farm.

    **SharePoint 2013**

    ```
    Install-SPSolution -Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint Server 2016 e 2019**

    ```
    Install-SPSolution -Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>Ativar recurso

1. No site do SharePoint, selecione o ícone de **engrenagem** no canto superior esquerdo e selecione **Configurações de Site**.

    ![Configurações de site no ícone de engrenagem.](media/sharepoint-site-settings.png)

    Por padrão, os aplicativos Web do SharePoint são acessados pela porta 80. Isso significa que você pode acessar frequentemente um site do SharePoint inserindo *https://<computer name>* para abrir o conjunto de sites raiz.

3. Em **Administração do Conjunto de Sites**, selecione **Recursos do conjunto de sites**.

4. Role a página até encontrar o Recurso **Web part do Visualizador de Relatórios**.

5. Selecione **Ativar**.

    ![Ativar o recurso web part do Visualizador de Relatórios](media/web-part-activiate-feature.png)

6. Repita a operação em outros conjuntos de sites, abrindo cada site e clicando em Ações do Site.

Opcionalmente, também use o PowerShell para habilitar esse recurso em todos os sites usando o cmdlet [Enable-SPFeature](https://technet.microsoft.com/library/ff607803.aspx).

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>Remover a solução

Embora a Administração Central do SharePoint forneça o cancelamento da solução, você não precisa cancelar o arquivo **ReportViewerWebPart.wsp**, a menos que esteja solucionando problemas sistematicamente de uma instalação ou um problema de implantação do patch.

1. Na Administração Central do SharePoint, em **Configurações do Sistema**, selecione **Gerenciar soluções de farm**.

2. Selecione **ReportViewerWebPart.wsp**.

3. Selecione Cancelar Solução.

### <a name="remove-the-web-part-from-site-settings"></a>Remover a web part das Configurações de site

O cancelamento da solução não remove a web part do Visualizador de Relatórios da lista de web parts no site do SharePoint. Para remover a web part do Visualizador de Relatórios, realize o procedimento a seguir.

1. No site do SharePoint, selecione o ícone de **engrenagem** no canto superior esquerdo e selecione **Configurações de Site**.

    ![Configurações de site no ícone de engrenagem.](media/sharepoint-site-settings.png)

    Por padrão, os aplicativos Web do SharePoint são acessados pela porta 80. Isso significa que você pode acessar frequentemente um site do SharePoint inserindo *https://<computer name>* para abrir o conjunto de sites raiz.

2. Em **Galerias de Web Designer**, selecione **web parts**.

3. Selecione o **ícone Editar** ao lado de **ReportViewerNativeMode.dwp**. Talvez ele não esteja listado na primeira página de resultados.

4. Selecione **Excluir Item**.

    ![Editar e excluir a web part do modo nativo do Visualizador de Relatórios](media/report-viewer-native-mode-edit-delete.png)

A tentativa de exclusão da web part pode ser feita usando o PowerShell, mas não há um comando direto para isso. Para obter um exemplo de script, consulte [Como excluir web parts da Galeria de web parts](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f).

## <a name="supported-languages"></a>Idiomas com suporte

Há suporte para os seguintes idiomas com a web part:

* Inglês (en)
* Alemão (de)
* Espanhol (sp)
* Francês (fr)
* Italiano (it)
* Japonês (ja)
* Coreano (ko)
* Português (pt)
* Russo (ru)
* Chinês (simplificado – zh-HANS e zh-CHS)
* Chinês (tradicional – zh-HANT e zh-CHT)

## <a name="troubleshoot"></a>Solucionar problemas

* Erro ao desinstalar o SSRS se você configurou o modo integrado do SharePoint:

    Install-SPRSService : [A] Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService não pode ser convertido em [B]Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService. O Tipo A é proveniente de 'Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' no contexto 'Default' e no local 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll'. O Tipo B é proveniente de 'Microsoft.ReportingServices.SharePoint.SharedService,Version=12.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' no contexto 'Default' e no local 'C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll'.
    
    Solução:
    1. Remover a web part do Visualizador de Relatórios
    2. Desinstalar o SSRS
    3. Reinstalar a web part do Visualizador de Relatórios

* Erro ao tentar atualizar o SharePoint se você configurou o modo integrado do SharePoint:

    Não foi possível carregar o arquivo ou o assembly 'Microsoft.ReportingServices.Alerting.ServiceContract, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' ou uma de suas dependências. O sistema não pode encontrar o arquivo especificado. 00000000-0000-0000-0000-000000000000
    
    Solução:
    1. Remover a web part do Visualizador de Relatórios
    2. Desinstalar o SSRS
    3. Reinstalar a web part do Visualizador de Relatórios

## <a name="next-steps"></a>Próximas etapas

Depois que a Web Part do Visualizador de Relatórios tiver sido implantada e ativada, será possível adicioná-la a uma página do SharePoint. Para obter mais informações, consulte [Adicionar uma web part do Visualizador de Relatórios a uma página do SharePoint](add-report-viewer-web-part-to-page.md).

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
