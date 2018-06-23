---
title: Removendo uma extensão de renderização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 37
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c8ad34be5d818d70b8c46d82dbf348b9d0814824
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007213"
---
# <a name="removing-a-rendering-extension"></a>Removendo uma extensão de renderização
  Para remover um [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensão de renderização, basta remover o `Extension` elemento para a sua extensão de renderização do arquivo rsreportserver. config, localizado em **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< Nome da instância > services\reportserver.** pasta. Se você criou entradas para um Designer de relatórios, bem como um servidor de relatório, remova o `Extension` elemento a partir de [RSReportDesigner Configuration File](../../report-server/rsreportdesigner-configuration-file.md) também. Após a remoção das informações de configuração, a extensão de renderização não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de configuração do Reporting Services](../../report-server/reporting-services-configuration-files.md)   
 [Implementando uma extensão de renderização](implementing-a-rendering-extension.md)   
 [Visão geral das extensões de renderização](rendering-extensions-overview.md)   
 [Implementando a interface IRenderingExtension](implementing-the-irenderingextension-interface.md)   
 [Considerações sobre segurança para extensões](../security-considerations-for-extensions.md)   
 [Implantando uma extensão de renderização](deploying-a-rendering-extension.md)  
  
  