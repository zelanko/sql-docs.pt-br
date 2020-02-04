---
title: Prevenindo solicitações inválidas | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 219fc1883f395e56f1fd73af32e95ea066df28b7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62992216"
---
# <a name="preventing-invalid-requests"></a>Impedindo solicitações inválidas
  Você pode impedir que alguns tipos de exceções sejam lançados ao analisar o fluxo do seu aplicativo e garantir que as solicitações enviadas ao servidor de relatório sejam válidas. Por exemplo, em aplicativos que permitem que usuários adicionem ou atualizem o nome de um relatório, fonte de dados ou outro item de servidor de relatório, valide o texto que possa ser inserido por um usuário. Sempre verifique a existência de caracteres reservados antes de enviar a solicitação para um servidor de relatório. Use instruções **if** condicionais ou outros constructos lógicos no código para alertar o usuário de que ele não atendeu às condições necessárias para enviar solicitações ao servidor de relatório.  
  
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
  
 Para obter mais informações sobre os tipos de erros que podem ser impedidos antes das solicitações serem enviadas ao servidor de relatório, consulte [Tabela de erros SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md). Para obter mais informações sobre como aprimorar ainda mais o exemplo anterior usando blocos try/catch, consulte [Usando blocos Try e Catch](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException do Reporting Services +](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
