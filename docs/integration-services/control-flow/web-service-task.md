---
title: "Tarefa serviço da Web | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.webservicetask.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: f91aa6e47ee1255c97e8ffd2f91a5fb559a942ca
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="web-service-task"></a>Tarefa Serviços Web
  A tarefa Serviço Web executa um método de serviço Web. Você pode usar essa tarefa para os seguintes propósitos:  
  
-   Gravar em uma variável os valores retornados pelo método de serviço da Web. Por exemplo, você pode obter a temperatura mais alta do dia a partir do método de serviço da Web e, em seguida, pode utilizar esse valor para atualizar uma variável usada em uma expressão que define um valor de coluna.  
  
-   Gravar em um arquivo os valores retornados pelo método de serviço da Web. Por exemplo, uma lista de clientes potenciais pode ser gravada em um arquivo e o arquivo pode ser usado depois como fonte de dados em um pacote que limpa os dados antes de gravá-los em um banco de dados.  
  
## <a name="wsdl-file"></a>Arquivo WSDL  
 A tarefa Serviço da Web utiliza um gerenciador de conexões HTTP para se conectar ao serviço da Web. O gerenciador de conexões HTTP é configurado separadamente da tarefa Serviço da Web e é mencionado na tarefa. O gerenciador de conexões HTTP especifica as configurações de proxy do servidor como o URL do servidor, as credenciais para acessar o servidor de serviços da Web e a duração do tempo limite. Para obter mais informações, consulte [Gerenciador de Conexões HTTP](../../integration-services/connection-manager/http-connection-manager.md).  
  
> [!IMPORTANT]  
>  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 O gerenciador de conexões HTTP pode apontar para um site da Web ou para um arquivo WSDL (Web Service Description Language). O URL do gerenciador de conexões HTTP que aponta para um arquivo WSDL inclui o parâmetro `?WSDL` : por exemplo, `http://MyServer/MyWebService/MyPage.asmx?WSDL`.  
  
 O arquivo WSDL deve estar disponível localmente para configurar a tarefa Serviço da Web usando a caixa de diálogo **Editor da Tarefa Serviço da Web** que o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece.  
  
-   Se o gerenciador de conexões HTTP apontar para um site da Web, o arquivo WSDL deve ser copiado manualmente em um computador local.  
  
-   Se o gerenciador de conexões HTTP apontar para um arquivo WSDL, o arquivo poderá ser baixado de um site para um arquivo local através da tarefa Serviço da Web.  
  
 O arquivo WSDL lista os métodos oferecidos pelo serviço da Web, os parâmetros de entrada necessários para os métodos, as respostas que os métodos retornam e como comunicar-se com o serviço da Web.  
  
 Se o método utilizar parâmetros de entrada, a tarefa Serviço da Web necessitará de valores de parâmetro. Por exemplo, um método de serviço da Web que recomenda o comprimento dos esquis que você deve comprar com base em sua altura requer que sua altura seja apresentada em um parâmetro de entrada. Os valores de parâmetro podem ser fornecidos por uma cadeia de caracteres definida na tarefa, por variáveis definidas no escopo da tarefa ou por um contêiner pai. Usar variáveis é vantajoso porque elas permitem a atualização dinâmica de valores de parâmetro por meio de configurações de pacote ou scripts. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Configurações de pacote](../../integration-services/packages/package-configurations.md).  
  
 Muitos métodos de serviço da Web não utilizam parâmetros de entrada. Por exemplo, um método de serviço da Web que busca nomes de presidentes que nasceram no mês atual não exigirá um parâmetro de entrada porque o serviço da Web pode determinar o mês atual localmente.  
  
 Os resultados do método de serviço da Web podem ser gravados em uma variável ou em um arquivo. Use o gerenciador de conexões de arquivos para especificar o arquivo ou fornecer o nome da variável na qual os resultados serão gravados. Para obter mais informações, consulte [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md) e [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Mensagens de log personalizadas disponíveis na tarefa Serviço da Web  
 A tabela a seguir relaciona as entradas de log personalizadas que podem ser habilitadas para a tarefa Serviço da Web. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|A tarefa começou a acessar um serviço Web.|  
|**WSTaskEnd**|A tarefa completou um método de serviço Web.|  
|**WSTaskInfo**|Informações descritivas sobre a tarefa.|  
  
## <a name="configuration-of-the-web-service-task"></a>Configuração da tarefa Serviço Web  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor da Tarefa Serviço da Web &#40;Página Geral&#41;](../../integration-services/control-flow/web-service-task-editor-general-page.md)  
  
-   [Editor da Tarefa Serviço Web &#40;Página Entrada&#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)  
  
-   [Editor da Tarefa Serviço Web &#40;Página Saída&#41;](../../integration-services/control-flow/web-service-task-editor-output-page.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Configuração programática da tarefa Serviço Web  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique em um dos tópicos a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Vídeo, [Como: Chamar um serviço Web usando a tarefa Serviço da Web (vídeo do SQL Server)](http://go.microsoft.com/fwlink/?LinkId=259642), no technet.microsoft.com.  

