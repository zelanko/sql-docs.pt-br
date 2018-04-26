---
title: Relatório de avaliação (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 903fcc1d14d7976e39603bf925595594b0b88170
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="assessment-report-accesstosql"></a>Relatório de avaliação (AccessToSQL)
A janela do relatório de avaliação mostra os resultados da conversão de objetos de banco de dados para [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, e também pode ajudar a estimar a complexidade e o custo de seus projetos de migração.  
  
Para criar um relatório de avaliação, selecionados objetos para converter o Gerenciador de metadados de origem, clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**. Também é possível exibir este relatório automaticamente após a conversão de esquemas. No entanto, o nome do relatório será o relatório de conversão. Para obter mais informações, consulte [projeto configurações (GUI) (SSMA comum)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
## <a name="options"></a>Opções  
**Painel do Explorer**  
Contém uma hierarquia de objetos no relatório de avaliação. Expanda pastas para exibir objetos individuais e subcomponentes. Quando você clica em uma categoria ou um objeto, as estatísticas de conversão para essa categoria ou objeto aparecem no painel de detalhes.  
  
**Painel de detalhes**  
Mostra a conversão de mensagens de estatísticas ou de erro e aviso para o objeto selecionado. Por exemplo, se a pasta de tabelas é selecionada, o painel de detalhes mostrará o número de chaves estrangeiras, índices, chaves primárias e tabelas que foram convertidas.  
  
**Painel mensagens**  
Mostra os erros, avisos e mensagens informativas que foram geradas quando o relatório de avaliação foi criado. As mensagens são agrupadas por número.  
  
Para exibir detalhes da mensagem, clique em **erros**, **avisos**, ou **mensagens**e, em seguida, expanda uma mensagem. O SSMA exibirá a lista de objetos que têm esse erro. Clique em um objeto para exibir todos os detalhes da conversão para o objeto.  
  
## <a name="see-also"></a>Consulte também  
[Reference(Access) de Interface do usuário](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
