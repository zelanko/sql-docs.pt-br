---
title: Como corrigir erros | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0d504e00-4ff0-4fdf-b874-85280bbd8668
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f4984e28ae3397b6296f8d1a39a6d32474b27f9c
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093639"
---
# <a name="how-to-fix-errors"></a>Como: Corrigir erros
O painel Lista de Erros exibe os erros de implantação ou compilação. Os erros de sintaxe e semântica causados ao editar no Editor de Transact\-SQL ou no Designer de Tabela também são exibidos na lista quando você estiver editando entidades de bancos de dados e suas definições. A Lista de Erros é atualizada dinamicamente conforme você edita scripts em guias diferentes. Você pode seguir os erros identificados para solucionar problemas no futuro.  
  
> [!WARNING]  
> Os procedimentos a seguir usam entidades criadas em procedimentos nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-fix-errors"></a>Para corrigir erros  
  
1.  Clique com o botão direito do mouse na tabela **Produto** (Product.sql) no **Gerenciador de Soluções** e selecione **Designer de Exibição**.  
  
2.  Na Grade de Colunas do designer, clique com o botão direito do mouse na coluna **ShelflLife** e selecione **Excluir** para excluir esta coluna da tabela.  
  
3.  Observe que, no painel **Lista de Erros**, na parte inferior da tela, um aviso e um erro semelhante ao seguinte aparece imediatamente.  
  
**Aviso SQL71502: Função: [dbo]. [GetProductsBySupplier] contém uma referência não resolvida a um objeto. Ou o objeto não existe ou a referência é ambígua porque pode se referir a qualquer um dos objetos seguintes: [dbo].[Product].[p]::[ShelfLife] ou [dbo].[Product].[ShelfLife].Erro SQL71501: Restrição de verificação: [dbo].[CK_Product_ShelfLife] tem uma referência não resolvida para o objeto [dbo].[Product].[ShelfLife].**  
  
4.  Você pode clicar com o botão direito do mouse na **Lista de Erros** e pode usar os menus contextuais para classificar resultados, filtrar quais entradas você deseja exibir, e quais colunas de informações você deseja que apareça para cada entrada.  
  
    Clique duas vezes no primeiro aviso identificado e siga-o para o arquivo de script que gerou o aviso. A seção de código problemática é realçada. No exemplo, isso ocorre porque a coluna `ShelfLife` está sendo usada por uma instrução `RETURN` e por uma instrução `SELECT` em uma função com valor de tabela criada anteriormente.  
  
5.  No Editor de Transact\-SQL, remova `ShelfLife` da função.  
  
6.  Corrija o segundo erro de uma maneira semelhante removendo a restrição de verificação.  
  
7.  Observe que o aviso e o erro desaparecem imediatamente da **Lista de Erros** depois que você corrige os problemas.  
  
## <a name="see-also"></a>Consulte Também  
[Usar o Editor Transact-SQL para editar e executar scripts](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
