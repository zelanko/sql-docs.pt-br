---
title: 'Lição 3: Acessando o serviço Web | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c3e4c198-ab35-4548-9471-1b4e6b6e5dfd
author: craigg-msft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c93def5590b634d2fb3f8374b5fb875fd2d740eb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108296"
---
# <a name="lesson-3-accessing-the-web-service"></a>Lição 3: Acessando o serviço Web
  Depois que você adicionar uma referência para o serviço Web Servidor de Relatórios ao seu projeto, a próxima etapa será criar uma instância da classe proxy do serviço Web. Assim, você poderá acessar os métodos do serviço Web chamando os métodos na classe proxy. Quando o aplicativo chama esses métodos, o proxy do código gerado da classe [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] manipula as comunicações entre seu aplicativo e o serviço Web.  
  
 Primeiro, você criará uma instância da classe de proxy do serviço Web, <xref:ReportService2010.ReportingService2010>. Em seguida, você fará uma chamada ao método <xref:ReportService2010.ReportingService2010.GetProperties%2A> do serviço Web usando a classe proxy. Use a chamada para recuperar o nome e descrição de um dos relatórios de exemplo, Company Sales.  
  
> [!NOTE]  
>  Ao acessar um serviço Web executado no [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] com Serviços Avançados, você deve acrescentar "$SQLExpress" ao caminho de "ReportServer". Por exemplo:  
>   
>  `http://<Server Name>/reportserver$sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-access-the-web-service"></a>Para acessar o serviço Web  
  
1.  Primeiro, adicione o namespace ao arquivo Program.cs (Module1.vb no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) acrescentando uma diretiva `using` (`Imports` no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) ao arquivo de código. Se você usar essa política, não precisará qualificar os tipos completamente no namespace.  
  
2.  Para fazer isso, adicione o seguinte código ao início de seu arquivo de código:  
  
    ```vb  
    Imports System  
    Imports GetPropertiesSample.ReportService2010  
    ```  
  
    ```csharp  
    using System;  
    using GetPropertiesSample.ReportService2010;  
    ```  
  
3.  Após a inserção da diretiva de namespace no arquivo de código, digite o código a seguir no método Main do aplicativo de console. Não se esqueça de alterar o nome do servidor ao configurar a propriedade **Url** da instância do serviço Web:  
  
    ```vb  
    Sub Main()  
       Dim rs As New ReportingService2010  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx"  
  
       Dim name As New [Property]  
       name.Name = "Name"  
  
       Dim description As New [Property]  
       description.Name = "Description"  
  
       Dim properties(1) As [Property]  
       properties(0) = name  
       properties(1) = description  
  
       Try  
          Dim returnProperties As [Property]() = rs.GetProperties( _  
             "/AdventureWorks 2012 Sample Reports/Company Sales 2012", properties)  
  
          Dim p As [Property]  
          For Each p In returnProperties  
              Console.WriteLine((p.Name + ": " + p.Value))  
          Next p  
  
       Catch e As Exception  
          Console.WriteLine(e.Message)  
       End Try  
    End Sub  
    ```  
  
    ```csharp  
    static void Main(string[] args)  
    {  
       ReportingService2010 rs = new ReportingService2010();  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx";  
  
       Property name = new Property();  
       name.Name = "Name";  
  
       Property description = new Property();  
       description.Name = "Description";  
  
       Property[] properties = new Property[2];  
       properties[0] = name;  
       properties[1] = description;  
  
       try  
       {  
          Property[] returnProperties = rs.GetProperties(  
          "/AdventureWorks 2012 Sample Reports/Company Sales 2012",properties);  
  
          foreach (Property p in returnProperties)  
          {  
             Console.WriteLine(p.Name + ": " + p.Value);  
          }  
       }  
  
       catch (Exception e)  
       {  
          Console.WriteLine(e.Message);  
       }  
    }  
    ```  
  
4.  Salve a solução.  
  
 O código de exemplo passo a passo usa o <xref:ReportService2010.ReportingService2010.GetProperties%2A> método do serviço Web para recuperar propriedades de relatório de exemplo, Company Sales 2012. O <xref:ReportService2010.ReportingService2010.GetProperties%2A> método requer dois argumentos: o nome do relatório para o qual você deseja recuperar informações de propriedade e uma matriz de **Property []** objetos que contém os nomes das propriedades cujos valores você deseja recuperar. O método também retorna uma matriz de **Property []** objetos que contém os nomes e valores das propriedades especificadas no argumento de propriedades.  
  
> [!NOTE]  
>  Se você fornecer um vazio **Property []** matriz para o argumento de propriedades, todas as propriedades disponíveis são retornadas.  
  
 No exemplo anterior, o código usa o método <xref:ReportService2010.ReportingService2010.GetProperties%2A> para retornar o nome e a descrição do relatório de exemplo, Company Sales 2012. O código usa um loop `foreach` para gravar as propriedades e os valores no console.  
  
 Para obter mais informações sobre como criar e usar uma classe proxy para o serviço Web servidor de relatório, consulte [criando o Proxy de serviço Web](../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md).  
  
## <a name="see-also"></a>Consulte também  
 [Lição 4: Executando o aplicativo &#40;VB VC&#35;&#41;](../../2014/tutorials/lesson-4-running-the-application-vb-vcsharp.md)   
 [Acessando o serviço de Web do servidor de relatório usando o Visual Basic ou Visual C&#35; &#40;Tutorial do SSRS&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
