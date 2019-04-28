---
title: Bloqueando e desbloqueando bancos de dados (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 290f1e5fe7efb876ab6c24004c7465cf109de0d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702228"
---
# <a name="locking-and-unlocking-databases-xmla"></a>Bloqueando e desbloqueando bancos de dados (XMLA)
  Você pode bloquear e desbloquear bancos de dados usando, respectivamente, o [bloqueio](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) e [Unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comandos no XML for Analysis (XMLA). Normalmente, outros comandos do XMLA bloqueiam e desbloqueiam objetos automaticamente quando necessário para concluir o comando durante a execução. Explicitamente, você pode bloquear ou desbloquear um banco de dados para executar vários comandos em uma única transação, como um [lote](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando, evitando que outros aplicativos confirmem uma transação de gravação ao banco de dados.  
  
## <a name="locking-databases"></a>Bloqueando bancos de dados  
 O comando `Lock` bloqueia um objeto, para uso compartilhado ou exclusivo, no contexto da transação ativa no momento. Um bloqueio em um objeto impede a confirmação de transações até que o bloqueio seja removido. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte a dois tipos de bloqueios, bloqueios compartilhados e bloqueios exclusivos. Para obter mais informações sobre os tipos de bloqueio com suporte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [elemento Mode &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla).  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite apenas o bloqueio de bancos de dados. O [objeto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) elemento deve conter uma referência de objeto para um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados. Se o `Object` não for especificado ou se o `Object` elemento se refere a um objeto diferente de um banco de dados, ocorrerá um erro.  
  
> [!IMPORTANT]  
>  Apenas administradores de banco de dados ou de servidor podem emitir um comando `Lock` explicitamente.  
  
 Outros comandos emitem um comando `Lock` implicitamente em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Qualquer operação que lê dados ou metadados de um banco de dados, por exemplo, qualquer [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) método ou uma [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) método executando uma [instrução](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) de comando, emite implicitamente um compartilhado bloqueio no banco de dados. Qualquer transação que confirme alterações em dados ou metadados em um objeto em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados, como um `Execute` método executando um [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) de comando, emite implicitamente um bloqueio exclusivo no banco de dados.  
  
## <a name="unlocking-objects"></a>Desbloqueando objetos  
 O comando `Unlock` remove um bloqueio estabelecido dentro do contexto da transação ativa no momento.  
  
> [!IMPORTANT]  
>  Apenas administradores de banco de dados ou servidor podem emitir explicitamente um `Unlock` comando.  
  
 Todos os bloqueios são mantidos no contexto da transação atual. Quando a transação atual é confirmada ou revertida, todos os bloqueios definidos dentro da transação são liberados automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Bloquear elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Desbloquear elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
