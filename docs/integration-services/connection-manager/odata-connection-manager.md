---
title: Gerenciador de Conexões OData | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 39499e36568d64f92d3608f610d64193c93389e6
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542182"
---
# <a name="odata-connection-manager"></a>Gerenciador de conexões do OData

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 Conecte-se a uma fonte de dados OData com um gerenciador de conexões OData. Um Componente do OData Source usa um gerenciador de conexões OData para se conectar a uma fonte de dados OData e consumir dados do serviço. Para obter mais informações, consulte [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Adição do Gerenciador de Conexões OData a um Pacote SSIS  
 Você pode adicionar um novo gerenciador de conexões OData a um pacote SSIS de três maneiras:  
  
-   Clique no botão **Novo...** em **Editor de origem OData**  
  
-   Clique com o botão direito do mouse na pasta **Gerenciadores de Conexões** no **Gerenciador de Soluções**e clique em **Novo Gerenciador de Conexões**. Selecione **ODATA** para o **Tipo de gerenciador de conexões**.  
  
-   Clique com o botão direito do mouse no painel **Gerenciadores de Conexões** na parte inferior do designer de pacote e selecione **Nova Conexão**. Selecione **ODATA** para o **Tipo de gerenciador de conexões**.  
  
## <a name="connection-manager-authentication"></a>Autenticação do gerenciador de conexões  
 O gerenciador de conexões OData dá suporte a cinco modos de autenticação.  
  
-   Autenticação do Windows  
  
-   Autenticação Básica (com nome de usuário e senha)  

-   O Microsoft Dynamics AX Online (com nome de usuário e senha)
  
-   O Microsoft Dynamics ARM Online (com nome de usuário e senha)
  
-   O Microsoft Online Services (com nome de usuário e senha)  
  
Para o acesso anônimo, selecione a opção de Autenticação do Windows.  

Para se conectar ao Microsoft Dynamics AX Online ou ao Microsoft Dynamics CRM Online, você não pode usar a opção de autenticação **Microsoft Online Services**. Também não é possível usar nenhuma opção que esteja configurada para autenticação multifator. No momento, não há suporte para a autenticação moderna. 
  
### <a name="specifying-and-securing-credentials"></a>Especificando e protegendo credenciais  
 Se o serviço OData exigir autenticação básica, você poderá especificar um nome de usuário e uma senha no [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md). Os valores que você insere no publicador são persistidos no pacote. O valor de senha é criptografado de acordo com o nível de proteção do pacote.  
  
 Há várias maneiras de parametrizar os valores de nome de usuário e senha ou armazená-los fora do pacote. Por exemplo, você pode usar parâmetros ou definir as propriedades do gerenciador de conexões diretamente ao executar o pacote do SQL Server Management Studio.  
  
## <a name="odata-connection-manager-properties"></a>Propriedades do gerenciador de conexões do OData  
 A lista a seguir descreve as propriedades do gerenciador de conexões OData.  
  
|||  
|-|-|  
|Propriedade|DESCRIÇÃO|  
|Url|URL do documento de serviço.|  
|UserName|O nome de usuário a ser usado para autenticação, se necessário.|  
|Senha|A senha a ser usada para autenticação, se necessário.|  
|ConnectionString|Inclui outras propriedades do gerenciador de conexões.|  
  
## <a name="odata-connection-manager-editor"></a>Editor de Gerenciador de Conexões OData
  Use a caixa de diálogo **Editor de Gerenciador de Conexões OData** para adicionar uma conexão ou editar uma conexão existente com uma fonte de dados OData.  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Nome do gerenciador de conexões.  
  
 **Local do documento de serviço**  
 URL do serviço OData. Por exemplo: https://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Autenticação**  
Selecione uma das seguintes opções:
-   **Autenticação do Windows**. Para acesso anônimo, selecione essa opção.
-   **Autenticação básica** 
-   **Microsoft Dynamics AX Online** para Dynamics AX Online
-   **Microsoft Dynamics CRM Online** para Dynamics CRM Online
-   **Microsoft Online Services** para Microsoft Online Services

Se você selecionar uma opção diferente da Autenticação do Windows, digite o **nome de usuário** e **senha**. 

Para se conectar ao Microsoft Dynamics AX Online ou ao Microsoft Dynamics CRM Online, você não pode usar a opção de autenticação **Microsoft Online Services**. Também não é possível usar nenhuma opção que esteja configurada para autenticação multifator.

 **Testar Conexão**  
 Clique neste botão para testar a conexão com o OData Source.  
