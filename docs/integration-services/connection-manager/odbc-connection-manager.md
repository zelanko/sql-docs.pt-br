---
title: Gerenciador de Conexões ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.odbcconnection.f1
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2b362f60e2fb38ce9a9eda476dd4b1077055da18
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914157"
---
# <a name="odbc-connection-manager"></a>gerenciador de conexões ODBC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um gerenciador de conexões ODBC permite que um pacote se conecte com vários sistemas de gerenciamento de banco de dados que usam a especificação ODBC (Conectividade Aberta de Banco de Dados).  
  
 Quando você adiciona um gerenciador de conexões ODBC a um pacote e define as propriedades do gerenciador de conexões, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões e adiciona o gerenciador de conexões à coleção **Connections** do pacote. No tempo de execução, o gerenciador de conexões é resolvido como uma conexão física ODBC.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **ODBC**.  
  
 Você pode configurar um gerenciador de conexões ODBC das seguintes formas:  
  
-   Forneça uma cadeia de caracteres de conexão que faça referência a um usuário ou a um nome de fonte de dados do sistema.  
  
-   Especifique o servidor a ser conectado.  
  
-   Indique se a conexão é retida no tempo de execução.  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>Configuração do gerenciador de conexões ODBC  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique em um dos seguintes tópicos:  
  
-   [Referência da interface do usuário do Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="odbc-connection-manager-ui-reference"></a>Referência da interface do usuário do Gerenciador de Conexões ODBC
  Use a caixa de diálogo **Configurar Gerenciador de Conexões ODBC** para adicionar uma conexão com uma fonte de dados ODBC.  
  
 Para saber mais sobre o gerenciador de conexões ODBC, consulte [Gerenciador de conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Conexões de dados**  
 Selecione um gerenciador de conexões ODBC existente na lista.  
  
 **Propriedades de conexão de dados**  
 Exiba propriedades e valores para o gerenciador de conexões ODBC selecionado.  
  
 **Novo**  
 Crie um gerenciador de conexões ODBC utilizando a caixa de diálogo **Gerenciador de Conexões** . Essa caixa de diálogo permite que você crie uma nova fonte de dados ODBC, caso necessário.  
  
 **Delete (excluir)**  
 Selecione uma conexão e exclua-a usando o botão **Excluir** .  
## <a name="see-also"></a>Consulte Também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
