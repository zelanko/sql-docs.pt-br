---
title: Usar a janela Propriedades no Management Studio
description: Saiba como usar a janela Propriedades para conferir informações sobre um item do SQL Server Management Studio, como a conexão, e sobre objetos de banco de dados.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing properties
- Properties window [SQL Server Management Studio]
- complex properties [SQL Server Management Studio]
ms.assetid: 903d4aca-f57c-43d9-a893-702eceaa7004
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f18cec0f6ac8754fc5826e75325c810e965b692
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480577"
---
# <a name="use-the-properties-window-in-management-studio"></a>Usar a janela Propriedades no Management Studio
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  A janela Propriedades descreve o estado de um item no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], como uma conexão ou um operador de plano de execução, e informações sobre objetos de banco de dados, como tabelas, exibições e designers.  
  
 Você pode usar a janela Propriedades para exibir as propriedades da conexão atual. Muitas propriedades são somente leitura na janela Propriedades, mas podem ser alteradas em outros lugares no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por exemplo, a propriedade Database de uma consulta é somente leitura na janela Propriedades, mas pode ser alterada na barra de ferramentas.  
  
### <a name="to-view-properties-using-the-properties-window"></a>Para exibir propriedades usando a janela Propriedades  
  
1.  Se a janela Propriedades não estiver visível, clique em **Janela de Propriedades** no menu **Exibir** ou pressione F4.  
  
2.  Defina o foco no objeto que você deseja exibir.  
  
3.  Procure uma propriedade específica na janela Propriedades.  
  
### <a name="to-view-connection-properties-of-a-query-window"></a>Para exibir propriedades de conexão de uma janela de consulta  
  
1.  Se a janela Propriedades não estiver visível, clique em **Janela de Propriedades** no menu **Exibir** ou pressione F4.  
  
2.  Na janela Propriedades, você pode ver todas as propriedades de conexão.  
  
### <a name="to-view-the-properties-of-a-showplan-operator"></a>Para exibir as propriedades de um operador de plano de execução  
  
1.  No menu **Consulta** , clique em **Incluir Plano de Execução Real**.  
  
2.  No Editor de Consultas SQL, digite e execute uma consulta.  
  
3.  Se a janela Propriedades não estiver visível, clique em **Janela de Propriedades** no menu **Exibir** ou pressione F4.  
  
4.  Na guia **Plano de execução** do Editor de Consultas SQL, clique nos ícones dos operadores para exibir informações sobre os operadores na janela Propriedades.  
  
## <a name="see-also"></a>Consulte Também  
 [Janela Propriedades &#40;Management Studio&#41;](../properties-window-management-studio.md)  
  
