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
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: 6d9d1f0cb60af9065c1ed1e071ad250840f6ac69
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
