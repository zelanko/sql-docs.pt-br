---
title: 'Como fazer: navegar entre scripts | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.editor.howto.navigate
ms.assetid: 8664bde5-86ff-4e8b-b5a6-af003316f6ad
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 49c19d1109f6105f2f081b1f85c2f188d2c02539
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65099670"
---
# <a name="how-to-navigate-between-scripts"></a>Como fazer: Navegar entre scripts
O Editor e Transact\-SQL para desenvolvimento offline fornece duas ferramentas de navegação úteis que são familiares aos usuários do Visual Studio: ir para Definição e Localizar Todas as Referências. Por exemplo, você pode clicar com o botão direito do mouse em um nome de tabela e usar "Localizar Todas as Referências" para listar todas as referências à tabela no projeto. Você pode clicar duas vezes em um resultado da pesquisa para ir para o arquivo de código específico. Nesse arquivo, você pode clicar com o botão direito do mouse no nome da tabela novamente e escolher "Ir para Definição" para voltar para a definição da tabela.  
  
> [!WARNING]  
> O procedimento a seguir usa entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-navigate-between-scripts"></a>Para navegar entre scripts  
  
1.  Expanda a pasta **Funções** no **Gerenciador de Soluções** e clique duas vezes em **GetProductsBySupplier.sql**.  
  
2.  Clique com o botão direito do mouse em `Products` nesta linha de código e selecione **Ir para Definição**  
  
    ```  
    SELECT * from Products p  
    ```  
  
3.  Products.sql é aberto automaticamente, mostrando o local onde o tipo `Products` está definido.  
  
4.  Volte para GetProductsBySupplier.sql. Dessa vez, selecione **Localizar Todas as Referências** no menu contextual para `Products`. No painel **Localizar Resultados de Símbolos**, você verá uma lista de locais onde a tabela `Products` é referenciada. Clicar duas vezes em qualquer um dos resultados da pesquisa levará você ao local da referência.  
  
