---
title: Relatório de avaliação (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: aae49bb6eb8ecf067911b2cb64017af0f3143aa0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47805064"
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
  
