---
title: A importância da posição do Cursor | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7be2574e700e15373d57bf4132ee2c3dd955112b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228387"
---
# <a name="the-significance-of-cursor-location"></a>A importância da posição do cursor
Cada cursor usa recursos temporários para armazenar seus dados. Esses recursos podem ser um arquivo de paginação de disco, memória, arquivos temporários no disco ou armazenamento temporário até mesmo no banco de dados. O cursor é chamado de um *cliente* cursor quando esses recursos estão localizados no computador cliente. O cursor é chamado de um *servidor* cursor quando esses recursos estão localizados no servidor.  
  
## <a name="client-side-cursors"></a>Cursores do lado do cliente  
 No ADO, chame para um cursor do lado do cliente usando o **adUseClient CursorLocationEnum.** Com um cursor do lado do cliente não keyset, o servidor envia o resultado de inteiro definido pela rede para o computador cliente. O computador cliente fornece e gerencia os recursos temporários necessários para o conjunto de cursor e resultado. O aplicativo do lado do cliente pode navegar pelos todo conjunto de resultados para determinar quais linhas em que ele exige.  
  
 Estáticos e controlado por cursores do lado do cliente podem colocar uma carga significativa em sua estação de trabalho se elas incluírem muitas linhas. Embora todas as bibliotecas de cursor são capazes de criação de cursores com milhares de linhas, os aplicativos projetados para buscar esses grandes conjuntos de linhas podem insatisfatório. Há exceções, é claro. Para alguns aplicativos, um grande cursor do lado do cliente pode ser perfeitamente adequado e desempenho pode não ser um problema.  
  
 Uma vantagem óbvia do cursor do lado do cliente é uma resposta rápida. Depois que o conjunto de resultados tiver sido baixado no computador cliente, navegar pelas linhas é muito rápido. Seu aplicativo é geralmente mais escalonável com cursores do lado do cliente, porque os requisitos de recursos do cursor são colocados em cada cliente separado e não no servidor.  
  
## <a name="server-side-cursors"></a>Cursores do lado do servidor  
 No ADO, chame para um cursor do lado do servidor usando o **adUseServer CursorLocationEnum.** Com um cursor do lado do servidor, o servidor gerencia o conjunto de resultados usando os recursos fornecidos pelo computador do servidor. O cursor do lado do servidor retorna apenas os dados solicitados pela rede. Esse tipo de cursor às vezes, pode fornecer desempenho melhor do que o cursor do lado do cliente, especialmente em situações em que o tráfego excessivo na rede é um problema.  
  
 No entanto, é importante ressaltar que – pelo menos temporariamente - um cursor do lado do servidor está consumindo recursos preciosos server para cada cliente do Active Directory. Você deve planejar adequadamente para garantir que seu hardware de servidor é capaz de gerenciar todos os cursores do lado do servidor solicitados por clientes do Active Directory. Além disso, um cursor do lado do servidor pode ser lento porque ele fornece acesso somente de única linha - nenhum cursor de lote está disponível.  
  
 Cursores de servidor são úteis quando a inserção, atualização ou exclusão de registros. Com cursores do lado do servidor, você pode ter várias instruções ativas na mesma conexão.
