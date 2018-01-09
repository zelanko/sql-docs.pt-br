---
title: "Propriedades de memória | Microsoft Docs"
ms.custom: 
ms.date: 11/17/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
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
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 8aa2f5f5c3e39680a9b0fe41e1b92443db4c8509
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="memory-properties"></a>Propriedades de memória
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] preallocates uma pequena quantidade de memória no início do backup para que as solicitações podem ser controladas imediatamente. Mais memória é alocada como consulta e as cargas de trabalho de processamento aumentam. 
  
  Ao especificar definições de configuração, você pode controlar os limites nos quais a memória é liberada. Por exemplo, a configuração **HardMemoryLimit** especifica uma condição de falta de memória imposta automaticamente (por padrão, esse limite não é habilitado), em que novas solicitações são rejeitadas totalmente até que mais recursos estejam disponíveis.
  
 **Aplica-se a:** modo de servidor multidimensional e de tabela, a menos que especificado o contrário.  
 
## <a name="default-memory-configuration"></a>Configuração de memória padrão

Na configuração padrão, cada instância do Analysis Services alocará um pequeno volume de RAM (40 a 50 MB) na inicialização, mesmo se a instância estiver ociosa. 

Lembre-se de que as definições de configuração são por instância. Se você estiver executando várias instâncias do Analysis Services, como uma instância tabular e multidimensional no mesmo hardware, cada instância alocará sua própria memória independentemente de outras instâncias.

A tabela a seguir descreve resumidamente as configurações de memória mais comumente usadas (com mais detalhes na seção de referência). Essas são as configurações que você deverá definir se o Analysis Services estiver competindo por memória com outros aplicativos no mesmo servidor:

Configuração | Description
--------|------------
LowMemoryLimit | Para instâncias multidimensionais, um limite inferior em que o servidor começa primeiramente a liberar a memória alocada a objetos usados com pouca frequência.
VertiPaqMemoryLimit | Para instâncias tabulares, um limite inferior em que o servidor começa primeiramente a liberar a memória alocada a objetos usados com pouca frequência.
TotalMemoryLimit | Um limite superior no qual o Analysis Services começa a liberar memória mais agressivamente para liberar espaço para solicitações em execução, bem como novas solicitações de alta prioridade. 
HardMemoryLimit | Outro limite em que o Analysis Services começa a rejeitar solicitações abertamente devido à pressão de memória. 
 
## <a name="property-reference"></a>Referência de Propriedade

As propriedades a seguir se aplicam aos modos tabulares e multidimensionais, a menos que especificado o contrário.

 Os valores entre 1 e 100 representam percentuais da **Memória Física Total** ou do **Espaço de Endereço Virtual**, o que for menor. Os valores acima de 100 representam limites de memória em bytes.
  
 **LowMemoryLimit**  
 Uma propriedade de número de ponto flutuante de precisão dupla de 64 bits assinada que define o primeiro limite em que o Analysis Services começa a liberar memória para objetos de baixa prioridade, como um cache usado com pouca frequência. Depois que a memória é alocada, o servidor não libera a memória abaixo desse limite. O valor padrão é 65; o que indica que o limite de memória baixo é 65% de memória física ou o espaço de endereço virtual, o que for menor.  
  
 **TotalMemoryLimit**  
 Define um limite que, quando alcançado, faz o servidor desalocar memória a fim de liberar espaço para outras solicitações. Quando este limite é atingido, a instância começa lentamente a limpar a memória de cache fechando sessões expiradas e descarregando cálculos não usados. O valor padrão de 80% de memória física ou o espaço de endereço virtual, o que for menor. Observe que **TotalMemoryLimit** deve ser sempre menor que **HardMemoryLimit**  
  
 **HardMemoryLimit**  
 Especifica um limite de memória depois do qual a instância finaliza sessões de usuário ativas agressivamente para reduzir o uso da memória. Todas as sessões terminadas receberão um erro sobre terem sido canceladas por pressão de memória. O valor padrão, 0 (zero), significa que **HardMemoryLimit** será definido como um valor entre **TotalMemoryLimit** e a memória física total do sistema; se a memória física do sistema for maior que o espaço de endereço virtual do processo, o espaço de endereço virtual será usado para calcular **HardMemoryLimit**.  
  
 **VirtualMemoryLimit**  
  Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **VertiPaqPagingPolicy**  
  Apenas para instâncias tabulares, especifica o comportamento de paginação, caso o servidor fique com pouca memória. Estes são os valores válidos:  
  
  

Configuração  |Description  
---------|---------
**0**     |  Desabilita a paginação. Se a memória for insuficiente, o processamento falhará com um erro de memória insuficiente. Se você desabilitar a paginação, será preciso conceder privilégios do Windows à conta de serviço. Consulte [Configurar contas de serviço &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md) para obter instruções. 
**1**     |  (padrão) Esta propriedade habilita a paginação no disco, usando o arquivo de paginação do sistema operacional (pagefile.sys).   
  
Quando definido como 1, o processamento apresenta menor probabilidade de falhar devido a restrições de memória, pois o servidor tentará paginar para o disco usando o método especificado por você. A definição da propriedade **VertiPaqPagingPolicy** não garante que erros de memória nunca ocorrerão. Erros de falta de memória ainda podem ocorrer sob as seguintes condições:  
  
-   Não há bastante memória para todos os dicionários. Durante o processamento, o Analysis Services bloqueia os dicionários para cada coluna na memória e todos eles juntos não podem ter mais do que o valor especificado para **VertiPaqMemoryLimit**.  
  
-   Não há espaço de endereço virtual insuficiente para acomodar o processo.  
  
 Para resolver erros de falta de memória persistentes, você pode tentar reprojetar o modelo para reduzir a quantidade de dados que precisa de processamento ou pode adicionar mais memória física ao computador.  
  
 **VertiPaqMemoryLimit**  
 Apenas para instâncias tabulares, se for permitido chamar o disco, esta propriedade especificará o nível de consumo de memória (como um percentual de memória total) no qual a paginação começará. O padrão é 60. Se o consumo de memória for menos que 60 por cento, o servidor não paginará para o disco. Esta propriedade depende do **VertiPaqPagingPolicyProperty**, que deve ser definido como 1 para que a paginação ocorra.  
  
 **HighMemoryPrice**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryHeapType**  
  Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Os valores válidos no SQL Server 2016 SP1 e posterior do Analysis Services são os seguintes:
  
  Configuração | Description
--------|------------
**-1** | (padrão) Automático. O mecanismo decidirá qual delas usar.
**1** | HEAP do Analysis Services.
**2** | LFH do Windows.
**5** | Alocador híbrido. Este alocador usará LFH do Windows para \<= alocações de 16 KB e o Heap como > alocações de 16 KB. 
**6** | Alocador TBB Intel. Disponível no Analysis Services do SQL Server 2016 SP1 (e posterior).
  
  
 **HeapTypeForObjects**  
  Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Estes são os valores válidos:
  
   Configuração | Description
--------|------------
**0** | Heap LFH do Windows.
**1** | Alocador de slot do Analysis Services.
**3** | Cada objeto tem seu próprio Heap do Analysis Services.

 
 **DefaultPagesCountToReuse**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **HandleIA64AlignmentFaults**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MidMemoryPrice**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MinimumAllocatedMemory**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **PreAllocate**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **SessionMemoryLimit**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **WaitCountIfHighMemory**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do servidor no Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  [Guia de Operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539)
  
