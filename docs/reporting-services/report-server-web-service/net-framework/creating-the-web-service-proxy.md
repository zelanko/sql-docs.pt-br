---
title: "Criando o Proxy do serviço Web | Microsoft Docs"
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
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: b1217843-8d3d-49f3-a0d2-d35b0db5b2df
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 1c39d81ec9a1d2cd24f01b9dccfed13e8560a770
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="creating-the-web-service-proxy"></a>Criando o proxy de serviço Web
  Um cliente e um serviço Web podem se comunicar usando mensagens SOAP que encapsulam os parâmetros de entrada e de saída como XML. Uma classe de proxy mapeia parâmetros para elementos XML e então envia as mensagens SOAP pela rede. Dessa forma, a classe proxy libera você de ter de se comunicar com o serviço Web no nível de SOAP e permite que você invoque métodos do serviço Web em qualquer ambiente de desenvolvimento que dê suporte a SOAP e a proxies de serviço Web.  
  
 Há duas maneiras de adicionar uma classe proxy ao seu projeto de desenvolvimento usando o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]: com a ferramenta WSDL o [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]e adicionando uma referência Web em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. As seções a seguir discutem este assunto em mais detalhes.  
  
## <a name="adding-the-proxy-using-the-wsdl-tool"></a>Adicionando o proxy usando a ferramenta WSDL  
 O SDK do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] inclui a ferramenta Wsdl.exe (Web Services Description Language), que permite a você gerar um proxy de serviço Web para uso em um ambiente de desenvolvimento do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. A maneira mais comum para criar um proxy de cliente em idiomas que oferecem suporte a serviços Web (atualmente, c# e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) é usar a ferramenta WSDL.  
  
 **Para adicionar uma classe proxy ao seu projeto usando Wsdl.exe**  
  
1.  Em um prompt de comando, use Wsdl.exe para criar uma classe proxy, especificando (no mínimo) a URL do serviço Web Servidor de Relatório.  
  
     Por exemplo, a instrução de prompt de comando a seguir especifica uma URL para o ponto de extremidade de gerenciamento do serviço Web Servidor de Relatório:  
  
    ```  
    wsdl /language:CS /n:"Microsoft.SqlServer.ReportingServices2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     A ferramenta WSDL aceita vários argumentos de prompt de comando para gerar um proxy. O exemplo anterior especifica a linguagem C#, um namespace sugerido para ser usado no proxy (para impedir a colisão de nomes se você estiver usando mais de um ponto de extremidade de serviço Web) e gera um arquivo C# chamado ReportingService2010.cs. Se o exemplo tivesse especificado [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], teria gerado um arquivo de proxy com o nome ReportingService2010.vb. Esse arquivo é criado no diretório a partir do qual você executou o comando.  
  
2.  Compile a classe proxy em um arquivo de assembly (com a extensão .dll) e faça referência a ele em seu projeto, ou adicione a classe como um item de projeto.  
  
    > [!NOTE]  
    >  Quando você adicionar uma classe proxy manualmente ao seu projeto, terá de acrescentar uma referência a System.Web.Services.dll. Se você adicionar o proxy usando uma referência da Web em Visual Studio .NET, a referência será criada automaticamente. Para obter mais informações, consulte "Adicionando o proxy usando uma referência da Web no Visual Studio" mais adiante neste tópico.  
  
     Depois de adicionar a classe proxy como um item ao seu projeto, o arquivo associado será exibido no Gerenciador de Soluções.  
  
3.  Para chamar o serviço programaticamente, crie uma instância da classe proxy.  
  
     O exemplo de código a seguir mostra a sintaxe para a criação de uma instância da classe proxy <xref:ReportService2010.ReportingService2010> em um projeto:  
  
```vb  
Dim service As New ReportingService2010()  
```  
  
```csharp  
ReportingService2010 service = new ReportingService2010();  
  
```  
  
 Para obter mais informações sobre a ferramenta Wsdl.exe, incluindo a sua sintaxe completa, consulte "Ferramenta Web Services Description Language" na documentação do SDK do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Para obter uma explicação completa sobre proxies de serviço Web, consulte "Criando um proxy de serviço Web XML" na documentação do SDK do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="adding-the-proxy-using-a-web-reference-in-visual-studio"></a>Adicionando o proxy usando uma referência da Web no Visual Studio  
 Uma referência Web permite que um projeto consuma um ou mais serviços Web. O [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] permite que os usuários adicionem referências de serviço Web a projetos seguindo algumas etapas simples.  
  
 **Para adicionar uma referência Web a um projeto**  
  
1.  Em **Solution Explorer**, selecione o projeto que consumirá o serviço Web.  
  
2.  Sobre o **projeto** menu, clique em **adicionar referência Web**.  
  
     O **adicionar referência Web** caixa de diálogo é aberta.  
  
3.  No **URL** campo, digite o caminho completo para o serviço Web do servidor de relatório.  
  
     Uma URL simplificada para o ponto de extremidade de execução de relatório do serviço Web Servidor de Relatório poderia ser assim:  
  
    ```  
    http://<Server Name>/reportserver/reportexecution2005.asmx  
    ```  
  
     A URL contém o domínio no qual o serviço Web Servidor de Relatório foi implantado, o nome da pasta que contém o serviço e o nome do arquivo de descoberta para o serviço. Para obter uma descrição completa dos diferentes elementos de URL, consulte [acessando a API SOAP](../../../reporting-services/report-server-web-service/accessing-the-soap-api.md).  
  
     Uma descrição dos métodos e das propriedades fornecidos pelo serviço Web é exibida no painel Navegador à esquerda.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre os itens associados ao serviço Web servidor de relatório, consulte [métodos de Web do serviço do servidor de relatório](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md).  
  
4.  Verifique se o seu projeto pode usar o serviço Web Servidor de Relatório e se você tem a permissão apropriada para acessar o servidor de relatório.  
  
5.  No **nome da referência Web** campo, digite um nome que você usará em seu código para acessar o serviço Web do servidor de relatório programaticamente.  
  
6.  Selecione o **adicionar referência** botão para criar uma referência em seu aplicativo para o serviço Web.  
  
     A nova referência aparece na **Solution Explorer** sob o nó referências da Web para o projeto ativo, nomeado como especificado no **nome da referência Web** campo.  
  
7.  Em **Solution Explorer**, expanda a pasta referências da Web para observar o namespace para as classes de referência da Web que estão disponíveis para os itens em seu projeto.  
  
     Depois de adicionar uma referência Web ao seu projeto, os arquivos associados são exibidos em uma pasta dentro da pasta referências da Web de **Gerenciador de soluções**.  
  
 Depois de adicionar a referência da Web, use a sintaxe a seguir para criar uma instância da classe proxy:  
  
```vb  
Dim rs As New myNamespace.myReferenceName.ReportExecutionService()  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
myNamespace.myReferenceName.ReportExecutionService rs = new myNamespace.myReferenceName.ReportExecutionService();  
rs.Url = "http://<Server Name>/reportserver/reportexecution2005.asmx?wsdl"  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
```  
  
 Você também pode adicionar uma **usando** (**importação** em [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) diretiva para a referência de serviço Web servidor de relatório. Se você usar essa política, não precisará qualificar os tipos completamente no namespace. Para fazer isso, adicione o código a seguir ao seu arquivo:  
  
```vb  
Import myNamespace.myReferenceName  
```  
  
```csharp  
using myNamespace.myReferenceName;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Serviço Web servidor de relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referência técnica &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  

