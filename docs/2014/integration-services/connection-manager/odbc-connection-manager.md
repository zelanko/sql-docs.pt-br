---
title: Gerenciador de Conexões ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c6c7ecd59bcf3a3ece0d61ecbb428bb39a80068f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833738"
---
# <a name="odbc-connection-manager"></a>gerenciador de conexões ODBC
  Um gerenciador de conexões ODBC permite que um pacote se conecte com vários sistemas de gerenciamento de banco de dados que usam a especificação ODBC (Conectividade Aberta de Banco de Dados).  
  
 Quando você adiciona uma conexão ODBC a um pacote e define as propriedades do Gerenciador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] conexões, o cria um Gerenciador de conexões e adiciona o `Connections` Gerenciador de conexões à coleção do pacote. No tempo de execução, o gerenciador de conexões é resolvido como uma conexão física ODBC.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `ODBC`.  
  
 Você pode configurar um gerenciador de conexões ODBC das seguintes formas:  
  
-   Forneça uma cadeia de caracteres de conexão que faça referência a um usuário ou a um nome de fonte de dados do sistema.  
  
-   Especifique o servidor a ser conectado.  
  
-   Indique se a conexão é retida no tempo de execução.  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>Configuração do gerenciador de conexões ODBC  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique em um dos seguintes tópicos:  
  
-   [Referência da interface do usuário do Gerenciador de Conexões ODBC](../odbc-connection-manager-ui-reference.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
