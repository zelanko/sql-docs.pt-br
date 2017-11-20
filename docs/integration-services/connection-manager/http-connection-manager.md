---
title: "Gerenciador de Conexão HTTP | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.httpconnection.server.f1
- sql13.dts.designer.httpconnection.proxy.f1
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 7dbd165b8d94247365697fe3b9e0cbb372becd8c
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="http-connection-manager"></a>Gerenciador de conexões HTTP
  Uma conexão HTTP permite que um pacote acesse um servidor Web usando o HTTP para enviar ou receber arquivos. A tarefa Serviço da Web incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa esse gerenciador de conexões.  
  
 Quando você adiciona um gerenciador de conexões HTTP a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que será resolvido para uma conexão HTTP em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** no pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **HTTP.**  
  
 Você pode configurar um gerenciador de conexões HTTP das seguintes maneiras:  
  
-   Use credenciais. Se o gerenciador de conexões HTTP usar credenciais, suas propriedades incluirão o nome de usuário, a senha e o domínio.  
  
    > [!IMPORTANT]  
    >  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
-   Use um certificado do cliente. Se o gerenciador de conexões usar um certificado do cliente, suas propriedades incluirão o nome de certificado.  
  
-   Forneça um tempo limite para conexão com o servidor e um tamanho da parte para gravar dados.  
  
-   Use um servidor proxy. O servidor proxy também pode ser configurado para usar credenciais e ignorar o servidor proxy com o uso de endereços locais em seu lugar.  
  
## <a name="configuration-of-the-http-connection-manager"></a>Configuração do gerenciador de conexões HTTP  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre como configurar um gerenciador de conexões de forma programática, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## <a name="http-connection-manager-editor-server-page"></a>Editor do Gerenciador de Conexões HTTP (página Servidor)
  Use a guia **Servidor** da caixa de diálogo **Editor do Gerenciador de Conexões de HTTP** para configurar o Gerenciador de Conexões de HTTP especificando propriedades como URL e credenciais de segurança. Uma conexão HTTP permite que um pacote acesse um servidor Web usando o HTTP para enviar ou receber arquivos. Depois de configurar o Gerenciador de Conexões de HTTP, você também pode testar a conexão.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões HTTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 Para obter mais informações sobre o gerenciador de conexões de HTTP, consulte [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Para saber mais sobre um cenário de utilização geral para o Gerenciador de Conexões de HTTP, consulte [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
### <a name="options"></a>Opções  
 **Servidor URL**  
 Digite o URL do servidor.  
  
 Para usar o botão **Baixar WSDL** na página **Geral** do **Editor da Tarefa Serviço da Web** para baixar um arquivo WSDL, digite a URL do arquivo WSDL. Essa URL termina com "?wsdl".  
  
 **Usar credenciais**  
 Especifique se você o Gerenciador de Conexões de HTTP deve usar as credenciais de segurança do usuário para autenticação.  
  
 **Nome de usuário**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Senha**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Domínio**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Usar certificado do cliente**  
 Especifique se o Gerenciador de Conexões de HTTP deve usar um certificado do cliente para autenticação.  
  
 **Certificado**  
 Selecione um certificado na lista usando a caixa de diálogo **Selecionar Certificado** . A caixa de texto exibe o nome associado a este certificado.  
  
 **Tempo limite (em segundos)**  
 Forneça um tempo limite para conexão com o servidor Web. O valor padrão desta propriedade é 30 segundos.  
  
 **Tamanho da parte (em KB)**  
 Forneça um tamanho da parte para gravar dados.  
  
 **Testar Conexão**  
 Depois de configurar o Gerenciador de Conexões de HTTP, confirme se a conexão é viável clicando em **Testar Conexão**.  
  
## <a name="http-connection-manager-editor-proxy-page"></a>Editor do Gerenciador de Conexões de HTTP (Página Proxy)
  Use a guia **Proxy** da caixa de diálogo **Editor do Gerenciador de Conexões de HTTP** para configurar o Gerenciador de Conexões de HTTP para usar um servidor proxy. Uma conexão HTTP permite que um pacote acesse um servidor Web usando o HTTP para enviar ou receber arquivos.  
  
 Para obter mais informações sobre o gerenciador de conexões de HTTP, consulte [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Para saber mais sobre um cenário de utilização geral para o Gerenciador de Conexões de HTTP, consulte [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
### <a name="options"></a>Opções  
 **Usar proxy**  
 Especifique se você quer que o Gerenciador de Conexões de HTTP conecte por de um servidor proxy.  
  
 **URL do Proxy**  
 Digite a URL para o servidor proxy.  
  
 **Ignorar proxy no local**  
 Especifique se você quer que o Gerenciador de Conexões de HTTP ignore o servidor proxy para endereços locais.  
  
 **Usar credenciais**  
 Especifique se você quer que o Gerenciador de Conexões de HTTP use credenciais de segurança para o servidor proxy.  
  
 **Nome de usuário**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Senha**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Domínio**  
 Se o Gerenciador de Conexões de HTTP usar credenciais, será necessário especificar um nome de usuário, senha e domínio.  
  
 **Lista proxies ignoráveis**  
 A lista de endereços para os quais você quer ignorar o servidor proxy.  
  
 **Adicionar**  
 Digite um endereço para o qual você quer ignorar o servidor proxy.  
  
 **Remover**  
 Selecione um endereço e remova-o clicando em **Remover**.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Serviços Web](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40; SSIS &#41; Conexões](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  

