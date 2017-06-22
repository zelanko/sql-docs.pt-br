---
title: "Usando o acesso à URL em um aplicativo do Windows | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Windows applications [Reporting Services]
- Web Browser controls [Reporting Services]
- Windows Forms [Reporting Services]
- browser controls [Reporting Services]
- URL access [Reporting Services], Windows applications
ms.assetid: a4b222e5-0cbd-409c-92c4-046a674db8ac
caps.latest.revision: 48
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6174bfd45317faf9b6c8c7131dd1c5026d3a4d51
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="integrating-reporting-services-using-url-access---windows-application"></a>Integrando o Reporting Services usando o acesso de URL - o aplicativo do Windows
  Embora o acesso à URL a um servidor de relatório seja otimizado para um ambiente da Web, você também pode usá-lo para inserir relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. No entanto, o acesso à URL que envolve o Windows Forms ainda exige que você use tecnologia de navegador da Web. Você pode usar os seguintes cenários de integração com o acesso à URL e o Windows Forms:  
  
-   Exiba um relatório de um aplicativo Windows Form iniciando um navegador da Web programaticamente.  
  
-   Use o controle <xref:System.Windows.Forms.WebBrowser> em um Windows Form para exibir um relatório.  
  
## <a name="starting-internet-explorer-from-a-windows-form"></a>Iniciando o Internet Explorer a partir de um Windows Form  
 Você pode usar a classe <xref:System.Diagnostics.Process> para acessar um processo que esteja em execução em um computador. O <xref:System.Diagnostics.Process> classe é útil [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] construção para iniciar, parar, controlar e monitorar aplicativos. Para exibir um relatório específico em seu banco de dados do servidor de relatório, você pode iniciar o **IExplore** processo, passando a URL para o relatório. O exemplo de código a seguir pode ser usado para iniciar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer e para passar uma URL específica do relatório quando o usuário clicar em um botão de um Windows Form.  
  
```vb  
Private Sub viewReportButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles viewReportButton.Click  
   ' Build the URL access string based on values supplied by a user  
   Dim url As String = serverUrlTextBox.Text + "?" & reportPathTextBox.Text & _  
   "&rs:Command=Render" & "&rs:Format=HTML4.0"  
  
   ' If the user does not select the toolbar check box,  
   ' turn the toolbar off in the HTML Viewer  
   If toolbarCheckBox.Checked = False Then  
      url += "&rc:Toolbar=False"  
   End If  
   ' load report in the Web browser  
   Try  
      System.Diagnostics.Process.Start("IExplore", url)  
   Catch  
      MessageBox.Show("The system could not start the specified report using Internet Explorer.", _  
      "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error)  
   End Try  
End Sub 'viewReportButton_Click  
```  
  
```csharp  
// Sample click event for a Button control on a Windows Form  
private void viewReportButton_Click(object sender, System.EventArgs e)  
{  
   // Build the URL access string based on values supplied by a user  
   string url = serverUrlTextBox.Text + "?" + reportPathTextBox.Text +  
      "&rs:Command=Render" + "&rs:Format=HTML4.0";  
  
   // If the user does not check the toolbar check box,  
   // turn the toolbar off in the HTML Viewer  
   if (toolbarCheckBox.Checked == false)  
      url += "&rc:Toolbar=False";  
  
   // load report in the Web browser  
   try  
   {  
      System.Diagnostics.Process.Start("IExplore", url);  
   }  
  
   catch (Exception)  
   {  
      MessageBox.Show(  
         "The system could not open the specified report using Internet Explorer.",   
         "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error);  
   }  
}  
```  
  
## <a name="embedding-a-browser-control-on-a-windows-form"></a>Inserindo um controle de navegador em um Windows Form  
 Se você não quiser exibir o seu relatório em um navegador da Web externo, poderá inserir um navegador da Web de forma direta, como parte do seu Windows Form, usando o controle <xref:System.Windows.Forms.WebBrowser>.  
  
###### <a name="to-add-the-webbrowser-control-to-your-windows-form"></a>Para adicionar o controle WebBrowser ao seu Windows Form  
  
1.  Criar um novo aplicativo do Windows no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
2.  Localize o <xref:System.Windows.Forms.WebBrowser> controlar o **caixa de ferramentas** caixa de diálogo.  
  
     Se o **caixa de ferramentas** é não visível você pode acessá-la clicando o **exibição** item de menu e selecionando **caixa de ferramentas**.  
  
3.  Arraste o <xref:System.Windows.Forms.WebBrowser>controle para a superfície de design do seu Windows Form.  
  
     O <xref:System.Windows.Forms.WebBrowser>controle chamado webBrowser1 será adicionado ao formulário  
  
 Direcione o <xref:System.Windows.Forms.WebBrowser> controle a uma URL chamando seu **navegar** método. Você pode atribuir uma cadeia de caracteres de acesso à URL específica ao seu controle <xref:System.Windows.Forms.WebBrowser> em tempo de execução como mostrado no exemplo a seguir.  
  
```vb  
Dim url As String = "http://localhost/reportserver?/" & _  
                    "AdventureWorks2012 Sample Reports/" & _  
                    "Company Sales&rs:Command=Render"  
WebBrowser1.Navigate(url)  
```  
  
```csharp  
string url = "http://localhost/reportserver?/" +  
             "AdventureWorks2012 Sample Reports/" +  
             "Company Sales&rs:Command=Render";  
webBrowser1.Navigate(url);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Integrando o Reporting Services em aplicativos](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integrando o Reporting Services usando o acesso à URL](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Integrando o Reporting Services usando SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)   
 [Integrando o Reporting Services usando os controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)   
 [Acesso à URL &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md)  
  
  
