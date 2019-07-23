---
title: Tarefa Serviço Web | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.webservicetask.f1
- sql13.dts.designer.webservicestask.general.f1
- sql13.dts.designer.webservicestask.input.f1
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9c3c18f666c4e7b7e5f1d161fb78535e8005f1a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045616"
---
# <a name="web-service-task"></a>Tarefa Serviços Web

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa Serviço Web executa um método de serviço Web. Você pode usar essa tarefa para os seguintes propósitos:  
  
-   Gravar em uma variável os valores retornados pelo método de serviço da Web. Por exemplo, você pode obter a temperatura mais alta do dia a partir do método de serviço da Web e, em seguida, pode utilizar esse valor para atualizar uma variável usada em uma expressão que define um valor de coluna.  
  
-   Gravar em um arquivo os valores retornados pelo método de serviço da Web. Por exemplo, uma lista de clientes potenciais pode ser gravada em um arquivo e o arquivo pode ser usado depois como fonte de dados em um pacote que limpa os dados antes de gravá-los em um banco de dados.  
  
## <a name="wsdl-file"></a>Arquivo WSDL  
 A tarefa Serviço da Web utiliza um gerenciador de conexões HTTP para se conectar ao serviço da Web. O gerenciador de conexões HTTP é configurado separadamente da tarefa Serviço da Web e é mencionado na tarefa. O gerenciador de conexões HTTP especifica as configurações de proxy do servidor como o URL do servidor, as credenciais para acessar o servidor de serviços da Web e a duração do tempo limite. Para obter mais informações, consulte [Gerenciador de Conexões HTTP](../../integration-services/connection-manager/http-connection-manager.md).  
  
> [!IMPORTANT]  
>  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 O gerenciador de conexões HTTP pode apontar para um site da Web ou para um arquivo WSDL (Web Service Description Language). O URL do gerenciador de conexões HTTP que aponta para um arquivo WSDL inclui o parâmetro `?WSDL` : por exemplo, `https://MyServer/MyWebService/MyPage.asmx?WSDL`.  
  
 O arquivo WSDL deve estar disponível localmente para configurar a tarefa Serviço da Web usando a caixa de diálogo **Editor da Tarefa Serviço da Web** que o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece.  
  
-   Se o gerenciador de conexões HTTP apontar para um site da Web, o arquivo WSDL deve ser copiado manualmente em um computador local.  
  
-   Se o gerenciador de conexões HTTP apontar para um arquivo WSDL, o arquivo poderá ser baixado de um site para um arquivo local através da tarefa Serviço da Web.  
  
 O arquivo WSDL lista os métodos oferecidos pelo serviço da Web, os parâmetros de entrada necessários para os métodos, as respostas que os métodos retornam e como comunicar-se com o serviço da Web.  
  
 Se o método utilizar parâmetros de entrada, a tarefa Serviço da Web necessitará de valores de parâmetro. Por exemplo, um método de serviço da Web que recomenda o comprimento dos esquis que você deve comprar com base em sua altura requer que sua altura seja apresentada em um parâmetro de entrada. Os valores de parâmetro podem ser fornecidos por uma cadeia de caracteres definida na tarefa, por variáveis definidas no escopo da tarefa ou por um contêiner pai. Usar variáveis é vantajoso porque elas permitem a atualização dinâmica de valores de parâmetro por meio de configurações de pacote ou scripts. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Configurações de pacote](../../integration-services/packages/package-configurations.md).  
  
 Muitos métodos de serviço da Web não utilizam parâmetros de entrada. Por exemplo, um método de serviço da Web que busca nomes de presidentes que nasceram no mês atual não exigirá um parâmetro de entrada porque o serviço da Web pode determinar o mês atual localmente.  
  
 Os resultados do método de serviço da Web podem ser gravados em uma variável ou em um arquivo. Use o gerenciador de conexões de arquivos para especificar o arquivo ou fornecer o nome da variável na qual os resultados serão gravados. Para obter mais informações, consulte [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md) e [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Mensagens de log personalizadas disponíveis na tarefa Serviço da Web  
 A tabela a seguir relaciona as entradas de log personalizadas que podem ser habilitadas para a tarefa Serviço da Web. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**WSTaskBegin**|A tarefa começou a acessar um serviço Web.|  
|**WSTaskEnd**|A tarefa completou um método de serviço Web.|  
|**WSTaskInfo**|Informações descritivas sobre a tarefa.|  
  
## <a name="configuration-of-the-web-service-task"></a>Configuração da tarefa Serviço Web  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Configuração programática da tarefa Serviço Web  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique em um dos tópicos a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="web-service-task-editor-general-page"></a>Editor da Tarefa Serviço da Web (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Serviços da Web** para especificar um gerenciador de conexões HTTP, o local do arquivo WSDL (linguagem WSDL) usado pela tarefa, descrever a tarefa Serviços da Web e baixar o arquivo WSDL.  
  
### <a name="options"></a>Opções  
 **HTTPConnection**  
 Selecione um gerenciador de conexões na lista ou clique em \<**Nova conexão…** > para criar um novo gerenciador de conexões.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 **Tópicos relacionados:**  [Gerenciador de Conexões de HTTP](../../integration-services/connection-manager/http-connection-manager.md), [Editor do Gerenciador de Conexões de HTTP &#40;página Servidor&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 Digite o caminho totalmente qualificado de um arquivo WSDL que é local para o computador ou clique no botão Procurar **(…)** e localize esse arquivo.  
  
 Se o arquivo WSDL já foi baixado manualmente no computador, selecione-o. No entanto, se o arquivo WSDL ainda não tiver sido baixado, siga estas etapas:  
  
-   Crie um arquivo vazio que tenha a extensão de nome de arquivo ".wsdl".  
  
-   Selecione esse arquivo vazio para a opção **Arquivo WSDL** .  
  
-   Defina o valor de **OverwriteWSDLFile** como **True** para permitir que o arquivo vazio seja substituído pelo arquivo WSDL real.  
  
-   Clique em **Baixar WSDL** para baixar o arquivo WSDL real e substituir o arquivo vazio.  
  
    > [!NOTE]  
    >  A opção **Baixar WSDL** não será habilitada até que você forneça o nome de um arquivo local existente na caixa **Arquivo WSDL** .  
  
 **OverwriteWSDLFile**  
 Indique se o arquivo WSDL da tarefa Serviço da Web pode ser substituído.  
  
 Para baixar o arquivo WSDL usando o botão **Baixar WSDL** , defina esse valor como **True**.  
  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Serviço da Web. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Serviço da Web.  
  
 **Baixar WSDL**  
 Faça o download do arquivo WSDL.  
  
 Esse botão não estará habilitado até que você forneça o nome de um arquivo local existente na caixa **Arquivo WSDL** .  
  
## <a name="web-service-task-editor-input-page"></a>Editor da Tarefa Serviço da Web (página Entrada)
  Use a página **Entrada** da caixa de diálogo do **Editor da Tarefa Serviço da Web** para especificar o Serviço da Web, o método Web e os valores a serem fornecidos ao método Web como entrada. Os valores podem ser fornecidos digitando cadeias de caracteres diretamente na coluna Valor ou selecionando variáveis na coluna Valor.  
  
### <a name="options"></a>Opções  
 **Serviço**  
 Selecione na lista um serviço da Web a ser usado para executar o método Web.  
  
 **Método**  
 Selecione na lista um método Web a ser executado pela tarefa.  
  
 **WebMethodDocumentation**  
 Digite uma descrição do método Web ou clique no botão Procurar **(...)** e digite a descrição na caixa de diálogo **Documentação do Método Web**.  
  
 **Nome**  
 Lista os nomes das entradas no método Web.  
  
 **Tipo**  
 Lista o tipo de dados das entradas.  
  
> [!NOTE]  
>  A tarefa Serviço da Web só suporta parâmetros dos seguintes tipos de dados: tipos primitivos, como números inteiros e cadeias de caracteres; matrizes e sequências de tipos primitivos; e enumerações.  
  
 **Variável**  
 Marque as caixas de seleção para usar variáveis para fornecer entradas.  
  
 **Value**  
 Se as caixas de seleção Variável forem marcadas, selecione as variáveis na lista para fornecer as entradas; caso contrário, digite os valores a serem usados nas entradas.  
  
## <a name="web-service-task-editor-output-page"></a>Editor da Tarefa Serviço da Web (página Saída)
  Use a página **Saída** da caixa de diálogo **Editor da Tarefa Serviço da Web** para especificar onde armazenar o resultado retornado pelo método Web.  
  
### <a name="static-options"></a>Opções estáticas  
 **OutputType**  
 Selecione o tipo de armazenamento a usar para os resultados. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**File Connection**|Armazene os resultados em um arquivo. A seleção deste valor exibe a opção dinâmica **File**.|  
|**Variável**|Armazene os resultados em uma variável. A seleção deste valor exibe a opção dinâmica **Variable**.|  
  
### <a name="outputtype-dynamic-options"></a>Opções dinâmicas de OutputType  
  
#### <a name="outputtype--file-connection"></a>OutputType = File Connection  
 **File**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor do Gerenciador de conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variável**  
 Selecione uma variável na lista ou clique em \<**Nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:**  [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Vídeo, [Como chamar um serviço Web usando a tarefa Serviço da Web (vídeo do SQL Server)](https://go.microsoft.com/fwlink/?LinkId=259642), no technet.microsoft.com.  
