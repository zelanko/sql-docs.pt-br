---
title: Introdução ao controle ReportViewer 2016 | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: conceptual
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1fd408e5459aea50c04c29d234fce54d8a3ab772
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503914"
---
# <a name="integrating-reporting-services-using-the-report-viewer-controls---get-started"></a>Integrando o Reporting Services usando os controles do Visualizador de Relatórios – Introdução

Os controles do Visualizador de Relatórios podem ser usados para integrar relatórios de RDL do Reporting Services a aplicativos de WebForms e WinForms. Para obter informações detalhadas sobre atualizações recentes, consulte o [log de mudanças](changelog.md).

## <a name="adding-the-report-viewer-control-to-a-new-web-project"></a>Adicionando o controle do Visualizador de Relatórios a um novo projeto Web

1. Crie um novo **Site ASP.NET vazio** ou abra um projeto ASP.NET existente.

    ![ssRS-Create-New-ASPNET-Project](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Instale o pacote NuGet do controle do Visualizador de Relatórios por meio do **Console do gerenciador de pacotes NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Adicione uma nova página .aspx ao projeto e registre o assembly de controle do Visualizador de Relatórios para uso na página.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Adicione um **ScriptManagerControl** à página.

5. Adicione o controle do Visualizador de Relatórios à página. O snippet abaixo pode ser atualizado para referenciar um relatório hospedado em um servidor de relatório remoto.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
A página final deve ser semelhante à mostrada a seguir.

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

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
            <ServerReport ReportServerUrl="https://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>

```

## <a name="updating-an-existing-project-to-use-the-report-viewer-control"></a>Atualizando um projeto existente para usar o controle do Visualizador de Relatórios

Certifique-se de atualizar todas as referências de assembly para a versão *15.0.0.0*, incluindo o web.config do projeto e todas as páginas .aspx que referenciam o controle do visualizador.

### <a name="sample-webconfig-changes"></a>Alterações de exemplo em web.config

```
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  https://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 15.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 15.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 15.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 15.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>.aspx de exemplo

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 15.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-report-viewer-control-to-a-new-windows-forms-project"></a>Adicionando o controle do Visualizador de Relatórios a um novo projeto do Windows Forms

1. Crie um novo **Aplicativo do Windows Forms** ou abra um projeto existente.

    ![ssRS-Create-New-winforms-Project](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Instale o pacote NuGet do controle do Visualizador de Relatórios por meio do **Console do gerenciador de pacotes NuGet**.

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

## <a name="how-to-set-100-height-on-the-report-viewer-control"></a>Como definir a altura em 100% no controle do Visualizador de Relatórios

Se for definir a altura do controle do visualizador como 100%, o elemento pai precisará ter uma altura definida ou todos os ancestrais precisarão ter alturas de percentual.

### <a name="setting-the-height-of-all-the-ancestors-to-100"></a>Definir a altura de todos os ancestrais como 100%

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
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

### <a name="setting-the-parents-height-attribute"></a>Definir o atributo de altura do pai

Para obter mais informações sobre tamanhos de percentual do visor, consulte [Tamanhos de percentual do visor](http://www.w3.org/TR/css3-values/#viewport-relative-lengths).

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
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

## <a name="adding-control-to-visual-studio-toolbar"></a>Adicionando um controle à barra de ferramentas do Visual Studio

O controle do Visualizador de Relatórios agora é fornecido como um pacote NuGet e não é exibido na caixa de ferramentas do Visual Studio por padrão. É possível adicionar o controle à caixa de ferramentas manualmente.

1. Instale o pacote NuGet para o WinForms ou o WebForms, conforme mencionado acima.

2. Remova o controle do Visualizador de Relatórios listado na caixa de ferramentas.

    ![ssRS-remove-old-rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. Clique com o botão direito do mouse em qualquer lugar da caixa de ferramentas e, em seguida, selecione **Escolher Itens…**.

    ![ssRS-toolbox-choose-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. Nos **Componentes do .NET Framework**, selecione **Procurar**.

    ![ssRS-toolbox-browse](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. Selecione o **Microsoft.ReportViewer.WinForms.dll** ou o **Microsoft.ReportViewer.WebForms.dll** do pacote NuGet instalado.

    > [!NOTE] 
    > O pacote NuGet será instalado no diretório da solução do projeto. O caminho para a dll será semelhante ao seguinte: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` ou `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`.

6. O novo controle deverá ser exibido na caixa de ferramentas. Em seguida, você poderá movê-lo para outra guia na caixa de ferramentas, se desejar.

    ![ssRS-toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

## <a name="common-issues"></a>Problemas comuns
    
O controle do visualizador foi criado para navegadores modernos. O controle pode não funcionar conforme esperado se o navegador renderiza a página usando o modo de compatibilidade do IE. Sites da intranet podem exigir uma meta tag para substituir o comportamento do navegador padrão.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="feedback"></a>Comentários

Informe a equipe sobre problemas nos [Fóruns do Reporting Services](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices).

## <a name="see-also"></a>Confira também

[Coleta de dados no controle do Visualizador de Relatórios](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
Ainda tem dúvidas? [Experimente o fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)

