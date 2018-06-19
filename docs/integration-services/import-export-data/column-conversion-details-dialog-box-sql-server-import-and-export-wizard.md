---
title: Caixa de diálogo Detalhes da Conversão de Coluna (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5341dac153f3bd9cc90d1abe43aa4dc2f8319f78
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332170"
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>Caixa de diálogo Detalhes da Conversão de Coluna (Assistente de Importação e Exportação do SQL Server)
  Se você clicar duas vezes na linha de uma coluna individual na página **Revisar Mapeamento de Tipo de Dados** , o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará a caixa de diálogo **Detalhes de Conversão de Coluna** . Nesta página, você pode examinar as informações detalhadas de conversão de uma coluna individual. Essas informações incluem os itens a seguir.
-   Tipo de dados da coluna na origem e no destino.
-   O tipo de dados que o assistente executará, se uma conversão for necessária.
-   Os arquivos de mapeamento de tipo de dados usados pelo assistente para determinar as conversões de tipo de dados necessárias. 

## <a name="screen-shot-of-the-column-conversion-details-page"></a>Captura de tela da página Detalhes de Conversão da Coluna 
 A captura de tela a seguir mostra a caixa de diálogo **Detalhes da conversão de coluna** do Assistente depois de o usuário clicar em uma linha na página **Revisar mapeamento de tipo de dados** . Dê mais uma olhada na página **Revisar mapeamento de tipo de dados** e observe [Revisar mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).
 
Neste exemplo, você vê o que é descrito a seguir.
-   A coluna `PersonID` na tabela do SQL Server de origem é do tipo `int`. O assistente mapeia esse tipo para o tipo de dados `DT_I4` do SSIS (SQL Server Integration Services), que é um inteiro com sinal de quatro bytes, consultando o arquivo de mapeamento de tipo de dados MSSQLToSSIS10.xml.
-   A coluna `PersonID` na tabela do SQL Server de destino também é do tipo `int`. O assistente mapeia esse tipo para o mesmo tipo de dados do SSIS.
-   O assistente é concluído, *essa coluna não precisa de conversão*.
 
  
 ![Página Conversão de coluna do Assistente de Importação e Exportação](../../integration-services/import-export-data/media/column-conversion.png "Página Conversão de coluna do Assistente de Importação e Exportação") 
  
## <a name="whats-next"></a>O que vem a seguir?  
 Depois de revisar os detalhes da conversão de coluna e clicar em **OK**, a caixa de diálogo **Detalhes da conversão de coluna** retornará a página **Revisar mapeamento de tipo de dados** . Para obter mais informações, consulte [Revisar mapeamento de tipo de dados](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Confira também
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
