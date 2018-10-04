---
title: Salvar pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8f7b354b70f5e936a7d2953fbbcbbfbd7695114
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193426"
---
# <a name="save-packages"></a>Salvar pacotes
  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , você cria pacotes usando o Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] e salva os pacotes no sistema de arquivos como arquivos XML (arquivos .dtsx). Você também pode salvar cópias do arquivo XML de pacote no banco de dados msdb no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou no repositório de pacotes. O repositório de pacotes representa as pastas no local do sistema de arquivos que o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gerencia.  
  
 Se você salvar um pacote no sistema de arquivos, poderá depois usar o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para importar o pacote para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou para o armazenamento de pacotes. Para obter mais informações, consulte [Importar e exportar pacotes &#40;Serviço SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md).  
  
 Você também pode usar um utilitário de prompt de comando, **dtutil**, para copiar um pacote entre o sistema de arquivos e o msdb. Para obter mais informações, consulte [dtutil Utility](dtutil-utility.md).  
  
### <a name="to-save-a-package"></a>Para salvar um pacote  
  
-   [Salvar um pacote no sistema de arquivos](../../2014/integration-services/save-a-package-to-the-file-system.md)  
  
-   [Salvar uma cópia de um pacote](../../2014/integration-services/save-a-copy-of-a-package.md)  
  
  
