---
title: Relatório de avaliação (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
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
ms.openlocfilehash: 777fab9d35118b4cffab8ed8f947a4e91cb2480d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="assessment-report-sybasetosql"></a>Relatório de avaliação (SybaseToSQL)
A janela do relatório de avaliação mostra os resultados da conversão de objetos de banco de dados para [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, e também pode ajudar a estimar a complexidade e o custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecionados objetos para converter no Gerenciador de metadados de origem, clique com botão direito **bancos de dados**e, em seguida, selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
**Estatísticas de conversão**  
Mostra as estatísticas de conversão por tipo de instrução. Esse painel fica visível apenas quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.  
  
**Objetos por categoria**  
Mostra as estatísticas de conversão por tipo de objeto. Esse painel fica visível apenas quando um objeto de grupo, como um esquema, ou um objeto sem código estiver selecionado no painel esquerdo.  
  
**Estatísticas**  
Mostra as estatísticas de conversão para o objeto selecionado. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo. Talvez você precise expandir **estatísticas** para exibir este painel.  
  
**Navegação de código-fonte**  
Mostra o código ASE para o objeto selecionado e realça o código que não foi convertido para [!INCLUDE[tsql](../../includes/tsql_md.md)]. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo.  
  
Clique no número de linha para definir ou limpar indicadores. Use os botões na parte superior do painel para navegar pelo código.  
  
**Navegação de destino**  
Mostra a conversão do resultante [!INCLUDE[tsql](../../includes/tsql_md.md)] código para o objeto selecionado e mensagens de erro de código que não foi convertido. Esse painel é visível somente quando um objeto individual com o código for selecionado no painel esquerdo.  
  
Clique no número de linha para definir ou limpar indicadores. Use os botões na parte superior do painel para navegar pelo código.  
  
**Painel mensagens**  
Mostra os erros, avisos e mensagens informativas que são geradas ao criar o relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erro**, **aviso**, ou **informações**, expanda a categoria de mensagens e, em seguida, clique em uma mensagem.  
  
