---
title: 'Lição 1: criar o projeto de esquema RDL do Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f420509c-51aa-4170-8c25-64c2954f4bb9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c34062acefc2dfd847790a39cea35b03727f49ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62678514"
---
# <a name="lesson-1-create-the-rdl-schema-visual-studio-project"></a>Lição 1: Criar o projeto do Visual Studio de esquema RDL
  Para este tutorial, você criará um aplicativo de console simples. Este tutorial pressupõe que você está desenvolvendo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]no.  
  
> [!NOTE]  
>  Ao acessar o serviço Web Servidor de Relatório que está em execução no [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] com Advanced Services, é preciso incluir "_SQLExpress" no caminho do "ReportServer". Por exemplo:  
>   
>  `http://myserver/reportserver_sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-create-the-web-service-proxy"></a>Para criar o proxy do serviço Web  
  
1.  No menu **Iniciar** , selecione **todos os programas**, Microsoft Visual Studio, em seguida, **Ferramentas do Visual Studio**e, em seguida, o Prompt de **comando do Visual Studio 2010**.  
  
2.  Na janela do prompt de comando, execute o seguinte comando se estiver usando o C#:  
  
    ```  
    wsdl /language:CS /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     Se estiver usando o Visual Basic, execute o seguinte comando:  
  
    ```  
    wsdl /language:VB /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     Esse comando gera um arquivo .cs ou .vb. Adicione esse arquivo ao seu aplicativo.  
  
### <a name="to-create-a-console-application"></a>Para criar um aplicativo de console  
  
1.  No menu **arquivo** , aponte para **novo**e clique em **projeto** para abrir a caixa de diálogo **novo projeto** .  
  
2.  No painel esquerdo, em **modelos instalados**, clique em **Visual Basic** ou no nó **Visual C#** e selecione uma categoria de tipos de projeto na lista expandida.  
  
3.  Escolha o tipo de projeto de **aplicativo de console** .  
  
4.  Na caixa **nome** , insira um nome para o seu projeto. Digite o nome `SampleRDLSchema`.  
  
5.  Na caixa **local** , digite o caminho onde você deseja salvar o projeto ou clique em **procurar** para navegar até a pasta.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]Uma exibição recolhida do seu projeto é exibida no Gerenciador de Soluções.  
  
7.  No menu **Projeto** , clique em **Adicionar Item Existente**.  
  
8.  Navegue até o local do arquivo. cs ou. vb gerado por você e, em seguida, selecione o arquivo e clique em **Adicionar**.  
  
     Você também precisará adicionar uma referência ao namespace <xref:System.Web.Services> para que a referência da Web funcione.  
  
9. No menu Projeto, clique em **Adicionar Referência**.  
  
     Na caixa de diálogo **Adicionar referência** , na guia **.net** , selecione **System. Web. Services**e clique em **OK**.  
  
     Para obter mais informações sobre como se conectar ao serviço Web servidor de relatórios, consulte [criando aplicativos usando o serviço Web e o .NET Framework](../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
10. No Gerenciador de Soluções, expanda o nó do projeto. Você verá que um arquivo de código com o nome padrão de Program.cs (Module1.vb para o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) foi adicionado ao seu projeto.  
  
11. Abra o arquivo Program.cs (Module1.vb para o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) e substitua o código pelo seguinte:  
  
     O código a seguir fornece os fragmentos de método que serão utilizados para implementar a funcionalidade Carregar, Atualizar e Salvar.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using System.Xml.Serialization;  
    using ReportService2010;  
  
    namespace SampleRDLSchema  
    {  
        class ReportUpdater  
        {  
            ReportingService2010 _reportService;  
  
            static void Main(string[] args)  
            {  
                ReportUpdater reportUpdater = new ReportUpdater();  
                reportUpdater.UpdateReport();  
            }  
  
            private void UpdateReport()  
            {  
                try  
                {  
                    // Set up the Report Service connection  
                    _reportService = new ReportingService2010();  
                    _reportService.Credentials =  
                        System.Net.CredentialCache.DefaultCredentials;  
                    _reportService.Url =  
                       "http://<Server Name>/reportserver/" +  
                                       "reportservice2010.asmx";  
  
                    // Call the methods to update a report definition  
                    LoadReportDefinition();  
                    UpdateReportDefinition();  
                    PublishReportDefinition();  
                }  
                catch (Exception ex)  
                {  
                    System.Console.WriteLine(ex.Message);  
                }  
            }  
  
            private void LoadReportDefinition()  
            {  
                //Lesson 3: Load a report definition from the report   
                //          catalog  
            }  
  
            private void UpdateReportDefinition()  
            {  
                //Lesson 4: Update the report definition using the    
                //          classes generated from the RDL Schema  
            }  
  
            private void PublishReportDefinition()  
            {  
                //Lesson 5: Publish the updated report definition back   
                //          to the report catalog  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Imports System  
    Imports System.Collections.Generic  
    Imports System.IO  
    Imports System.Text  
    Imports System.Xml  
    Imports System.Xml.Serialization  
    Imports ReportService2010  
  
    Namespace SampleRDLSchema  
  
        Module ReportUpdater  
  
            Private m_reportService As ReportingService2010  
  
            Public Sub Main(ByVal args As String())  
  
                Try  
                    'Set up the Report Service connection  
                    m_reportService = New ReportingService2010  
                    m_reportService.Credentials = _  
                        System.Net.CredentialCache.DefaultCredentials  
                    m_reportService.Url = _  
                        "http:// <Server Name>/reportserver/" & _  
                               "reportservice2010.asmx"  
  
                    'Call the methods to update a report definition  
                    LoadReportDefinition()  
                    UpdateReportDefinition()  
                    PublishReportDefinition()  
                Catch ex As Exception  
                    System.Console.WriteLine(ex.Message)  
                End Try  
  
            End Sub  
  
            Private Sub LoadReportDefinition()  
                'Lesson 3: Load a report definition from the report   
                '          catalog  
            End Sub  
  
            Private Sub UpdateReportDefinition()  
                'Lesson 4: Update the report definition using the   
                '          classes generated from the RDL Schema  
            End Sub  
  
            Private Sub PublishReportDefinition()  
                'Lesson 5: Publish the updated report definition back   
                '          to the report catalog  
            End Sub  
  
        End Module  
  
    End Namespace   
    ```  
  
## <a name="next-lesson"></a>Próxima lição  
 Na próxima lição, você usará a Ferramenta de Definição de Esquema XML (Xsd.exe) para gerar classes com base no esquema RDL e incluí-las no seu projeto. Consulte [lição 2: gerar classes a partir do esquema RDL usando a ferramenta xsd](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizando relatórios usando classes geradas do esquema RDL &#40;tutorial do SSRS&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [Linguagem RDL &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
