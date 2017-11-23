---
title: "Gerenciador de Conexão do OData | Microsoft Docs"
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.custom: 
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: f54562b59e8c61f723c17e2812ca39cb2e95f273
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="odata-connection-manager"></a>Gerenciador de Conexões OData
 Conecte-se a uma fonte de dados OData com um Gerenciador de conexão do OData. Um componente de origem OData usa um Gerenciador de conexão do OData para se conectar a uma fonte de dados OData e consumir dados do serviço. Para obter mais informações, consulte [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Adição do Gerenciador de Conexões OData a um Pacote SSIS  
 Você pode adicionar um novo Gerenciador de conexão de OData a um pacote do SSIS de três maneiras:  
  
-   Clique no botão **Novo...** em **Editor de origem OData**  
  
-   Clique com o botão direito do mouse na pasta **Gerenciadores de Conexões** no **Gerenciador de Soluções**e clique em **Novo Gerenciador de Conexões**. Selecione **ODATA** para o **Tipo de gerenciador de conexões**.  
  
-   Clique com botão direito no **gerenciadores de Conexão** painel na parte inferior do pacote do designer e, em seguida, selecione **nova Conexão**. Selecione **ODATA** para o **Tipo de gerenciador de conexões**.  
  
## <a name="connection-manager-authentication"></a>Autenticação do gerenciador de conexões  
 O Gerenciador de conexão do OData oferece suporte a cinco modos de autenticação.  
  
-   Autenticação do Windows  
  
-   Autenticação Básica (com nome de usuário e senha)  

-   O Microsoft Dynamics AX Online (com nome de usuário e senha)
  
-   O Microsoft Dynamics ARM Online (com nome de usuário e senha)
  
-   O Microsoft Online Services (com nome de usuário e senha)  
  
Para o acesso anônimo, selecione a opção de Autenticação do Windows.  

Para se conectar ao Microsoft Dynamics AX Online ou do Microsoft Dynamics CRM online, você não pode usar o **Microsoft Online Services** opção de autenticação. Também é possível usar qualquer opção que está configurada para autenticação multifator.
  
### <a name="specifying-and-securing-credentials"></a>Especificando e protegendo credenciais  
 Se o serviço OData exigir autenticação básica, você poderá especificar um nome de usuário e uma senha no [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md). Os valores que você insere no publicador são persistidos no pacote. O valor de senha é criptografado de acordo com o nível de proteção do pacote.  
  
 Há várias maneiras de parametrizar os valores de nome de usuário e senha ou armazená-los fora do pacote. Por exemplo, você pode usar parâmetros ou definir a conexão propriedades do Gerenciador diretamente quando você executa o pacote do SQL Server Management Studio.  
  
## <a name="odata-connection-manager-properties"></a>Propriedades do gerenciador de conexões do OData  
 A lista a seguir descreve as propriedades do Gerenciador de conexão de OData.  
  
|||  
|-|-|  
|Propriedade|Description|  
|Url|URL do documento de serviço.|  
|UserName|Nome de usuário a ser usado para autenticação, se necessário.|  
|Senha|Senha a ser usada para autenticação, se necessário.|  
|ConnectionString|Inclui outras propriedades do Gerenciador de conexão.|  
  
## <a name="odata-connection-manager-editor"></a>Editor de Gerenciador de Conexões OData
  Use o **Editor do Gerenciador de Conexão de OData** caixa de diálogo para adicionar uma conexão ou editar uma conexão existente a uma fonte de dados OData.  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Nome do gerenciador de conexões.  
  
 **Local do documento de serviço**  
 URL do serviço OData. Por exemplo: http://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Autenticação**  
Selecione uma das opções a seguir:
-   **Autenticação do Windows**. Para acesso anônimo, selecione essa opção.
-   **Autenticação Básica** 
-   **Online do Microsoft Dynamics AX** do Dynamics AX Online
-   **Microsoft Dynamics CRM Online** do Dynamics CRM Online
-   **Serviços Online da Microsoft** do Microsoft Online Services

Se você selecionar uma opção diferente da autenticação do Windows, digite o **nome de usuário** e **senha**. 

Para se conectar ao Microsoft Dynamics AX Online ou do Microsoft Dynamics CRM online, você não pode usar o **Microsoft Online Services** opção de autenticação. Também é possível usar qualquer opção que está configurada para autenticação multifator.

 **Testar Conexão**  
 Clique neste botão para testar a conexão com o OData source.  

