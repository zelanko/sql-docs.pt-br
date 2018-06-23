---
title: Pesquisar texto com curingas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.wildcards
- vswildcardsbuilder
helpviewer_keywords:
- searches [SQL Server Management Studio], wildcards
- Query Editor [SQL Server Management Studio], wildcard searches
- wildcard options [SQL Server Management Studio]
ms.assetid: 449600f8-cc87-4b3f-878a-59c158a88a40
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 06d3b62a4526284a0bd88d490f49769b0c7ef1d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118623"
---
# <a name="search-text-with-wildcards"></a>Pesquisar texto com curingas
  As expressões a seguir podem substituir caracteres ou dígitos no campo **Localizar** da caixa de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **do** .  
  
#### <a name="to-search-using-wildcards"></a>Para pesquisar usando curingas  
  
1.  Para habilitar o uso de curingas no campo **Localizar** durante a Localização Rápida, **Localizar em Arquivos**, **Substituição Rápida**ou em operações **Substituir nos Arquivos** , selecione a opção **Usar** em **Opções de Pesquisa** e selecione **Curingas**.  
  
2.  O botão triangular **Lista de Referências** próximo ao campo **Localizar** torna-se disponível. Clique nesse botão para exibir uma lista dos curingas disponíveis. Quando você selecionar qualquer item da **Lista de Referências**, ele será inserido na cadeia de caracteres **Localizar** .  
  
 A tabela a seguir descreve os curingas disponíveis na **Lista de Referências**.  
  
|Expression|Sintaxe|Description|  
|----------------|------------|-----------------|  
|Qualquer caractere único|?|Corresponde a qualquer caractere único.|  
|Qualquer dígito único|#|Corresponde a qualquer dígito único. Por exemplo, 7# corresponde a números que incluem 7 seguidos por outro número, como 71, mas não 17.|  
|Caracteres fora de um conjunto|[! ]|Corresponde a qualquer caractere único que não esteja especificado no conjunto.|  
|Um ou mais caracteres|*|Corresponde a qualquer um ou mais caracteres. Por exemplo, new* corresponde a qualquer texto que inclui "new", como newfile.txt.|  
|Conjunto de caracteres|[ ]|Corresponde a qualquer um dos caracteres especificados no conjunto.|  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisar e substituir](search-and-replace.md)   
 [Pesquisar texto com expressões regulares](search-text-with-regular-expressions.md)  
  
  