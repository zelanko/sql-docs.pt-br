---
title: Adicionar tabelas a uma instância CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- addTabs
ms.assetid: ad260e19-c021-4035-9311-c02fc96ceaea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 546f001ac4809a4fb8c455e37bf10f975d84dce8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771502"
---
# <a name="add-tables-to-a-cdc-instance"></a>Adicionar tabelas a uma instância CDC
  Use a caixa de diálogo Seleção de Tabela para adicionar tabelas da origem do Oracle para a instância CDC. As tabelas selecionadas são adicionadas à lista na guia **Tabelas** do editor de Propriedades.  
  
 Por padrão, nenhuma tabela está incluída na lista de tabelas nesta caixa de diálogo. Você pode marcar a caixa de seleção **(Selecionar Tudo)** ou pesquisar tabelas específicas.  
  
 **Para pesquisar tabelas específicas**  
 Insira os critérios de pesquisa da seguinte maneira e clique em **Pesquisar**:  
  
-   **Esquema**: selecione um esquema de banco de dados da lista. Somente tabelas que têm esquema serão incluídas na lista.  
  
-   **Padrão de Nome de Tabela**: insira qualquer cadeia de caracteres. Somente tabelas que incluem a cadeia de caracteres inserida serão exibidas.  
  
> [!NOTE]  
>  Você pode inserir critérios em um ou ambos os campos.  
  
-   **Exibir as 1000 primeiras tabelas correspondentes**: por padrão, esta caixa de seleção está marcada. Limita o vídeo às primeiras 1000 tabelas compatíveis. Se você desmarcar a caixa de seleção, todas as tabelas que correspondem aos critérios serão exibidas. Se houver um número grande de tabelas, poderá levar muito tempo para exibir a lista.  
  
 **Para selecionar tabelas a serem incluídas na instância CDC**  
 Clique na caixa de seleção ao lado de qualquer uma das tabelas que você quer incluir e clique em **Adicionar**. As tabelas são adicionadas à lista na página **Selecionar Tabelas e Colunas** do Assistente de Nova Instância.  
  
 Clique em **Fechar** para fechar a caixa de diálogo sem adicionar tabelas.  
  
> [!NOTE]  
>  Se você selecionar uma tabela que inclui um tipo de dados sem suporte, verá uma mensagem de erro e a tabela não será incluída.  
  
> [!NOTE]  
>  Você pode exibir a lista de tabelas no visualizador. Ao usar o visualizador, as informações serão somente leitura. O visualizador também inclui uma lista das colunas capturadas na tabela. Para obter mais informações sobre como acessar o visualizador, consulte [How to Manage a CDC Instance](manage-a-cdc-instance.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Como editar as propriedades de instância CDC](how-to-edit-the-cdc-instance-properties.md)   
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [Selecionar as tabelas Oracle para capturar alterações](select-oracle-tables-for-capturing-changes.md)  
  
  
