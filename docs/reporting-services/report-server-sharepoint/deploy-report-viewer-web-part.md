---
title: "Implantar a web part do Visualizador de Relatórios do SQL Server Reporting Services em um site do SharePoint | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 32a2cc64cb54fda7244a07ad8aff8463899f0b3d
ms.sourcegitcommit: 4286dddf27dcdf1c8ef3ef134474e72559c2f65c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2017
---
# <a name="deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-site"></a>Implantar a web part do Visualizador de Relatórios do SQL Server Reporting Services em um site do SharePoint

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

A web part do Visualizador de Relatórios é uma web part personalizada que pode ser usada para exibir relatórios do SQL Server Reporting Services (modo nativo) no site do SharePoint. Você pode usar a web part para exibir, navegar, imprimir e exportar relatórios em um servidor de relatório. A web part do Visualizador de Relatórios está associada a arquivos de definição de relatório (.rdl) que são processados por um servidor de relatório do SQL Server Reporting Services ou um Servidor de Relatórios do Power BI. Essa web part do Visualizador de Relatórios não pode ser usada com relatórios do Power BI hospedados no Servidor de Relatórios do Power BI.

Use as instruções a seguir para implantar manualmente o pacote de solução que adiciona a web part do Visualizador de Relatórios a um ambiente do SharePoint Server 2013 ou SharePoint Server 2016. A implantação da solução é uma etapa necessária para configurar a web part.

**A web part do Visualizador de Relatórios é um pacote de solução autônoma e não está associada ao modo integrado do SharePoint para SQL Server Reporting Services.**

## <a name="requirements"></a>Requisitos

**Dar suporte a versões do SharePoint Server:**  
* SharePoint Server 2016
* SharePoint Server 2013

**Dar suporte a versões do Reporting Services:**  
* SQL Server 2008 Reporting Services (modo nativo) e posterior.
* Servidor de Relatório do Power BI

## <a name="download-the-report-viewer-web-part-solution-package"></a>Baixar o pacote de solução da web part do Visualizador de Relatórios

A web part do Visualizador de Relatórios está disponível no Centro de Download da Microsoft.

[Baixar o pacote de solução da web part do Visualizador de Relatórios](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>Implantar a solução de farm

Esta seção mostra como implantar o pacote de solução no farm do SharePoint. Essa tarefa só precisa ser realizada uma vez.

1. Em um servidor do SharePoint, abra um Shell de Gerenciamento do SharePoint usando a opção **Executar como Administrador**.

2. Execute [Add-SPSolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx) para adicionar a solução de farm.

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.

3. Execute o cmdlet [Install-SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) para implantar a solução de farm.

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>Ativar recurso

1. No site do SharePoint, selecione o ícone de **engrenagem** no canto superior esquerdo e selecione **Configurações de Site**.

    ![Configurações de site no ícone de engrenagem.](media/sharepoint-site-settings.png)

    Por padrão, os aplicativos Web do SharePoint são acessados pela porta 80. Isso significa que você pode acessar frequentemente um site do SharePoint inserindo *http://<computer name>* para abrir o conjunto de sites raiz.

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

    Por padrão, os aplicativos Web do SharePoint são acessados pela porta 80. Isso significa que você pode acessar frequentemente um site do SharePoint inserindo *http://<computer name>* para abrir o conjunto de sites raiz.

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

## <a name="next-steps"></a>Próximas etapas

Após a implantação e ativação da web part do Visualizador de Relatórios, adicione a web part a uma página do SharePoint. Para obter mais informações, consulte [Adicionar uma web part do Visualizador de Relatórios a uma página do SharePoint](add-report-viewer-web-part-to-page.md).

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
