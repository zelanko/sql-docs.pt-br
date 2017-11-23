---
title: "Seleção de objeto (MySQLToSQL) avançada | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 390ef0c2-107c-4443-9495-80f35f22d168
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5fc817e35da894972d1af0490dc9e219eb3bdafb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="advanced-object-selection--mysqltosql"></a>Seleção de objeto avançado (MySQLToSQL)
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
  
**Filter**  
Insira a cadeia de caracteres que você deseja usar para filtrar itens. Por exemplo, para localizar itens disponíveis que contêm a cadeia de caracteres "ID" no nome do item, insira a cadeia de caracteres "ID" no **filtro** caixa.  
  
Se itens correspondem aos critérios de filtro, as categorias ou itens serão exibido conforme você digita a cadeia de caracteres. Para ver os itens correspondentes, é recomendável que você clique o **exibido somente itens carregados** botão.  
  
**Limpar Filtro**  
Limpa o **filtro** caixa.  
  
