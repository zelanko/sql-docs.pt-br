---
title: Pesquisar documentos usando listas de resultados
description: Saiba como pesquisar e substituir um texto em todos os arquivos contidos em um projeto, uma solução ou uma pasta do sistema de arquivos. As correspondências são exibidas na janela Localizar Resultados 1, e você pode clicar duas vezes em uma correspondência para ver a linha que a contém.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], result lists
- result list searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], multiple files
- Query Editor [SQL Server Management Studio], search multiple files
ms.assetid: 275e1b6c-fbd0-4408-af77-35903f90657c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 817395eca7ed1fd5f9a0ae9f01c3059c17deffef
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036357"
---
# <a name="search-documents-using-results-lists"></a>Pesquisar documentos usando listas de resultados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Usando a caixa de diálogo **Localizar e Substituir** , você pode pesquisar e substituir texto em todos os arquivos de um projeto ou solução, ou em uma pasta do sistema de arquivos, mesmo quando eles não estiverem abertos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Correspondências de pesquisas executadas com a caixa de diálogo **Localizar e Substituir** são exibidas nas janelas Localizar Resultados 1 e Localizar Resultados 2, que permitem a exibição do texto exato da linha que contém a correspondência.  
  
### <a name="to-search-in-multiple-files"></a>Para executar pesquisas em vários arquivos  
  
1.  No menu **Editar** , aponte para **Localizar e Substituir** e depois clique em **Localizar nos Arquivos**.  
  
2.  Na caixa de texto **Localizar** , digite o texto da pesquisa.  
  
3.  Na lista **Examinar** , clique em **Todos os Documentos Abertos**, **Projeto Atual**, **Solução Inteira**ou digite um caminho de diretório.  
  
4.  Na lista **Tipos de arquivo** , selecione um dos conjuntos relacionados de extensões de arquivo ou digite as extensões dos tipos de arquivo a serem pesquisados, separados por ponto-e-vírgula. Use \*.\* para pesquisar todos os arquivos no diretório relacionados na lista suspensa **Examinar** .  
  
5.  Selecione uma opção dentre as opções restantes para melhorar a precisão da pesquisa.  
  
6.  Clique em **Localizar** para começar a pesquisa.  
  
 As correspondências da pesquisa são exibidas na janela Localizar Resultados 1 por padrão. Você pode navegar pelos resultados da pesquisa clicando duas vezes em cada entrada na janela Localizar Resultados 1. Para exibir os resultados da pesquisa em uma janela nova, selecione **Exibir em Localizar 2.**  
  
#### <a name="to-replace-across-multiple-files-or-folders"></a>Para efetuar uma substituição em vários arquivos ou pastas  
  
1.  No menu **Editar** , aponte para **Localizar e Substituir** e depois clique em **Substituir nos Arquivos**.  
  
2.  Na caixa de texto **Localizar** , digite o texto da pesquisa.  
  
3.  Na caixa **Substituir por** , digite o texto para substituir o texto de pesquisa.  
  
4.  Na lista **Examinar** , clique em **Todos os Documentos Abertos**, **Projeto Atual**, **Solução Inteira**ou digite um caminho de diretório.  
  
5.  Clique em **Substituir** para substituir a correspondência da pesquisa atual pelo texto da caixa **Substituir por** . Você pode passar para a próxima correspondência clicando em **Localizar Próximo** ou passar para o próximo arquivo clicando em **Ignorar Arquivo**.  
  
     \- ou –  
  
     Selecione **Substituir tudo** para substituir todas as correspondências pelo texto da caixa **Substituir por** . Selecione **Manter arquivos modificados abertos após Substituir Tudo** se você quiser desfazer algumas das substituições em outro momento.  
  
    > [!NOTE]  
    >  **Substituir tudo** substitui todas as correspondências da pesquisa, inclusive aquelas nos arquivos ignorados com **Ignorar Arquivo** ou **Localizar Próximo**. Você só pode usar **Desfazer** para substituições feitas em arquivos que tenham permanecido abertos depois da operação de substituição.  
  
 As informações de substituição são exibidas na janela Localizar Resultados 1 por padrão. Você pode navegar pelas substituições clicando duas vezes em cada entrada na janela Localizar Resultados 1.  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisar e substituir](./search-and-replace.md)   
 [Pesquisar documentos interativamente](./search-documents-interactively.md)   
 [Pesquisar texto com curingas](./search-text-with-wildcards.md)   
 [Pesquisar texto com expressões regulares](./search-text-with-regular-expressions.md)  
  
