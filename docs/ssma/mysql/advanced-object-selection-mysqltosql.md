---
title: Seleção de objeto avançada (MySQLToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061200"
---
# <a name="advanced-object-selection--mysqltosql"></a>Seleção de objetos avançada (MySQLToSQL)
A caixa de diálogo **seção de objeto avançado** permite filtrar objetos de banco de dados usando cadeias de caracteres e subcadeias no nome do objeto e, em seguida, selecionar ou desmarcar esses objetos. O SSMA executa operações de conversão e migração em objetos selecionados.  
  
Para acessar essa caixa de diálogo, clique com o botão direito do mouse em um Gerenciador de metadados e selecione **seleção avançada de objetos**.  
  
Ao abrir pela primeira vez a caixa de diálogo, clique em **Mostrar itens de subcategorias** para exibir todos os objetos que têm metadados carregados no projeto. Em seguida, você pode inserir cadeias de caracteres para filtrar os itens. Por exemplo, digite a cadeia de caracteres "Company" para mostrar todos os itens com nomes que incluem essa cadeia de caracteres.  
  
Antes de usar essa caixa de diálogo, talvez você queira forçar o SSMA a carregar todos os metadados convertendo esquemas ou salvando o projeto.  
  
## <a name="options"></a>Opções  
**Verificar todos os itens**  
Adiciona uma marca de seleção ao lado de todos os itens. Esses itens serão selecionados imediatamente no Gerenciador de metadados.  
  
**Desmarcar todos os itens**  
Remove a marca de seleção ao lado de todos os itens. Esses itens serão apagados imediatamente no Gerenciador de metadados.  
  
**Modo de exibição de lista**  
Exibe itens filtrados em uma lista.  
  
**Modo de exibição de tabela**  
Exibe itens filtrados em uma tabela.  
  
**Exibidos somente itens carregados**  
Alterna a exibição de categorias ou itens. Quando esse botão é selecionado, o SSMA mostra todos os itens que correspondem aos critérios de filtro e os que foram carregados anteriormente. Quando esse botão não é selecionado, o SSMA mostra as pastas de categoria.  
  
**Filter**  
Insira a cadeia de caracteres que você deseja usar para filtrar itens. Por exemplo, para localizar todos os itens disponíveis que contêm a cadeia de caracteres "ID" no nome do item, insira a cadeia de caracteres "ID" na caixa de **filtro** .  
  
Se os itens corresponderem aos critérios de filtro, as categorias ou os itens aparecerão à medida que você digitar a cadeia de caracteres. Para ver os itens correspondentes, recomendamos que você clique no botão **exibido somente itens carregados** .  
  
**Limpar filtro**  
Limpa a caixa de **filtro** .  
  
