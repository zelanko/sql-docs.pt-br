---
title: Gerenciador de Conexões SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 32710f704e3d51d143e071178d690413735319f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833091"
---
# <a name="smo-connection-manager"></a>gerenciador de conexões SMO
  Um gerenciador de conexões SMO habilita um pacote para conexão a um servidor do SQL Management Object (SMO). As tarefas de transferência que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui utilizam um gerenciador de conexões do SMO. Por exemplo, a tarefa Transferir Logons que transfere os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um gerenciador de conexões do SMO.  
  
 Quando você adiciona um gerenciador de conexões SMO a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibilizará uma conexão do SMO no momento da execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção do `Connections` no pacote. A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `SMOServer`.  
  
 Você pode configurar um gerenciador de conexões SMO das seguintes maneiras:  
  
-   Especifique o nome de um servidor no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.  
  
-   Selecione o modo de autenticação para a conexão com o servidor.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>Configuração do gerenciador de conexões SMO  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões do SMO](../smo-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
