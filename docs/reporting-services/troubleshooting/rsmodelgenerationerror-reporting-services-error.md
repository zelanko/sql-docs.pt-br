---
title: "rsModelGenerationError - Erro do Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "rsModelGenerationError"
ms.assetid: 3a0ad63f-87f9-4ca1-b0c2-c85fa991634a
caps.latest.revision: 17
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 17
---
# rsModelGenerationError - Erro do Reporting Services
    
## Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|rsRenderingError|  
|Origem do evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|Erro ao gerar modelo. (rsModelGenerationError) (ReportingServicesLibrary) %1|  
  
## Explicação  
 O modelo de relatório não pôde ser gerado. No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 SP1 e versões anteriores, esse erro tem mais probabilidade de acontecer quando o objeto System.Data.DataSet não for capaz de controlar uma tabela ou relação dentro do esquema de banco de dados, como quando, por exemplo, duas chaves estrangeiras são definidas na mesma coluna em uma tabela.  
  
## Ação do usuário  
 Para determinar o motivo específico que causou essa mensagem de erro, examine os arquivos de log do servidor de relatório, localizados em \Microsoft SQL Server\\<SQL Server Instance\>\Reporting Services\LogFiles.  
  
## Somente interno  
  