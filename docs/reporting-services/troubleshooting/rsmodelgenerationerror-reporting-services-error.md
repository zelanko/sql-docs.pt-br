---
title: rsModelGenerationError – Erro do Reporting Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsModelGenerationError
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9a8c2dc17bbb6599acbb363d7d8f8b9c51bc061a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707674"
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
  
