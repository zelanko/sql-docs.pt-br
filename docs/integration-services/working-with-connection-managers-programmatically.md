---
title: "Trabalhando programaticamente com gerenciadores de Conexão | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9093b9eadce231aea248cd04c2b57dc5dd5e1a76
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="working-with-connection-managers-programmatically"></a>Trabalhando programaticamente com gerenciadores de conexões
  Em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], o método AcquireConnection da classe de Gerenciador de conexão associado é o método que você chamar a maioria das vezes, quando você estiver trabalhando com gerenciadores de conexão no código gerenciado. Quando você escreve código gerenciado, você precisa chamar o método AcquireConnection para usar a funcionalidade de uma conexão manager. Chame esse método independentemente de estar escrevendo o código gerenciado em uma tarefa Script, em um componente Script, em um objeto personalizado ou em uma aplicação personalizada.  
  
 Para chamar o método AcquireConnection com êxito, você precisa saber as respostas às seguintes perguntas:  
  
-   **Quais gerenciadores de conexão retornam um objeto gerenciado do método AcquireConnection?**  
  
     Muitos gerenciadores de conexão retornam objetos não gerenciados ( ComObject) e esses objetos facilmente não podem ser usados no código gerenciado. A lista desses gerenciadores de conexões inclui o OLE DB, que é usado com frequência.  
  
-   **Para esses gerenciadores de conexão que retornam um objeto gerenciado, quais objetos seus métodos AcquireConnection retornarem?**  
  
     Para converter o valor de retorno para o tipo apropriado, você precisa saber o tipo de objeto que retorna o método AcquireConnection. Por exemplo, o método AcquireConnection para o [!INCLUDE[vstecado](../includes/vstecado-md.md)] Gerenciador de conexão retorna um objeto SqlConnection aberto quando você usa o provedor SqlClient. No entanto, o método AcquireConnection para o Gerenciador de conexão de arquivo apenas retorna uma cadeia de caracteres.  
  
 Este tópico responde a essas perguntas para os gerenciadores de conexões incluídos no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>Gerenciadores de conexões que não retornam um objeto gerenciado  
 A tabela a seguir lista os gerenciadores de conexão que retornam um objeto COM nativo ( ComObject) do método AcquireConnection. Esses objetos não gerenciados não podem ser usados facilmente pelo código gerenciado.  
  
|Tipo do gerenciador de conexões|Nome do Gerenciador de Conexão|  
|-----------------------------|-----------------------------|  
|ADO|Gerenciador de conexões ADO|  
|MSOLAP90|Gerenciador de conexões [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|  
|EXCEL|Gerenciador de conexões do Excel|  
|FTP|Gerenciador de conexões FTP|  
|HTTP|Gerenciador de conexões HTTP|  
|ODBC|gerenciador de conexões ODBC|  
|OLEDB|gerenciador de conexões OLE DB|  
  
 Normalmente, você pode usar um [!INCLUDE[vstecado](../includes/vstecado-md.md)] Gerenciador de conexão de código gerenciado para se conectar a uma fonte de dados ADO, Excel, ODBC ou OLE DB.  
  
## <a name="return-values-from-the-acquireconnection-method"></a>Valores de retorno do método AcquireConnection  
 A tabela a seguir lista os gerenciadores de conexão que retornam um objeto gerenciado do método AcquireConnection. Esses objetos gerenciados podem ser usados facilmente pelo código gerenciado.  
  
|Tipo do gerenciador de conexões|Nome do Gerenciador de Conexão|Tipo de valor de retorno|Informações adicionais|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Gerenciador de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)]|**SqlConnection**||  
|FILE|Gerenciador de conexões de arquivos|**System. String**|Caminho para o arquivo.|  
|FLATFILE|Gerenciador de conexões de arquivos simples|**System. String**|Caminho para o arquivo.|  
|MSMQ|Gerenciador de conexões MSMQ|**System.Messaging.MessageQueue**||  
|MULTIFILE|Gerenciador de conexões de vários arquivos|**System. String**|Caminho para um dos arquivos.|  
|MULTIFLATFILE|Gerenciador de conexões de vários arquivos simples|**System. String**|Caminho para um dos arquivos.|  
|SMOServer|gerenciador de conexões SMO|**Microsoft.SqlServer.Management.Smo.Server**||  
|SMTP|Gerenciador de conexões SMTP|**System. String**|Por exemplo: `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|Gerenciador de conexões WMI|**System.Management.ManagementScope**||  
|SQLMOBILE|Gerenciador de conexões do SQL Server Compact|**System.Data.SqlServerCe.SqlCeConnection**||  
  
## <a name="see-also"></a>Consulte também  
 [Conectando-se a fontes de dados na tarefa Script](../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [Conectando-se a fontes de dados no componente Script](../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [Conectar-se a fontes de dados em uma tarefa personalizada](../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
