---
title: "Removendo uma extensão de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: f16194ee794cfeacd6ba7902a42be6f970eddf1a
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="removing-a-data-processing-extension"></a>Removendo uma extensão de processamento de dados
  Para remover uma extensão de processamento de dados, basta remover o **extensão** elemento para a sua extensão de processamento de dados do arquivo de configuração. Se você criou entradas para um servidor de relatório, bem como o Designer de relatórios, remova o **extensão** elemento de arquivos de rsreportserver. config e RSReportDesigner. config. Depois que as informações de configuração forem removidas, a extensão do processamento de dados não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
