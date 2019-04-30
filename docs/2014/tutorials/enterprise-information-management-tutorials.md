---
title: Tutoriais de gerenciamento de informações empresariais | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8745dc80-193d-4de0-9f17-ba648ab1e81c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ee7cc12f4fde3a2e5116458034ae3d4a8cc1c13a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313848"
---
# <a name="enterprise-information-management-tutorials"></a>Tutoriais de Gerenciamento de Informações da Empresa
  Esta seção contém tutoriais para gerenciar as informações em uma empresa usando as tecnologias de EIM (Gerenciamento de Informações da Empresa) incluídas no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. O EIM (Gerenciamento de Informações da Empresa) fornece um portfólio de soluções que permitem que as organizações confiem na credibilidade e na consistência de seus dados para que possam tomar decisões comerciais críticas. O [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] tem as tecnologias a seguir que o ajudam a implementar soluções de EIM na sua empresa.  
  
-   SQL Server Integration Services (SSIS). O SSIS fornece uma plataforma sofisticada e extensível para a integração de dados de várias fontes em uma solução de extração, transformação e carregamento (ETL) abrangente que oferece suporte a fluxos de trabalho comerciais, data warehouse ou gerenciamento de dados mestres.  
  
-   SQL Server Data Quality Services (DQS). O DQS permite a limpeza, a correspondência, a padronização e o enriquecimento dos dados; portanto, é possível enviar informações confiáveis para business intelligence, data warehouse e cargas de trabalho de processamento de transações.  
  
-   SQL Server Master Data Services (MDS). O MDS fornece um hub de dados central que assegura a constante integridade das informações e consistência dos dados entre diferentes aplicativos.  
  
 [Gerenciamento de informações da empresa usando SSIS, MDS e DQS em conjunto &#91;Tutorial&#93;](../../2014/tutorials/enterprise-information-management-using-ssis-mds-and-dqs-together-[tutorial].md)  
 Neste tutorial, você aprenderá a usar o SSIS, o MDS e o DQS em conjunto para implementar um exemplo de solução de Gerenciamento de informações da empresa (EIM). Primeiro, use o DQS para criar uma base de dados de conhecimento com informações sobre os dados do fornecedor (metadados), limpar os dados em um arquivo do Excel usando a base de dados de conhecimento e faça a correspondência dos dados para identificar e remover duplicatas. Em seguida, use o Suplemento MDS para Excel a fim de carregar os dados limpos e correspondentes no MDS. Depois, automatize todo o processo usando uma solução SSIS.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de informações - Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=270871)  
  
  
