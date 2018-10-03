---
title: Removendo uma extensão de processamento de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7a1ad001df3353d4f114ec5ef38af2a7fdc9f142
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200046"
---
# <a name="removing-a-data-processing-extension"></a>Removendo uma extensão de processamento de dados
  Para remover uma extensão de processamento de dados, basta remover o elemento **Extension** na extensão de processamento de dados do arquivo de configuração. Se você criou entradas para um servidor de relatório e para o Designer de Relatórios, remova o elemento **Extension** dos arquivos RSReportServer.config e RSReportDesigner.config. Depois que as informações de configuração forem removidas, a extensão do processamento de dados não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
