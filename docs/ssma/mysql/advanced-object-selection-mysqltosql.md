---
title: Seleção de objeto (MySQLToSQL) avançada | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 390ef0c2-107c-4443-9495-80f35f22d168
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2e00eece4d8a3064806b401975aa299e76518f3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061200"
---
# <a name="advanced-object-selection--mysqltosql"></a>Seleção de objetos avançada (MySQLToSQL)
O **seção de objeto avançado** caixa de diálogo permite que você filtre os objetos de banco de dados usando cadeias de caracteres e subcadeias de caracteres no nome do objeto e, em seguida, selecionar ou desmarcar esses objetos. O SSMA executa operações de conversão e a migração em objetos selecionados.  
  
Para acessar essa caixa de diálogo, clique com botão direito em um Gerenciador de metadados e, em seguida, selecione **seleção de objeto avançado**.  
  
Quando você abrir a caixa de diálogo, clique em **Mostrar itens de subcategorias** para exibir todos os objetos que têm metadados carregados no projeto. Em seguida, você pode inserir cadeias de caracteres para filtrar os itens. Por exemplo, insira a cadeia de caracteres "empresa" Mostrar todos os itens com nomes que incluem essa cadeia de caracteres.  
  
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
  
**Carregado apenas itens exibidos**  
Alterna a exibição de categorias ou itens. Quando esse botão é selecionado, o SSMA mostra todos os itens que correspondem aos critérios de filtro e aqueles que foram carregados anteriormente. Quando esse botão não estiver selecionado, o SSMA mostra as pastas de categoria.  
  
**Filtrar**  
Insira a cadeia de caracteres que você deseja usar para filtrar itens. Por exemplo, para localizar os itens disponíveis que contêm a cadeia de caracteres "ID" no nome do item, digite a cadeia de caracteres "ID" no **filtro** caixa.  
  
Se itens correspondem aos critérios de filtro, as categorias ou itens serão exibida conforme você digita a cadeia de caracteres. Para ver os itens correspondentes, é recomendável que você clique o **exibido somente itens carregados** botão.  
  
**Limpar Filtro**  
Limpa a **filtro** caixa.  
  
