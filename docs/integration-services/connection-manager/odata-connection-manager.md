---
title: "Gerenciador de Conexão do OData | Microsoft Docs"
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
caps.latest.revision: 9
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: b23a158bff546fd6ffb4208638c039d690379ce1
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="odata-connection-manager"></a>Gerenciador de Conexões OData
  Um gerenciador de conexões OData habilita um pacote a conectar-se a uma fonte OData. Um componente de origem OData se conecta a uma origem OData usando um gerenciador de conexões OData e consome dados do serviço. Para obter mais informações, consulte [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Adição do Gerenciador de Conexões OData a um Pacote SSIS  
 Você pode adicionar um novo Gerenciador de Conexões OData a um pacote SSIS de três maneiras:  
  
-   Clique no botão **Novo...** em **Editor de origem OData**  
  
-   Clique com o botão direito do mouse na pasta **Gerenciadores de Conexões** no **Gerenciador de Soluções**e clique em **Novo Gerenciador de Conexões**. Selecione **ODATA** para o **Tipo de gerenciador de conexões**.  
  
-   Clique com o botão direito do mouse no painel **Gerenciadores de Conexões** na parte inferior do designer de pacote e selecione **Nova Conexão…**. Selecione **ODATA** para o **Tipo de gerenciador de conexões**.  
  
## <a name="connection-manager-authentication"></a>Autenticação do gerenciador de conexões  
 O gerenciador de conexões do OData oferece suporte a cinco modos de autenticação.  
  
-   Autenticação do Windows  
  
-   Autenticação Básica (com nome de usuário e senha)  

-   O Microsoft Dynamics AX Online (com nome de usuário e senha)
  
-   O Microsoft Dynamics ARM Online (com nome de usuário e senha)
  
-   O Microsoft Online Services (com nome de usuário e senha)  
  
 Para o acesso anônimo, selecione a opção de Autenticação do Windows.  
  
### <a name="specifying-and-securing-credentials"></a>Especificando e protegendo credenciais  
 Se o serviço OData exigir autenticação básica, você poderá especificar um nome de usuário e uma senha no [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md). Os valores que você insere no publicador são persistidos no pacote. O valor de senha é criptografado de acordo com o nível de proteção do pacote.  
  
 Há várias maneiras de parametrizar os valores de nome de usuário e senha ou armazená-los fora do pacote. Por exemplo, você pode fazer isso usando parâmetros ou definindo as propriedades do gerenciador de conexões diretamente ao executar o pacote usando o SQL Server Management Studio.  
  
## <a name="odata-connection-manager-properties"></a>Propriedades do gerenciador de conexões do OData  
 A lista a seguir descreve as propriedades do Gerenciador de Conexões OData.  
  
|||  
|-|-|  
|Propriedade|Description|  
|Url|URL do documento de serviço.|  
|UserName|Nome de usuário para ser usado na autenticação básica.|  
|Senha|Senha a ser usada na autenticação básica.|  
|ConnectionString|Reflete outras propriedades do gerenciador de conexões.|  
  
## <a name="odata-connection-manager-editor"></a>Editor de Gerenciador de Conexões OData
  Use a caixa de diálogo **Editor de Gerenciador de Conexões OData** para adicionar uma conexão ou editar uma conexão existente com um OData Source.  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Nome do gerenciador de conexões.  
  
 **Local do documento de serviço**  
 URL do serviço OData. Por exemplo: http://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Autenticação**  
 Selecione **Autenticação do Windows** ou use **este nome de usuário e senha** para **autenticação básica**. Se você selecionar a segunda opção, insira o **nome de usuário** e a **senha**. 
 
 Agora existem mais três opções. Selecione **Microsoft Dynamics AX Online** para Dynamics AX Online, selecione **Microsoft Dynamics CRM Online** para Dynamics CRM Online e selecione **Microsoft Online Services** para Microsoft Online Services. Se você selecionar uma destas três opções, digite o **nome de usuário** e **senha**.
  
 **Testar Conexão**  
 Clique neste botão para testar a conexão com o OData Source.  
  
## <a name="see-also"></a>Consulte também  
 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)  
  
  
