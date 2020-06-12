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
ms.openlocfilehash: 96afa94f7c9c20072ae88b09a436d079ce0478ae
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544985"
---
# <a name="locking-and-unlocking-databases-xmla"></a>Bloqueando e desbloqueando bancos de dados (XMLA)
  Você pode bloquear e desbloquear bancos de dados usando, respectivamente, os comandos [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) e [Unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) no XML for Analysis (XMLA). Normalmente, outros comandos do XMLA bloqueiam e desbloqueiam objetos automaticamente quando necessário para concluir o comando durante a execução. Você pode bloquear ou desbloquear explicitamente um banco de dados para executar vários comandos em uma única transação, como um comando de [lote](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) , ao mesmo tempo em que impede que outros aplicativos confirmassem uma transação de gravação no banco de dados.  
  
## <a name="locking-databases"></a>Bloqueando bancos de dados  
 O comando `Lock` bloqueia um objeto, para uso compartilhado ou exclusivo, no contexto da transação ativa no momento. Um bloqueio em um objeto impede a confirmação de transações até que o bloqueio seja removido. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]O  oferece suporte a dois tipos de bloqueios, bloqueios compartilhados e bloqueios exclusivos. Para obter mais informações sobre os tipos de bloqueio com suporte no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , consulte [elemento Mode &#40;&#41;XMLA ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla).  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite apenas o bloqueio de bancos de dados. O elemento [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) deve conter uma referência de objeto a um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados. Se o `Object` elemento não for especificado ou se o `Object` elemento se referir a um objeto que não seja um banco de dados, ocorrerá um erro.  
  
> [!IMPORTANT]  
>  Apenas administradores de banco de dados ou de servidor podem emitir um comando `Lock` explicitamente.  
  
 Outros comandos emitem um comando `Lock` implicitamente em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Qualquer operação que lê dados ou metadados de um banco de dado, como qualquer método [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) ou um método [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) que executa um comando de [instrução](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) , implicitamente emite um bloqueio compartilhado no banco de dados. Qualquer transação que confirme alterações nos dados ou metadados em um objeto em um banco de dado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , como um `Execute` método que executa um comando [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) , emite implicitamente um bloqueio exclusivo no banco de dados.  
  
## <a name="unlocking-objects"></a>Desbloqueando objetos  
 O comando `Unlock` remove um bloqueio estabelecido dentro do contexto da transação ativa no momento.  
  
> [!IMPORTANT]  
>  Somente administradores de banco de dados ou administradores de servidor podem emitir um `Unlock` comando explicitamente.  
  
 Todos os bloqueios são mantidos no contexto da transação atual. Quando a transação atual é confirmada ou revertida, todos os bloqueios definidos dentro da transação são liberados automaticamente.  
  
## <a name="see-also"></a>Consulte Também  
 [Bloquear o elemento &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Elemento Unlock &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
