---
title: Gerenciador de conexões SMTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b05612ac34e4c2e7eb412d59eb9dcf5f28e99c78
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213476"
---
# <a name="smtp-connection-manager"></a>Gerenciador de conexões SMTP
  Um gerenciador de conexões SMTP permite que um pacote conecte-se a um servidor SMTP. A tarefa Enviar Email incluída pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa um gerenciador de conexões SMTP.  
  
 Ao utilizar o Microsoft Exchange como servidor SMTP, você talvez precise configurar o gerenciador de conexões SMTP para utilizar a Autenticação do Windows. Os servidores Exchange podem ser configurados para não permitir conexões SMTP não autenticadas.  
  
## <a name="configuration-the-smtp-connection-manager"></a>Configuração do gerenciador de conexões SMTP  
 Quando você adiciona um Gerenciador de conexão SMTP a um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria uma conexão Gerenciador que resolverá uma conexão SMTP em tempo de execução, define propriedades do Gerenciador da conexão e adiciona o Gerenciador de conexão para o `Connections` coleta no pacote. O `ConnectionManagerType` propriedade do Gerenciador de conexão é definida como `SMTP`.  
  
 Você pode configurar um gerenciador de conexões SMTP das seguintes maneiras:  
  
-   Fornecendo uma sequência de conexão.  
  
-   Especificando o nome de um servidor SMTP.  
  
-   Especificando o método de autenticação a ser usado.  
  
    > [!IMPORTANT]  
    >  O gerenciador de conexões SMTP dá suporte apenas para autenticação anônima e Autenticação do Windows. Ele não suporta a autenticação básica.  
  
-   Especificando se é necessário criptografar a comunicação utilizando o SSL ao enviar mensagens de email.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões de SMTP](../smtp-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um Gerenciador de conexão programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
