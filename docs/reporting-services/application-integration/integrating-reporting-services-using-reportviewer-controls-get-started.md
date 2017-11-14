---
title: "Guia de Introdução com o controle ReportViewer 2016 | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: 51c6e0a0baa59e49ae482db01253c1998894b5f8
ms.contentlocale: pt-br
ms.lasthandoff: 09/13/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>Integrando o Reporting Services usando os controles ReportViewer - Introdução

Saiba como os desenvolvedores podem incorporar relatórios paginados em sites da web ASP.NET e aplicativos de formulários do Windows, por meio do Reporting Services 2016 ReportViewer controle. Você pode adicionar o controle para um novo projeto, ou atualizar um projeto existente.

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>Adicionar o controle ReportViewer a um novo projeto da web

1. Criar um novo **Site vazio do ASP.NET** ou abrir um projeto existente do ASP.NET.

    ![Criar-novo-ASPNET-projeto ssRS](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Instale o pacote de nuget de controle ReportViewer 2016 por meio de **console de Gerenciador de pacote do Nuget**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Adicionar uma nova página. aspx ao projeto e registre o assembly de controle ReportViewer para uso dentro da página.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Adicionar um **ScriptManagerControl** para a página.

5. Adicione o controle ReportViewer para a página. O trecho a seguir pode ser atualizado para fazer referência a um relatório hospedado em um servidor de relatório remoto.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
A página final deve ser semelhante ao seguinte.

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

Para usar o controle ReportViewer 2016 em um projeto existente, adicione o controle por meio do Nuget e atualizar as referências de assembly para a versão *14.0.0.0*. Isso inclui a atualização Web. config do projeto e todas as páginas. aspx que referenciam o controle ReportViewer.

### <a name="sample-webconfig-changes"></a>Alterações de Web. config de exemplo

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

### <a name="sample-aspx"></a>Exemplo aspx

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>Adicionar o controle ReportViewer a um novo projeto do Windows Forms

1. Criar um novo **aplicativo do Windows Forms** ou abrir um projeto existente.

    ![Criar-novo-winforms-projeto ssRS](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Instale o pacote de nuget de controle ReportViewer 2016 por meio de **console de Gerenciador de pacote do Nuget**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. Adicione um novo controle de código ou [adicionar o controle à caixa de ferramentas](##adding-control-to-visual-studio-toolbar).

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

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>Como definir a altura de 100% do controle de 2016 do Visualizador de relatórios

O novo controle de 2016 do Visualizador de relatórios é otimizado para páginas de modo de padrões do HTML5 e funciona em todos os navegadores modernos. No passado, com o controle RVC antigo, quando você definir a propriedade de altura de 100%, funcionou mesmo se nenhum dos ancestrais tinha altura especificada. Esse comportamento foi alterado em HTML5. Quando você definir essa propriedade no novo controle RVC, ele funcionará corretamente somente se o elemento pai possui uma altura definida, ou seja, não é um valor de auto ou todos os ancestrais de RVC ter altura de 100% muito.

Abaixo estão os dois exemplos para fazer isso.

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>Definindo a altura do pai todos os elementos para 100%

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

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>Definindo o atributo de estilo a altura do pai do controle reportviewer

Para obter mais informações sobre tamanhos de porcentagem do visor, consulte [comprimentos de porcentagem do visor](https://www.w3.org/TR/css3-values/#viewport-relative-lengths).

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

## <a name="adding-control-to-visual-studio-toolbar"></a>Adicionando controle a barra de ferramentas do Visual Studio

O controle do Visualizador de relatórios agora é enviado como um pacote do NuGet. Por isso, você não verá o controle do Visualizador de relatórios aparecerão na caixa de ferramentas do Visual Studio, por padrão. Você pode adicionar o controle à caixa de ferramentas, fazendo o seguinte.

1. Instale o pacote NuGet do WinForms ou o WebForms conforme mencionado acima.

2. Remova o controle ReportViewer que está listado na caixa de ferramentas. Este é o controle com uma versão de 12. x.

    ![ssRS-remove-antigo-rvcontrol-caixa de ferramentas](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. Clique com botão direito em qualquer lugar na caixa de ferramentas e, em seguida, selecione **escolher itens...** .

    ![ssRS-caixa de ferramentas-escolha-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. Sobre o **componentes do .NET Framework**, selecione **procurar**.

    ![ssRS de caixa de ferramentas de navegação](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. Selecione o **Microsoft.ReportViewer.WinForms.dll** ou **Microsoft.ReportViewer.WebForms.dll** do pacote do NuGet é instalado.

    > [!NOTE] 
    > O pacote NuGet será instalado no diretório da solução do projeto. O caminho para a dll será semelhante à seguinte: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` ou `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`.

6. O novo controle deve exibir na caixa de ferramentas. Você pode movê-lo para outra guia na caixa de ferramentas se desejar.

    ![ssRS de caixa de ferramentas de rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>Coisas a serem consideradas

- Isso adicionará uma referência para o pacote do NuGet instalada em seu projeto atual. O item na caixa de ferramentas serão mantidas para outros projetos. Quando você instala o pacote do NuGet em uma nova solução/projeto, o item de caixa de ferramentas pode fazer referência a uma versão mais antiga. 

- O controle permanecerá na caixa de ferramentas, mesmo se o assembly não está disponível mais. Se esse projeto foi excluído, Visual Studio gerará um erro se você tentar e adicionar o controle da caixa de ferramentas. Para corrigir esse erro, remova o controle da caixa de ferramentas e adicioná-lo seguindo as etapas acima novamente.


## <a name="common-issues"></a>Problemas comuns
    
- O controle ReportViewer 2016 destina-se a ser usado com navegadores modernos. O controle pode não funcionar se navegadores renderizam a página da web em um modo de compatibilidade do Internet Explorer. Sites da intranet podem exigir uma meta tag para substituir a configuração que incentivamos páginas da intranet no modo de compatibilidade de renderização.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>Fornecendo comentários

Informar a equipe sobre problemas encontrados com o controle sobre o [fóruns do Reporting Services MSDN](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices) ou por meio de email em [ RVCFeedback@microsoft.com ](mailto:RVCFeedback@microsoft.com).

## <a name="see-also"></a>Consulte também

[Coleta de dados no controle ReportingViewer 2016](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
Ainda tem dúvidas? [Experimente o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)


