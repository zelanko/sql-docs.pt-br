---
title: Pesquisar texto com curingas
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vswildcardsbuilder
helpviewer_keywords:
- searches [SQL Server Management Studio], wildcards
- Query Editor [SQL Server Management Studio], wildcard searches
- wildcard options [SQL Server Management Studio]
ms.assetid: 449600f8-cc87-4b3f-878a-59c158a88a40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caeda52d612f4df6672f686e06834de6fef0cc67
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75243283"
---
# <a name="search-text-with-wildcards"></a>Pesquisar texto com curingas
  As expressões a seguir podem substituir caracteres ou dígitos no campo **O que localizar** da caixa de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Localizar e Substituir**do**.  
  
#### <a name="to-search-using-wildcards"></a>Para pesquisar usando curingas  
  
1.  Para habilitar o uso de curingas no campo **Localizar** durante a Localização Rápida, **Localizar em Arquivos**, **Substituição Rápida**ou em operações **Substituir nos Arquivos** , selecione a opção **Usar** em **Opções de Pesquisa** e selecione **Curingas**.  
  
2.  O botão triangular **Lista de Referências** próximo ao campo **Localizar** torna-se disponível. Clique nesse botão para exibir uma lista dos curingas disponíveis. Quando você selecionar qualquer item da **Lista de Referências**, ele será inserido na cadeia de caracteres **Localizar** .  
  
 A tabela a seguir descreve os curingas disponíveis na **Lista de Referências**.  
  
|Expression|Sintaxe|DESCRIÇÃO|  
|----------------|------------|-----------------|  
|Qualquer caractere único|?|Corresponde a qualquer caractere único.|  
|Qualquer dígito único|#|Corresponde a qualquer dígito único. Por exemplo, 7# corresponde a números que incluem 7 seguidos por outro número, como 71, mas não 17.|  
|Caracteres fora de um conjunto|[! ]|Corresponde a qualquer caractere único que não esteja especificado no conjunto.|  
|Um ou mais caracteres|*|Corresponde a qualquer um ou mais caracteres. Por exemplo, new* corresponde a qualquer texto que inclui "new", como newfile.txt.|  
|Conjunto de caracteres|[ ]|Corresponde a qualquer um dos caracteres especificados no conjunto.|  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisar e substituir](search-and-replace.md)   
 [Pesquisar texto com expressões regulares](search-text-with-regular-expressions.md)  
