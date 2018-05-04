---
title: Seleção de objeto (DB2ToSQL) avançada | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
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
ms.assetid: ca098c15-c343-4d7d-a284-c2fc405eb991
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0e9d7e30c77be069474a8c32c8b4eded2235bc5f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="advanced-object-selection-db2tosql"></a>Seleção de objeto avançado (DB2ToSQL)
O **seção Avançado do objeto** caixa de diálogo lhe permite filtrar os objetos de banco de dados por meio de cadeias de caracteres e subcadeias de caracteres no nome do objeto e, em seguida, marque ou desmarque esses objetos. O SSMA executa operações de conversão e a migração em objetos selecionados.  
  
Para acessar essa caixa de diálogo, clique com botão direito em um Gerenciador de metadados e, em seguida, selecione **seleção de objeto avançado**.  
  
Quando você abre a caixa de diálogo pela primeira vez, clique em **Mostrar itens de subcategorias** para exibir todos os objetos que têm metadados carregado no projeto. Em seguida, você pode digitar cadeias de caracteres para filtrar os itens. Por exemplo, digite a cadeia de caracteres "company" Mostrar todos os itens com nomes que incluam essa cadeia de caracteres.  
  
Antes de usar essa caixa de diálogo, você talvez queira forçar SSMA para carregar todos os metadados de conversão de esquemas ou salvar o projeto.  
  
## <a name="options"></a>Opções  
**Verifique todos os itens**  
Adiciona uma marca de seleção ao lado de todos os itens. Esses itens serão selecionados imediatamente no Gerenciador de metadados.  
  
**Desmarcar todos os itens**  
Remove a marca de seleção ao lado de todos os itens. Esses itens serão apagados imediatamente no Gerenciador de metadados.  
  
**Modo de exibição de lista**  
Exibe itens em uma lista de filtrados.  
  
**Modo de exibição de tabela**  
Exibe itens em uma tabela de filtrados.  
  
**Carregadas somente itens exibidos**  
Alterna a exibição de categorias ou itens. Quando esse botão é selecionado, o SSMA mostra todos os itens que correspondem aos critérios de filtro e aqueles que foram carregados anteriormente. Quando esse botão não estiver selecionado, o SSMA mostra as pastas de categoria.  
  
**Filtro**  
Insira a cadeia de caracteres que você deseja usar para filtrar itens. Por exemplo, para localizar itens disponíveis que contêm a cadeia de caracteres "ID" no nome do item, insira a cadeia de caracteres "ID" no **filtro** caixa.  
  
Se itens correspondem aos critérios de filtro, as categorias ou itens serão exibido conforme você digita a cadeia de caracteres. Para ver os itens correspondentes, é recomendável que você clique o **exibido somente itens carregados** botão.  
  
**Limpar Filtro**  
Limpa o **filtro** caixa.  
  
