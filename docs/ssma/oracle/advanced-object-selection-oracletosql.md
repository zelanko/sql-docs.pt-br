---
title: "Seleção de objeto (OracleToSQL) avançada | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c978fba4-c953-4ed0-a21d-1b38e7225552
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: v-pelars
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 350b223034355afa675d0a18300028841edeee71
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="advanced-object-selection--oracletosql"></a>Seleção de objeto avançado (OracleToSQL)
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
  

