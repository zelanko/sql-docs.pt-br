---
title: Bloqueando e desbloqueando bancos de dados (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dbcf03fee7b0b286a88c4c3089f42741e60dbff0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122049"
---
# <a name="locking-and-unlocking-databases-xmla"></a>Bloqueando e desbloqueando bancos de dados (XMLA)
  Você pode bloquear e desbloquear bancos de dados usando, respectivamente, o [bloqueio](../xmla/xml-elements-commands/lock-element-xmla.md) e [Unlock](../xmla/xml-elements-commands/unlock-element-xmla.md) comandos em XML for Analysis (XMLA). Normalmente, outros comandos do XMLA bloqueiam e desbloqueiam objetos automaticamente quando necessário para concluir o comando durante a execução. Explicitamente, você pode bloquear ou desbloquear um banco de dados para executar vários comandos em uma única transação, como um [lote](../xmla/xml-elements-commands/batch-element-xmla.md) comando, enquanto impede que outros aplicativos confirmem uma transação de gravação no banco de dados.  
  
## <a name="locking-databases"></a>Bloqueando bancos de dados  
 O comando `Lock` bloqueia um objeto, para uso compartilhado ou exclusivo, no contexto da transação ativa no momento. Um bloqueio em um objeto impede a confirmação de transações até que o bloqueio seja removido. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte a dois tipos de bloqueios, bloqueios compartilhados e bloqueios exclusivos. Para obter mais informações sobre os tipos de bloqueio suportados pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [elemento Mode &#40;XMLA&#41;](../xmla/xml-elements-properties/mode-element-xmla.md).  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite apenas o bloqueio de bancos de dados. O [objeto](../xmla/xml-elements-properties/object-element-xmla.md) elemento deve conter uma referência de objeto para um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados. Se o `Object` elemento não for especificado ou se o `Object` elemento se refere a um objeto diferente de um banco de dados, ocorrerá um erro.  
  
> [!IMPORTANT]  
>  Apenas administradores de banco de dados ou de servidor podem emitir um comando `Lock` explicitamente.  
  
 Outros comandos emitem um comando `Lock` implicitamente em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Qualquer operação que leia dados ou metadados de um banco de dados, como qualquer [Discover](../xmla/xml-elements-methods-discover.md) método ou um [Execute](../xmla/xml-elements-methods-execute.md) método executando um [instrução](../xmla/xml-elements-commands/statement-element-xmla.md) command, emite implicitamente um compartilhado bloqueio no banco de dados. Qualquer transação que confirme alterações em dados ou metadados para um objeto em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados, como um `Execute` método executando um [Alter](../xmla/xml-elements-commands/alter-element-xmla.md) command, emite implicitamente um bloqueio exclusivo no banco de dados.  
  
## <a name="unlocking-objects"></a>Desbloqueando objetos  
 O comando `Unlock` remove um bloqueio estabelecido dentro do contexto da transação ativa no momento.  
  
> [!IMPORTANT]  
>  Apenas administradores de banco de dados ou servidor podem emitir explicitamente um `Unlock` comando.  
  
 Todos os bloqueios são mantidos no contexto da transação atual. Quando a transação atual é confirmada ou revertida, todos os bloqueios definidos dentro da transação são liberados automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Bloquear elemento &#40;XMLA&#41;](../xmla/xml-elements-commands/lock-element-xmla.md)   
 [Elemento Unlock &#40;XMLA&#41;](../xmla/xml-elements-commands/unlock-element-xmla.md)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  