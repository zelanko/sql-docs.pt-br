---
title: Gerenciador de Conexões do SQL Server Compact Edition | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 752c825cb34fbf2afe5d2306afbd562a49f74b7f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833141"
---
# <a name="sql-server-compact-edition-connection-manager"></a>Gerenciador de Conexões do SQL Server Compact Edition
  Um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact permite que um pacote se conecte a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino do Compact [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que inclui o usa esse Gerenciador de conexões para carregar dados em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela em um banco de dados do Compact.  
  
> [!NOTE]  
>  Em um computador de 64 bits, você deve executar pacotes que se conectam a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact no modo de 32 bits. O provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa para se conectar a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, só está disponível na versão de 32 bits.  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>Configuração do gerenciador de conexões do SQL Server Compact Edition  
 Quando você adiciona um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de conexões compacta a um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , o cria um Gerenciador de conexões que será [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resolvido para uma conexão compacta em tempo de execução, define as propriedades do Gerenciador de conexões e adiciona `Connections` o Gerenciador de conexões à coleção no pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `SQLMOBILE`.  
  
 Você pode configurar um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão que especifique o local do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
-   Forneça uma senha para um banco de dados protegido por senha.  
  
-   Especifique o servidor no qual o banco de dados está armazenado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [&#40;página de conexão do editor do Gerenciador de conexões do SQL Server Compact Edition&#41;](../sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [Editor do Gerenciador de conexões do SQL Server Compact Edition &#40;página de todas as&#41;](../sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
