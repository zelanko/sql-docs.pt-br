---
title: Gerenciador de Conexões WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5d57a0783c8af0121169f09622b8e5bd8547d1ad
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58386014"
---
# <a name="wmi-connection-manager"></a>Gerenciador de conexões WMI
  Um gerenciador de conexões WMI permite que um pacote use o WMI (Instrumentação de Gerenciamento do Windows, Windows Management Instrumentation) para gerenciar informações em um ambiente corporativo. A tarefa Serviço Web que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usa um gerenciador de conexões WMI.  
  
 Quando você adiciona um Gerenciador de conexão do WMI a um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria uma conexão Gerenciador que resolverá uma conexão WMI no tempo de execução, define propriedades do Gerenciador da conexão e adiciona o Gerenciador de conexão para o `Connections` coleção do pacote . A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `WMI`.  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>Configuração do gerenciador de conexões WMI  
 Você pode configurar um gerenciador de conexões WMI das seguintes maneiras:  
  
-   Especifique o nome de um servidor.  
  
-   Especifique um namespace no servidor.  
  
-   Selecione o modo de autenticação para a conexão com o servidor.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte [Editor do Gerenciador de Conexões WMI](../wmi-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Serviços Web](../control-flow/web-service-task.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](integration-services-ssis-connections.md)  
  
  
