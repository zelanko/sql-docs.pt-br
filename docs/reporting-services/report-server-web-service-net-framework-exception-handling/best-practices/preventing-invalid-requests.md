---
title: "Impedindo solicitações inválidas | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 830e388abe098bab402e5af56486d1e6cd528e98
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="preventing-invalid-requests"></a>Impedindo solicitações inválidas
  Você pode impedir que alguns tipos de exceções sejam lançados ao analisar o fluxo do seu aplicativo e garantir que as solicitações enviadas ao servidor de relatório sejam válidas. Por exemplo, em aplicativos que permitem que usuários adicionem ou atualizem o nome de um relatório, fonte de dados ou outro item de servidor de relatório, valide o texto que possa ser inserido por um usuário. Sempre verifique a existência de caracteres reservados antes de enviar a solicitação para um servidor de relatório. Use condicional **se** instruções ou outras construções lógicas em seu código para alertar o usuário que ele não atendeu as condições necessárias para enviar solicitações para o servidor de relatório.  
  
 No exemplo de C# simplificado a seguir, os usuários obtêm uma mensagem de erro amigável quando tentam criar um relatório com um nome que contém um caractere de barra (/).  
  
```  
// C#  
private void PublishReport()  
{  
   int index;  
   string reservedChar;  
   string message;  
  
   // Check the text value of the name text box for "/",  
   // a reserved character  
   index = nameTextBox.Text.IndexOf(@"/");  
  
   if ( index != -1) // The text contains the character  
   {  
      reservedChar = nameTextBox.Text.Substring(index, 1);  
      // Build a user-friendly error message  
      message = "The name of the report cannot contain the reserved character " +  
         "\"" + reservedChar + "\". " +  
         "Please enter a valid name for the report. " +  
         "For more information about reserved characters, " +  
         "see the help documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      FileStream stream = File.OpenRead("MyReport.rdl");  
      definition = new Byte[stream.Length];  
      stream.Read(definition, 0, (int) stream.Length);  
      stream.Close();  
      // Create report with user-defined name  
      rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
      MessageBox.Show("Report: {0} created successfully", name);  
   }  
}  
```  
  
 Para obter mais informações sobre os tipos de erros que podem ser impedidos antes das solicitações são enviadas ao servidor de relatório, consulte [tabela de erros SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md). Para obter mais informações sobre como aprimorar ainda mais o exemplo anterior usando blocos try/catch, consulte [usando Try e Catch blocos](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md).  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services classe SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
