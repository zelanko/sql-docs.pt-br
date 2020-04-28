---
title: O significado do local do cursor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e663ac5cdcf85fc1d050e0f066b597d29141ebfd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923899"
---
# <a name="the-significance-of-cursor-location"></a>A importância da posição do cursor
Cada cursor usa recursos temporários para manter seus dados. Esses recursos podem ser memória, um arquivo de paginação de disco, arquivos de disco temporário ou até mesmo armazenamento temporário no banco de dados. O cursor é chamado de cursor *do lado do cliente* quando esses recursos estão localizados no computador cliente. O cursor é chamado de cursor *do lado do servidor* quando esses recursos estão localizados no servidor.  
  
## <a name="client-side-cursors"></a>Cursores do lado do cliente  
 No ADO, chame um cursor do lado do cliente usando o **AdUseClient CursorLocationEnum.** Com um cursor do lado do cliente não definido pelo conjunto de chaves, o servidor envia todo o conjunto de resultados pela rede para o computador cliente. O computador cliente fornece e gerencia os recursos temporários necessários para o cursor e o conjunto de resultados. O aplicativo do lado do cliente pode navegar pelo conjunto de resultados inteiro para determinar quais linhas ele exige.  
  
 Os cursores estáticos e controlados por conjunto de chaves do cliente podem fazer uma carga significativa em sua estação de trabalho se incluírem muitas linhas. Embora todas as bibliotecas de cursores sejam capazes de criar cursores com milhares de linhas, os aplicativos criados para buscar tais conjuntos de linhas grandes podem funcionar mal. Há exceções, é claro. Para alguns aplicativos, um grande cursor do lado do cliente pode ser perfeitamente apropriado e o desempenho pode não ser um problema.  
  
 Um benefício óbvio do cursor do lado do cliente é resposta rápida. Depois que o conjunto de resultados tiver sido baixado para o computador cliente, a navegação pelas linhas será muito rápida. Seu aplicativo é geralmente mais escalonável com cursores do lado do cliente porque os requisitos de recursos do cursor são colocados em cada cliente separado e não no servidor.  
  
## <a name="server-side-cursors"></a>Cursores do lado do servidor  
 No ADO, chame um cursor do lado do servidor usando o **AdUseServer CursorLocationEnum.** Com um cursor do lado do servidor, o servidor gerencia o conjunto de resultados usando os recursos fornecidos pelo computador do servidor. O cursor do lado do servidor retorna apenas os dados solicitados pela rede. Esse tipo de cursor às vezes pode fornecer um desempenho melhor do que o cursor do lado do cliente, especialmente em situações em que o tráfego excessivo de rede é um problema.  
  
 No entanto, é importante ressaltar que um cursor do lado do servidor está, pelo menos, consumindo recursos preciosos do servidor de forma temporária para cada cliente ativo. Você deve planejar adequadamente para garantir que o hardware do servidor seja capaz de gerenciar todos os cursores do lado do servidor solicitados por clientes ativos. Além disso, um cursor do lado do servidor pode ser lento porque fornece apenas acesso de linha única-não há nenhum cursor de lote disponível.  
  
 Cursores do lado do servidor são úteis ao inserir, atualizar ou excluir registros. Com cursores do lado do servidor, você pode ter várias instruções ativas na mesma conexão.
