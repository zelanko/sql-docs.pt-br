---
title: Exemplo de fluxo de trabalho personalizado (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: develop
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: bfc0c557f8c645fe7dfa56850bce64b533bc9340
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="create-a-custom-workflow---example"></a>Criar um fluxo de trabalho personalizado – Exemplo
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], quando cria uma biblioteca de classes de fluxo de trabalho personalizado, você cria uma classe que implementa a interface Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender interface. Essa interface inclui um método, <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>que é chamado pelo Serviço de Integração de Fluxo de Trabalho MDS do SQL Server quando um fluxo de trabalho é iniciado. O método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> contém dois parâmetros: *workflowType* contém o texto que você inseriu na caixa de texto **Tipo de Fluxo de trabalho** no [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e *dataElement* contém metadados e dados de item sobre o item que disparou a regra de negócios do fluxo de trabalho.  
  
## <a name="custom-workflow-example"></a>Exemplo de fluxo de trabalho personalizado  
 O exemplo de código a seguir mostra como implementar o método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> para extrair os atributos Name, Code e LastChgUserName dos dados XML para o elemento que disparou a regra de negócio do fluxo de trabalho e como chamar um procedimento armazenado para inseri-los em outro banco de dados. Para obter um exemplo do XML dos dados de item e uma explicação das marcas que ele contém, consulte [Descrição de XML de fluxo de trabalho personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar um fluxo de trabalho personalizado &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  

