---
title: Relatório de avaliação (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 36aef5cb925aa97c27c4778fa4ee636aaa74b5e3
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "40395011"
---
# <a name="assessment-report-sybasetosql"></a>Relatório de avaliação (SybaseToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco de dados para [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, e também pode ajudar a estimar a complexidade e custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecionar objetos a ser convertido no Gerenciador de metadados de código-fonte, clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
**Estatísticas de conversão**  
Mostra as estatísticas de conversão pelo tipo de instrução. Esse painel fica visível apenas quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.  
  
**Objetos por categoria**  
Mostra as estatísticas de conversão por tipo de objeto. Esse painel fica visível apenas quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.  
  
**Estatísticas**  
Mostra as estatísticas de conversão para o objeto selecionado. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo. Talvez você precise expandir **estatísticas** para exibir esse painel.  
  
**Navegação de código-fonte**  
Mostra o código do ASE para o objeto selecionado e destaca o código que não foi convertido em [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo.  
  
Clique para definir ou limpar indicadores, os números de linha. Use os botões na parte superior do painel para navegar por meio do código.  
  
**Navegação de destino**  
Mostra a conversão do resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] código para o objeto selecionado e mensagens de erro para o código que não foi convertido. Esse painel é visível somente quando um objeto individual com o código é selecionado no painel esquerdo.  
  
Clique para definir ou limpar indicadores, os números de linha. Use os botões na parte superior do painel para navegar por meio do código.  
  
**Painel mensagens**  
Mostra os erros, avisos e mensagens de informações que são geradas ao criar o relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erro**, **aviso**, ou **informações**, expanda a categoria de mensagens e, em seguida, clique em uma mensagem.  
  
