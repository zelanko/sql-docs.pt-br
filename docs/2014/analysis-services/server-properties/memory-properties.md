---
title: Propriedades da memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- LowMemoryLimit property
- MinimumAllocatedMemory property
- MidMemoryPrice property
- MemoryHeapType property
- memory [Analysis Services]
- DefaultPagesCountToReuse property
- TotalMemoryLimit property
- SessionMemoryLimit property
- VirtualMemoryLimit property
- WaitCountIfHighMemory property
- HighMemoryPrice property
- HeapTypeForObjects property
ms.assetid: 085f5195-7b2c-411a-9813-0ff5c6066d13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a88e2c1508ec849437d90b3de7c66705299dafc1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068889"
---
# <a name="memory-properties"></a>Propriedades de memória
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades de memória do servidor listadas na tabela a seguir. Para obter orientações sobre a configuração dessas propriedades, consulte [Guia de Operações do SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
 Os valores entre 1 e 100 representam percentuais da **Memória Física Total** ou do **Espaço de Endereço Virtual**, o que for menor. Os valores acima de 100 representam limites de memória em bytes.  
  
 **Aplica-se a:** Modo de servidor multidimensional e tabular, a menos que indicado o contrário.  
  
## <a name="properties"></a>Propriedades  
 `LowMemoryLimit`  
 Uma propriedade de número de ponto flutuante da precisão dupla de 64 bits assinada que define o ponto em que o servidor está com pouca memória, expressada como percentual da memória física total. Quando este limite é atingido, a instância começa lentamente a limpar a memória de cache fechando sessões expiradas e descarregando cálculos não usados. O servidor não liberará memória debaixo deste limite. O valor padrão é 65; o que indica que o limite de memória baixo é 65% de memória física ou o espaço de endereço virtual, o que for menor.  
  
 `TotalMemoryLimit`  
 Define um limite que, quando alcançado, faz o servidor desalocar memória de maneira mais agressiva. O valor padrão de 80% de memória física ou o espaço de endereço virtual, o que for menor.  
  
 Observe que `TotalMemoryLimit` deve ser sempre menor que `HardMemoryLimit`  
  
 `HardMemoryLimit`  
 Especifica um limite de memória depois do qual a instância finaliza sessões de usuário ativas agressivamente para reduzir o uso da memória. Todas as sessões terminadas receberão um erro sobre terem sido canceladas por pressão de memória. O valor padrão, zero (0), significa que o `HardMemoryLimit` será definido como um valor entre `TotalMemoryLimit` e a memória física total do sistema; se a memória física do sistema for maior que o espaço de endereço virtual do processo, o espaço de endereço virtual será usado para calcular o `HardMemoryLimit`.  
  
 `VirtualMemoryLimit`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `VertiPaqPagingPolicy`  
 Especifica o comportamento de paginação no evento que o servidor é executa com pouca memória. Estes são os valores válidos:  
  
 Zero (**0**) desabilita a paginação. Se a memória for insuficiente, o processamento falhará com um erro de memória insuficiente. Se você desabilitar a paginação, será preciso conceder privilégios do Windows à conta de serviço. Consulte [Configurar contas de serviço &#40;Analysis Services&#41;](../instances/configure-service-accounts-analysis-services.md) para obter instruções.  
  
 **1** é o padrão. Esta propriedade habilita a paginação no disco usando o arquivo de paginação do sistema operacional (pagefile.sys).  
  
 Quando `VertiPaqPagingPolicy` é definida como 1, o processamento apresenta menor probabilidade de falhar devido às restrições de memória, pois o servidor tentará paginar para o disco usando o método especificado por você. A definição da propriedade `VertiPaqPagingPolicy` não garante que erros de memória nunca ocorrerão. Erros de falta de memória ainda podem ocorrer sob as seguintes condições:  
  
-   Não há bastante memória para todos os dicionários. Durante o processamento, o Analysis Services bloqueia os dicionários para cada coluna na memória e todos eles juntos não podem ter mais do que o valor especificado para `VertiPaqMemoryLimit`.  
  
-   Não há espaço de endereço virtual insuficiente para acomodar o processo.  
  
 Para resolver erros de falta de memória persistentes, você pode tentar reprojetar o modelo para reduzir a quantidade de dados que precisa de processamento ou pode adicionar mais memória física ao computador.  
  
 Isso se aplica apenas ao modo de servidor tabular.  
  
 `VertiPaqMemoryLimit`  
 Se é permitido chamar o disco, esta propriedade especificará o nível de consumo de memória (como um percentual de memória total) no qual a paginação começará. O padrão é 60. Se o consumo de memória for menos que 60 por cento, o servidor não paginará para o disco.  
  
 Esta propriedade depende do `VertiPaqPagingPolicyProperty`, que deve ser definido como 1 para que a paginação ocorra.  
  
 Isso se aplica apenas ao modo de servidor tabular.  
  
 `HighMemoryPrice`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MemoryHeapType`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Aplica-se a somente o modo de servidor multidimensional.  
  
 `HeapTypeForObjects`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Aplica-se a somente o modo de servidor multidimensional.  
  
 `DefaultPagesCountToReuse`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `HandleIA64AlignmentFaults`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MidMemoryPrice`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `MinimumAllocatedMemory`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `PreAllocate`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `SessionMemoryLimit`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `WaitCountIfHighMemory`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar propriedades do servidor no Analysis Services](server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
