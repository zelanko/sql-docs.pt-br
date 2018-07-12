---
title: rsModelGenerationError – Erro do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 09183b8aa2af3257d10e3e9929d3d7457da787ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228796"
---
# <a name="rsmodelgenerationerror---reporting-services-error"></a>rsModelGenerationError - Erro do Reporting Services
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|rsRenderingError|  
|Origem do evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|Erro ao gerar modelo. (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## <a name="explanation"></a>Explicação  
 O modelo de relatório não pôde ser gerado. No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 e versões anteriores, esse erro tem mais probabilidade de acontecer quando o objeto System.Data.DataSet não for capaz de controlar uma tabela ou relação dentro do esquema de banco de dados, como quando, por exemplo, duas chaves estrangeiras são definidas na mesma coluna em uma tabela.  
  
## <a name="user-action"></a>Ação do usuário  
 Para determinar o motivo específico que causou essa mensagem de erro, examine os arquivos de log do servidor de relatório, localizados em \Microsoft SQL Server\\<SQL Server Instance\>\Reporting Services\LogFiles.  
  
## <a name="internal-only"></a>Somente interno  
  
