---
title: Gerenciador de Conexões SMO | Microsoft Docs
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
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 85639e416be3870a52a9d44284534f080c62a1a9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292896"
---
# <a name="smo-connection-manager"></a>gerenciador de conexões SMO
  Um gerenciador de conexões SMO habilita um pacote para conexão a um servidor do SQL Management Object (SMO). As tarefas de transferência que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui utilizam um gerenciador de conexões do SMO. Por exemplo, a tarefa Transferir Logons que transfere os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um gerenciador de conexões do SMO.  
  
 Quando você adiciona um Gerenciador de conexão do SMO a um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria uma conexão Gerenciador que resolverá uma conexão do SMO em tempo de execução, define propriedades do Gerenciador da conexão e adiciona o Gerenciador de conexão para o `Connections` coleta no pacote. O `ConnectionManagerType` propriedade do Gerenciador de conexão é definida como `SMOServer`.  
  
 Você pode configurar um gerenciador de conexões SMO das seguintes maneiras:  
  
-   Especifique o nome de um servidor no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.  
  
-   Selecione o modo de autenticação para a conexão com o servidor.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>Configuração do gerenciador de conexões SMO  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões do SMO](../smo-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um Gerenciador de conexão programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte também  
 [Serviços de integração &#40;SSIS&#41; conexões](integration-services-ssis-connections.md)  
  
  
