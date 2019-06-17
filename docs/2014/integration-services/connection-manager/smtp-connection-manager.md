---
title: Gerenciador de conexões SMTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 948a7411c39191635245fdf0f6777538b1ef57fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833075"
---
# <a name="smtp-connection-manager"></a>Gerenciador de conexões SMTP
  Um gerenciador de conexões SMTP permite que um pacote conecte-se a um servidor SMTP. A tarefa Enviar Email incluída pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa um gerenciador de conexões SMTP.  
  
 Ao utilizar o Microsoft Exchange como servidor SMTP, você talvez precise configurar o gerenciador de conexões SMTP para utilizar a Autenticação do Windows. Os servidores Exchange podem ser configurados para não permitir conexões SMTP não autenticadas.  
  
## <a name="configuration-the-smtp-connection-manager"></a>Configuração do gerenciador de conexões SMTP  
 Quando você adiciona um gerenciador de conexões SMTP a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que será resolvido para uma conexão SMTP em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção `Connections` no pacote. A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `SMTP`.  
  
 Você pode configurar um gerenciador de conexões SMTP das seguintes maneiras:  
  
-   Fornecendo uma sequência de conexão.  
  
-   Especificando o nome de um servidor SMTP.  
  
-   Especificando o método de autenticação a ser usado.  
  
    > [!IMPORTANT]  
    >  O gerenciador de conexões SMTP dá suporte apenas para autenticação anônima e Autenticação do Windows. Ele não suporta a autenticação básica.  
  
-   Especificando se é necessário criptografar a comunicação utilizando o SSL ao enviar mensagens de email.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões de SMTP](../smtp-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
