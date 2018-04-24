---
title: A importância da posição do Cursor | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb82081d69a03cd7ab9b7a42cf5ed7fead811657
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="the-significance-of-cursor-location"></a>A importância da posição do Cursor
Cada cursor usa recursos temporários para armazenar seus dados. Esses recursos podem ser a memória, um arquivo de paginação de disco, os arquivos de disco temporário ou armazenamento temporário até mesmo no banco de dados. O cursor é chamado um *cliente* cursor quando esses recursos estão localizados no computador cliente. O cursor é chamado um *do lado do servidor* cursor quando esses recursos estão localizados no servidor.  
  
## <a name="client-side-cursors"></a>Cursores do lado do cliente  
 No ADO, chame para um cursor do lado do cliente, usando o **adUseClient CursorLocationEnum.** Com um cursor do conjunto de chaves não do lado do cliente, o servidor envia todo conjunto de resultados pela rede para o computador cliente. O computador cliente fornece e gerencia o temporário de recursos necessários pelo conjunto de cursor e resultado. O aplicativo cliente pode procurar por meio de todo conjunto de resultados para determinar quais linhas requer.  
  
 Estáticos e controlado por cursores do lado do cliente podem colocar uma carga significativa em sua estação de trabalho se elas incluem muitas linhas. Enquanto todas as bibliotecas de cursor são capazes de criação de cursores com milhares de linhas, os aplicativos projetados para buscar esses grandes conjuntos de linhas podem insatisfatório. Há exceções, claro. Para alguns aplicativos, um grande cursor do lado do cliente pode ser perfeitamente adequado e desempenho não pode ser um problema.  
  
 Uma vantagem óbvia do cursor do lado do cliente é uma resposta rápida. Depois que o conjunto de resultados foi baixado para o computador cliente, navegar pelas linhas é muito rápido. Seu aplicativo é geralmente mais escalonável com cursores do lado do cliente, pois os requisitos de recursos do cursor são colocados em cada cliente separado e não no servidor.  
  
## <a name="server-side-cursors"></a>Cursores do lado do servidor  
 No ADO, chame para um cursor do lado do servidor, usando o **adUseServer CursorLocationEnum.** Com um cursor do lado do servidor, o servidor gerencia o conjunto de resultados usando os recursos fornecidos com o computador do servidor. O cursor do lado do servidor retorna apenas os dados solicitados pela rede. Esse tipo de cursor às vezes pode fornecer desempenho melhor do que o cursor do lado do cliente, especialmente em situações em que o tráfego excessivo na rede é um problema.  
  
 No entanto, é importante ressaltar que é um cursor do lado do servidor — pelo menos temporariamente — consuma recursos do servidor preciosos para cada cliente ativo. Você deve planejar adequadamente para garantir que o hardware de servidor é capaz de gerenciar todos os cursores do lado do servidor solicitados por clientes ativos. Além disso, um cursor do lado do servidor pode ser lento porque ele fornece acesso somente de única linha, nenhum cursor de lote está disponível.  
  
 Cursores do lado do servidor são úteis quando a inserção, atualização ou exclusão de registros. Com cursores do lado do servidor, você pode ter várias instruções ativas na mesma conexão.
