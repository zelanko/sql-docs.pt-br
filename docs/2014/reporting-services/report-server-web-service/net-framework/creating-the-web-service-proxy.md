---
title: Criando o proxy do serviço Web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: b1217843-8d3d-49f3-a0d2-d35b0db5b2df
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: decf503b7da6fb4e3f3a3846a714b1062255f1a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62520369"
---
# <a name="creating-the-web-service-proxy"></a>Criando o proxy de serviço Web
  Um cliente e um serviço Web podem se comunicar usando mensagens SOAP que encapsulam os parâmetros de entrada e de saída como XML. Uma classe de proxy mapeia parâmetros para elementos XML e então envia as mensagens SOAP pela rede. Dessa forma, a classe proxy libera você de ter de se comunicar com o serviço Web no nível de SOAP e permite que você invoque métodos do serviço Web em qualquer ambiente de desenvolvimento que dê suporte a SOAP e a proxies de serviço Web.  
  
 Existem duas formas de adicionar uma classe proxy ao projeto de desenvolvimento usando o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]: com a ferramenta WSDL do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] e pela adição de uma referência Web no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. As seções a seguir discutem este assunto em mais detalhes.  
  
## <a name="adding-the-proxy-using-the-wsdl-tool"></a>Adicionando o proxy usando a ferramenta WSDL  
 O SDK do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] inclui a ferramenta Wsdl.exe (Web Services Description Language), que permite a você gerar um proxy de serviço Web para uso em um ambiente de desenvolvimento do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. A forma mais comum de criar um proxy de cliente em linguagens que dão suporte a serviços Web (atualmente, C# e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) é usar a ferramenta WSDL.  
  
 **Para adicionar uma classe proxy ao projeto usando Wsdl.exe**  
  
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
  
1.  No **Gerenciador de Soluções**, selecione o projeto que consumirá o serviço Web.  
  
2.  No menu **Projeto**, clique em **Adicionar Referência Web**.  
  
     A caixa de diálogo **Adicionar Referência Web** será aberta.  
  
3.  No campo **URL**, insira o caminho completo para o serviço Web Servidor de Relatórios.  
  
     Uma URL simplificada para o ponto de extremidade de execução de relatório do serviço Web Servidor de Relatório poderia ser assim:  
  
    ```  
    http://<Server Name>/reportserver/reportexecution2005.asmx  
    ```  
  
     A URL contém o domínio no qual o serviço Web Servidor de Relatório foi implantado, o nome da pasta que contém o serviço e o nome do arquivo de descoberta para o serviço. Para obter uma descrição completa dos diferentes elementos de URL, consulte [Acessando a API SOAP](../accessing-the-soap-api.md).  
  
     Uma descrição dos métodos e das propriedades fornecidos pelo serviço Web é exibida no painel Navegador à esquerda.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre os itens associados ao serviço Web Servidor de Relatórios, consulte [Métodos do serviço Web Servidor de Relatórios](../methods/report-server-web-service-methods.md).  
  
4.  Verifique se o seu projeto pode usar o serviço Web Servidor de Relatório e se você tem a permissão apropriada para acessar o servidor de relatório.  
  
5.  No campo **Nome da referência Web**, insira um nome que você usará no código para acessar o serviço Web Servidor de Relatórios de forma programática.  
  
6.  Selecione o botão **Adicionar Referência** para criar uma referência no aplicativo ao serviço Web.  
  
     A nova referência será exibida no **Gerenciador de Soluções**, sob o nó Referências Web do projeto ativo, nomeada como especificado no campo **Nome da referência Web**.  
  
7.  No **Gerenciador de Soluções**, expanda a pasta Referências Web para observar o namespace das classes de referência Web disponíveis para os itens do projeto.  
  
     Depois de adicionar uma referência Web ao projeto, os arquivos associados serão exibidos em uma pasta dentro da pasta Referências Web do **Gerenciador de Soluções**.  
  
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
  
 Você também pode adicionar uma diretiva **using** (**Import** no [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) à referência de serviço Web Servidor de Relatórios. Se você usar essa política, não precisará qualificar os tipos completamente no namespace. Para fazer isso, adicione o código a seguir ao seu arquivo:  
  
```vb  
Import myNamespace.myReferenceName  
```  
  
```csharp  
using myNamespace.myReferenceName;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)   
 [Criando aplicativos usando o serviço Web e o .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
