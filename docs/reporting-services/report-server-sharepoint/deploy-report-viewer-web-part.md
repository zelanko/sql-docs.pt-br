---
title: "Implantar a web part do Visualizador de relatórios do SQL Server Reporting Services em um site do SharePoint | Microsoft Docs"
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a75ad193204e17e1d053aa4e00adba5f551d684b
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---

# <a name="deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-site"></a>Implantar a web part do Visualizador de relatórios do SQL Server Reporting Services em um site do SharePoint

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

A web part do Visualizador de relatórios é uma parte da web personalizado que pode ser usada para exibir relatórios do SQL Server Reporting Services (modo nativo) dentro de seu site do SharePoint. Você pode usar a web part para exibir, navegar, imprimir e exportar relatórios em um servidor de relatório. A web part do Visualizador de relatórios está associada a arquivos de definição (. RDL) de relatório que são processados por um servidor de relatório do SQL Server Reporting Services ou um servidor de relatório do Power BI. Esta web part do Visualizador de relatórios não pode ser usado com relatórios do Power BI hospedados no servidor de relatório do Power BI.

Use as instruções a seguir para implantar manualmente o pacote de solução que adiciona a web part do Visualizador de relatórios para um ambiente do SharePoint Server 2013 ou SharePoint Server 2016. Implantar a solução é uma etapa necessária para configurar a web part.

**A web part do Visualizador de relatórios é um pacote de solução autônoma e não está associada com o modo integrado do SharePoint para SQL Server Reporting Services.**

## <a name="requirements"></a>Requisitos

**Suporte a versões de servidor do SharePoint:**  
* SharePoint Server 2016
* SharePoint Server 2013

**Suporte a versões do Reporting Services:**  
* SQL Server 2008 Reporting Services (modo nativo) e posterior.
* Servidor de Relatório do Power BI

## <a name="download-the-report-viewer-web-part-solution-package"></a>Baixe o pacote de solução do Visualizador de relatórios da web part

A web part do Visualizador de relatórios está disponível no Microsoft Download Center.

[Baixe o pacote de solução web part Visualizador de relatórios](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="deploy-the-farm-solution"></a>Implantar a solução de farm

Esta seção mostra como implantar o pacote de solução em seu farm do SharePoint. Essa tarefa só precisa ser realizada uma vez.

1. Em um servidor do SharePoint, abra um Shell de gerenciamento do SharePoint usando o **executar como administrador** opção.

2. Executar [Add-SPSolution](https://technet.microsoft.com/library/ff607552(v=office.16).aspx) para adicionar a solução de farm.

    ```
    Add-SPSolution –LiteralPath "{path to file}\ReportViewerWebPart.wsp"
    ```

    O cmdlet retorna o nome da solução, sua ID de solução e Deployed=False. Na próxima etapa, você implantará a solução.

3. Execute o [Install-SPSolution](https://technet.microsoft.com/library/ff607534(v=office.16).aspx) cmdlet para implantar a solução de farm.

    **SharePoint 2013**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -CompatibilityLevel "14,15" -GACDeployment -WebApplication {URL to web application}
    ```

    **SharePoint 2016**

    ```
    Install-SPSolution –Identity ReportViewerWebPart.wsp -GACDeployment -WebApplication {URL to web application}
    ```

## <a name="activate-feature"></a>Ativar recurso

1. No site do SharePoint, selecione o **engrenagem** ícone no canto superior esquerdo e selecione **configurações do Site*.

    ![Configurações de site do ícone de engrenagem.](media/sharepoint-site-settings.png)

    Por padrão, os aplicativos Web do SharePoint são acessados pela porta 80. Isso significa que você geralmente pode acessar um site do SharePoint digitando *http://<computer name>*  para abrir o conjunto de sites raiz.

3. Em **administração do conjunto de sites**, selecione **recursos de coleção de sites**.

4. Role a página até encontrar o **web part do Visualizador de relatórios** recurso.

5. Selecione **Ativar**.

    ![Ativar o recurso de web part do Visualizador de relatórios](media/web-part-activiate-feature.png)

6. Repita para outros conjuntos de sites, abrindo cada site e clicando em ações do Site.

Opcionalmente, você também pode usar do PowerShell para habilitar esse recurso em todos os sites usando o [Enable-SPFeature](https://technet.microsoft.com/library/ff607803.aspx) cmdlet.

```
Get-SPWebApplication "<web application url>" | Get-SPSite -Limit ALL | 
        ForEach-Object {
            Write-Host "Enabling feature for $($_.URL)"
            Enable-SPFeature -identity "ReportViewerWebPart" -URL $_.URL -ErrorAction Continue
        }
```

## <a name="remove-the-solution"></a>Remover a solução

Embora a Administração Central do SharePoint fornece retração da solução, você não precisa cancelar o **ReportViewerWebPart.wsp** , a menos que você esteja Solucionando problemas sistematicamente um problema de implantação de instalação ou o patch de arquivo.

1. Na Administração Central do SharePoint, em **configurações do sistema**, selecione **gerenciar soluções de farm**.

2. Selecione **ReportViewerWebPart.wsp**.

3. Selecione Cancelar a solução.

### <a name="remove-the-web-part-from-site-settings"></a>Remova a web part de configurações do Site

Cancelamento da solução não remove a web part do Visualizador de relatórios na lista de web parts dentro de seu site do SharePoint. Para remover a web part do Visualizador de relatórios, faça o seguinte:

1. No site do SharePoint, selecione o **engrenagem** ícone no canto superior esquerdo e selecione **configurações do Site*.

    ![Configurações de site do ícone de engrenagem.](media/sharepoint-site-settings.png)

    Por padrão, os aplicativos Web do SharePoint são acessados pela porta 80. Isso significa que você geralmente pode acessar um site do SharePoint digitando *http://<computer name>*  para abrir o conjunto de sites raiz.

2. Em **Web Designer galerias**, selecione **web parts**.

3. Selecione o **ícone Editar** lado **ReportViewerNativeMode.dwp**. Não podem ser listado na primeira página de resultados.

4. Selecione **Excluir Item**.

    ![Editar e excluir a web part do modo nativo do Visualizador de relatórios](media/report-viewer-native-mode-edit-delete.png)

Tentativa de exclusão da web part usando o PowerShell, mas não é um comando direto para ele. Para obter um exemplo de script, consulte [como excluir web parts da Galeria de web parts](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f).

## <a name="supported-languages"></a>Idiomas com suporte

Os idiomas a seguir têm suporte com a web part:

* Inglês (en)
* Alemão (de)
* Espanhol (sp)
* Francês (fr)
* Italiano ()
* Japonês (ja)
* Coreano (ko)
* Português (Portugal)
* Russo (ru)
* Chinês (simplificado - zh-HANS e zh-CHS)
* Chinês (tradicional - zh-HANT e zh-CHT)

## <a name="next-steps"></a>Próximas etapas

Após a implantação da web part do Visualizador de relatórios e para ativar, você pode adicionar a web part a uma página do SharePoint. Para obter mais informações, consulte [web part do Visualizador de relatórios de adicionar a uma página do SharePoint](add-report-viewer-web-part-to-page.md).

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
