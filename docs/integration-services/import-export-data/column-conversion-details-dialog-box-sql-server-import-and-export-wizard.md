---
title: "Caixa de diálogo (Assistente de exportação e importação do SQL Server) de detalhes de conversão de coluna | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 985ba8a478999a153b3bb32649b98c3e809fc5e8
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>Caixa de diálogo Detalhes da Conversão de Coluna (Assistente de Importação e Exportação do SQL Server)
  Se você clicar duas vezes na linha de uma coluna individual na página **Revisar Mapeamento de Tipo de Dados** , o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará a caixa de diálogo **Detalhes de Conversão de Coluna** . Nesta página, você pode examinar as informações detalhadas de conversão de uma coluna individual. Essas informações incluem os itens a seguir.
-   O tipo de dados da coluna na origem e destino.
-   O tipo de dados de conversão que executará o assistente, se for necessária uma conversão.
-   Os arquivos de mapeamento de tipo de dados usados pelo assistente para determinar as conversões de tipo de dados necessárias. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>Captura de tela da página Detalhes de Conversão da Coluna 
 A captura de tela a seguir mostra a caixa de diálogo **Detalhes da conversão de coluna** do Assistente depois de o usuário clicar em uma linha na página **Revisar mapeamento de tipo de dados** . Dê mais uma olhada na página **Revisar mapeamento de tipo de dados** e observe [Revisar mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).
 
Neste exemplo, você deve ver os itens a seguir.
-   O `PersonID` coluna na tabela do SQL Server de origem é do tipo `int`. O assistente mapeia esse tipo para SQL Server Integration Services (SSIS) `DT_I4` tipo de dados, que é um inteiro assinado de quatro bytes, consultando o arquivo de mapeamento de tipo de dados MSSQLToSSIS10.xml.
-   O `PersonID` coluna na tabela do SQL Server de destino também é do tipo `int`. O assistente mapeia esse tipo para o mesmo tipo de dados do SSIS.
-   O assistente é concluído, *essa coluna não precisa de conversão*.
 
  
 ![Página do Assistente de importação e exportação de conversão de coluna](../../integration-services/import-export-data/media/column-conversion.png "página de conversão de coluna do Assistente de importação e exportação") 
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de revisar os detalhes da conversão de coluna e clicar em **OK**, a caixa de diálogo **Detalhes da conversão de coluna** retornará a página **Revisar mapeamento de tipo de dados** . Para obter mais informações, consulte [Revisar mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Consulte também
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

