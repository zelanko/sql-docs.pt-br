---
title: Trabalhar programaticamente com gerenciadores de conexões | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- connection managers [Integration Services], programming
ms.assetid: 2686fe84-1ecc-48b8-9160-e7122274bd84
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 973cb7dcfe7eb95e003428adf0c8a0beb7e68e87
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374564"
---
# <a name="working-with-connection-managers-programmatically"></a>Trabalhando programaticamente com gerenciadores de conexões
  No [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], o método AcquireConnection da classe do gerenciador de conexões associado é o método chamado com maior frequência quando você trabalha com gerenciadores de conexões em código gerenciado. Ao escrever código gerenciado, chame o método AcquireConnection para usar a funcionalidade de um gerenciador de conexões. Chame esse método independentemente de estar escrevendo o código gerenciado em uma tarefa Script, em um componente Script, em um objeto personalizado ou em uma aplicação personalizada.  
  
 Para chamar o método AcquireConnection com êxito, você precisa saber as respostas para as seguintes perguntas:  
  
-   **Quais gerenciadores de conexões retornam um objeto gerenciado do método AcquireConnection?**  
  
     Muitos gerenciadores de conexões retornam objetos COM não gerenciados (System.__ComObject) e esses objetos não podem ser usados com facilidade por meio do código gerenciado. A lista desses gerenciadores de conexões inclui o OLE DB, que é usado com frequência.  
  
-   **Que objetos são retornados pelos métodos AcquireConnection dos gerenciadores de conexões que retornam um objeto gerenciado?**  
  
     Para converter o valor retornado no tipo apropriado, você precisa saber que tipo de objeto é retornado pelo método AcquireConnection. Por exemplo, o método AcquireConnection do gerenciador de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)] retorna um objeto aberto do SqlConnection quando você usa o provedor SqlClient. Porém, o método AcquireConnection do gerenciador de conexões do arquivo só retorna uma cadeia de caracteres.  
  
 Este tópico responde a essas perguntas para os gerenciadores de conexões incluídos no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## <a name="connection-managers-that-do-not-return-a-managed-object"></a>Gerenciadores de conexões que não retornam um objeto gerenciado  
 A tabela a seguir lista os gerenciadores de conexões que retornam um objeto COM nativo (System.__ComObject) do método AcquireConnection. Esses objetos não gerenciados não podem ser usados facilmente pelo código gerenciado.  
  
|Tipo do gerenciador de conexões|Nome do gerenciador de conexões|  
|-----------------------------|-----------------------------|  
|ADO|Gerenciador de conexões ADO|  
|MSOLAP90|Gerenciador de conexões [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|  
|EXCEL|Gerenciador de conexões do Excel|  
|FTP|Gerenciador de conexões FTP|  
|HTTP|Gerenciador de conexões HTTP|  
|ODBC|gerenciador de conexões ODBC|  
|OLEDB|gerenciador de conexões OLE DB|  
  
 Em geral, você pode usar um gerenciador de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)] de código gerenciado para se conectar a um ADO, Excel, ODBC ou fonte de dados OLE DB.  
  
## <a name="return-values-from-the-acquireconnection-method"></a>Valores de retorno do método AcquireConnection  
 A tabela a seguir lista os gerenciadores de conexões que retornam um objeto gerenciado do método AcquireConnection. Esses objetos gerenciados podem ser usados facilmente pelo código gerenciado.  
  
|Tipo do gerenciador de conexões|Nome do gerenciador de conexões|Tipo de valor de retorno|Informações adicionais|  
|-----------------------------|-----------------------------|--------------------------|----------------------------|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Gerenciador de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)]|`System.Data.SqlClient.SqlConnection`||  
|FILE|Gerenciador de conexões de arquivos|`System.String`|Caminho para o arquivo.|  
|FLATFILE|Gerenciador de conexões de arquivos simples|`System.String`|Caminho para o arquivo.|  
|MSMQ|Gerenciador de conexões MSMQ|`System.Messaging.MessageQueue`||  
|MULTIFILE|Gerenciador de conexões de vários arquivos|`System.String`|Caminho para um dos arquivos.|  
|MULTIFLATFILE|Gerenciador de conexões de vários arquivos simples|`System.String`|Caminho para um dos arquivos.|  
|SMOServer|gerenciador de conexões SMO|`Microsoft.SqlServer.Management.Smo.Server`||  
|SMTP|Gerenciador de conexões SMTP|`System.String`|Por exemplo: `SmtpServer=<server name>;UseWindowsAuthentication=True;EnableSsl=False;`|  
|WMI|Gerenciador de conexões WMI|`System.Management.ManagementScope`||  
|SQLMOBILE|Gerenciador de conexões do SQL Server Compact|`System.Data.SqlServerCe.SqlCeConnection`||  
  
![Ícone do Integration Services (pequeno)](media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Conectar-se a fontes de dados na tarefa Script](extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)   
 [Conectar-se a fontes de dados no componente de Script](extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)   
 [Conectar-se a fontes de dados em uma tarefa personalizada](extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
  
  
