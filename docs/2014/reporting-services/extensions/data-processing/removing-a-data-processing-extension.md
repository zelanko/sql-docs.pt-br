---
title: Removendo uma extensão de processamento de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- deleting data processing extensions
- data processing extensions [Reporting Services], removing
- removing data processing extensions
ms.assetid: 1d89e32b-0631-44f6-8178-a57fb791d26d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9f5dfd3a6a7615fa3fd91c917bba6dbf0808f0f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63163976"
---
# <a name="removing-a-data-processing-extension"></a>Removendo uma extensão de processamento de dados
  Para remover uma extensão de processamento de dados, basta remover o elemento **Extension** na extensão de processamento de dados do arquivo de configuração. Se você criou entradas para um servidor de relatório e para o Designer de Relatórios, remova o elemento **Extension** dos arquivos RSReportServer.config e RSReportDesigner.config. Depois que as informações de configuração forem removidas, a extensão do processamento de dados não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões do Reporting Services](../reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
