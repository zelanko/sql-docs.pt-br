---
title: "Introdução ao controle ReportViewer 2016 | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: application-integration
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: c42fbb1d3323eb3b151687d451958bc042fa8ef4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>Integrando o Reporting Services usando os controles ReportViewer – Introdução

Saiba como os desenvolvedores podem inserir relatórios paginados em sites ASP.NET e aplicativos do Windows Forms, por meio do controle ReportViewer do Reporting Services 2016. Adicione o controle a um novo projeto ou atualize um projeto existente.

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>Adicionando o controle ReportViewer a um novo projeto Web

1. Crie um novo **Site ASP.NET vazio** ou abra um projeto ASP.NET existente.

    ![ssRS-Create-New-ASPNET-Project](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Instale o pacote NuGet do controle ReportViewer 2016 por meio do **console do gerenciador de pacotes NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Adicione uma nova página .aspx ao projeto e registre o assembly de controle ReportViewer para uso na página.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Adicione um **ScriptManagerControl** à página.

5. Adicione o controle ReportViewer à página. O trecho abaixo pode ser atualizado para referenciar um relatório hospedado em um servidor de relatório remoto.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
A página final deve ser semelhante à mostrada a seguir.

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="http://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>

```

## <a name="updating-an-existing-project-to-use-the-reportviewer-control"></a>Atualizando um projeto existente para usar o controle ReportViewer

Para usar o controle ReportViewer 2016 em um projeto existente, adicione o controle por meio do NuGet e atualize as referências de assembly para a versão *14.0.0.0*. Isso incluirá a atualização do web.config do projeto e de todas as páginas .aspx que referenciam o controle ReportViewer.

### <a name="sample-webconfig-changes"></a>Alterações de exemplo em web.config

```
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  http://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 14.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 14.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 14.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 14.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>.aspx de exemplo

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>Adicionando o controle ReportViewer a um novo projeto do Windows Forms

1. Crie um novo **Aplicativo do Windows Forms** ou abra um projeto existente.

    ![ssRS-Create-New-winforms-Project](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Instale o pacote NuGet do controle ReportViewer 2016 por meio do **console do gerenciador de pacotes NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. Adicione um novo controle do código ou [adicione o controle à caixa de ferramentas](##adding-control-to-visual-studio-toolbar).

    ```
    private Microsoft.Reporting.WinForms.ReportViewer reportViewer1;
    
    private void InitializeComponent()
    {
        this.reportViewer1 = new Microsoft.Reporting.WinForms.ReportViewer();
        this.SuspendLayout();
        // 
        // reportViewer1
        // 
        this.reportViewer1.Location = new System.Drawing.Point(168, 132);
        this.reportViewer1.Name = "reportViewer1";
        this.reportViewer1.ServerReport.BearerToken = null;
        this.reportViewer1.Size = new System.Drawing.Size(396, 246);
        this.reportViewer1.TabIndex = 0;
        // 
        // Form1
        // 
        this.Controls.Add(this.reportViewer1);
    }
    ```

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>Como definir a altura em 100% no controle do Visualizador de Relatórios 2016

O novo controle do Visualizador de Relatórios 2016 é otimizado para páginas do modo de Padrões do HTML5 e funciona em todos os navegadores modernos. No passado, com o controle RVC antigo, quando você definia a propriedade de altura em 100%, ela funcionava, mesmo se nenhum dos ancestrais tinha a altura especificada. Esse comportamento foi alterado no HTML5. Quando você define essa propriedade no novo controle RVC, ela funcionará corretamente somente se o elemento pai tiver uma altura definida, ou seja, não for um valor automático ou se todos os ancestrais do RVC tiverem a altura em 100% também.

Veja abaixo os dois exemplos para fazer isso.

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>Definindo a altura de todos os elementos pai como 100%

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <style>
        html,body,form,#div1 {
            height: 100%; 
        }
    </style>
   </head>
<body>
    <form id="form1" runat="server">
    <div id="div1" >
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>Definindo o atributo de estilo de altura no pai do controle reportviewer

Para obter mais informações sobre tamanhos de percentual do visor, consulte [Tamanhos de percentual do visor](https://www.w3.org/TR/css3-values/#viewport-relative-lengths).

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

## <a name="adding-control-to-visual-studio-toolbar"></a>Adicionando um controle à barra de ferramentas do Visual Studio

O controle do Visualizador de Relatórios agora é fornecido como um pacote NuGet. Por isso, você não verá o Controle do Visualizador de Relatórios aparecer na caixa de ferramentas do Visual Studio, por padrão. Adicione o controle à caixa de ferramentas seguindo o procedimento abaixo.

1. Instale o pacote NuGet para o WinForms ou o WebForms, conforme mencionado acima.

2. Remova o Controle ReportViewer listado na caixa de ferramentas. Esse é o controle com a versão 12.x.

    ![ssRS-remove-old-rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. Clique com o botão direito do mouse em qualquer lugar da caixa de ferramentas e, em seguida, selecione **Escolher Itens...**.

    ![ssRS-toolbox-choose-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. Nos **Componentes do .NET Framework**, selecione **Procurar**.

    ![ssRS-toolbox-browse](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. Selecione o **Microsoft.ReportViewer.WinForms.dll** ou o **Microsoft.ReportViewer.WebForms.dll** do pacote NuGet instalado.

    > [!NOTE] 
    > O pacote NuGet será instalado no diretório da solução do projeto. O caminho para a dll será semelhante ao seguinte: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` ou `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`.

6. O novo controle deverá ser exibido na caixa de ferramentas. Em seguida, você poderá movê-lo para outra guia na caixa de ferramentas, se desejar.

    ![ssRS-toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>Considerações

- Isso adicionará uma referência ao pacote NuGet instalado no projeto atual. O item na caixa de ferramentas será persistido em outros projetos. Quando você instala o pacote NuGet em uma nova solução/projeto, o item de caixa de ferramentas pode referenciar uma versão mais antiga. 

- O controle permanecerá na caixa de ferramentas, mesmo se o assembly não estiver mais disponível. Se esse projeto foi excluído, o Visual Studio gerará um erro se você tentar adicionar o controle por meio da caixa de ferramentas. Para corrigir esse erro, remova o controle da caixa de ferramentas e adicione-o novamente usando as etapas acima.


## <a name="common-issues"></a>Problemas comuns
    
- O controle ReportViewer 2016 destina-se a ser usado com navegadores modernos. O controle poderá não funcionar se os navegadores renderizarem a página da Web em um modo de compatibilidade do IE. Os sites da intranet podem exigir uma marca META para substituir a configuração, o que incentiva a renderização de páginas da intranet no modo de compatibilidade.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>Fornecendo comentários

Informe a equipe sobre os problemas encontrados com o controle nos [fóruns do MSDN do Reporting Services](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices) ou por email em [RVCFeedback@microsoft.com](mailto:RVCFeedback@microsoft.com).

## <a name="see-also"></a>Consulte também

[Coleta de dados no controle ReportingViewer 2016](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
Ainda tem dúvidas? [Experimente o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)

