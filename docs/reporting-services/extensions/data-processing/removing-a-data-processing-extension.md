---
title: Removendo uma extensão de processamento de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 01f260e3bb3be11ec878c951470e420fe6156647
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014093"
---
# <a name="removing-a-data-processing-extension"></a>Removendo uma extensão de processamento de dados
  Para remover uma extensão de processamento de dados, basta remover o elemento **Extension** na extensão de processamento de dados do arquivo de configuração. Se você criou entradas para um servidor de relatório e para o Designer de Relatórios, remova o elemento **Extension** dos arquivos RSReportServer.config e RSReportDesigner.config. Depois que as informações de configuração forem removidas, a extensão do processamento de dados não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
