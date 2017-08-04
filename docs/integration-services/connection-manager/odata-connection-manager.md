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
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 22374d52835c37ecf45fef20e15d563dad8e5917
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

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
  
## <a name="see-also"></a>Consulte também  
 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)  
  
  
