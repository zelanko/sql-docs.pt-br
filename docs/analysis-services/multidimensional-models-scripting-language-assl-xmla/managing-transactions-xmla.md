---
title: Gerenciando transações (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c85b1f9db4667c64bed7cf87189e48b507e5f75
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148361"
---
# <a name="managing-transactions-xmla"></a>Gerenciando transações (XMLA)
  Cada comando XML for Analysis (XMLA) enviado a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é executado dentro do contexto de uma transação na sessão implícita ou explícita atual. Para gerenciar cada uma dessas transações, você deve usar o [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla), [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla), e [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) comandos. Ao usar esses comandos, você poderá criar transações implícitas ou explícitas, alterar a contagem de referência de transação, além de iniciar, confirmar ou reverter transações.  
  
## <a name="implicit-and-explicit-transactions"></a>Transações implícitas e explícitas  
 Uma transação é implícita ou explícita:  
  
 **transação implícita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria uma *implícita* transação para um XMLA comando se o **BeginTransaction** comando não especifica o início de uma transação. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sempre confirma uma transação implícita se o comando é bem-sucedido, e reverte uma transação implícita se o comando falha.  
  
 **transação explícita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria uma *explícita* transação se a **BeginTransaction** comando inicia uma transação. No entanto, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] apenas confirma uma transação explícita se um **CommitTransaction** comando é enviado e reverterá uma transação explícita se um **RollbackTransaction** comando é enviado.  
  
 Além disso, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reverterá transações implícitas e explícitas se a sessão atual terminar antes da conclusão da transação ativa.  
  
## <a name="transactions-and-reference-counts"></a>Transações e contagens de referência  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantém uma contagem de referência de transação para cada sessão. No entanto, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não dá suporte a transações aninhadas já que somente uma transação ativa é mantida por sessão. Se a sessão atual não tiver uma transação ativa, a contagem de referência de transação será definida como zero.  
  
 Em outras palavras, cada **BeginTransaction** comando incrementa a contagem de referência em um, enquanto cada **CommitTransaction** diminui de comando em um a contagem de referência. Se um **CommitTransaction** comando define a contagem de transações como zero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] confirma a transação.  
  
 No entanto, o **RollbackTransaction** comando reverte a transação ativa, independentemente do valor atual da contagem de referência de transação. Em outras palavras, uma única **RollbackTransaction** comando reverte a transação ativa, não importa quantas **BeginTransaction** comandos ou **CommitTransaction** comandos foram enviados e define a contagem de referência de transação como zero.  
  
## <a name="beginning-a-transaction"></a>A partir de uma transação  
 O **BeginTransaction** comando inicia uma transação explícita na sessão atual e incrementa a contagem de referência de transação para a sessão atual em um. Todos os comandos subsequentes são considerados dentro da transação ativa, até que suficiente **CommitTransaction** comandos são enviados para confirmar a transação ativa ou um único **RollbackTransaction**comando é enviado para reverter a transação ativa.  
  
## <a name="committing-a-transaction"></a>Confirmando uma transação  
 O **CommitTransaction** comando confirma os resultados dos comandos executados após o **BeginTransaction** comando foi executado na sessão atual. Cada **CommitTransaction** comando diminui a contagem de referência para transações ativas em uma sessão. Se um **CommitTransaction** comando define a contagem de referência como zero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] confirma a transação ativa. Se não houver nenhuma transação ativa (em outras palavras, a contagem de referência de transação para a sessão atual já está definida como zero), uma **CommitTransaction** resulta em um erro de comando.  
  
## <a name="rolling-back-a-transaction"></a>Revertendo uma transação  
 O **RollbackTransaction** comando reverte os resultados dos comandos executados após o **BeginTransaction** comando foi executado na sessão atual. O **RollbackTransaction** comando reverte a transação ativa, independentemente da contagem de referência de transação atual e define a contagem de referência de transação como zero. Se não houver nenhuma transação ativa (em outras palavras, a contagem de referência de transação para a sessão atual já está definida como zero), uma **RollbackTransaction** resulta em um erro de comando.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
