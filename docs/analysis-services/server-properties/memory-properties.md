---
title: Propriedades de memória | Microsoft Docs
ms.date: 10/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a080bed935a8f981376ff40dc36e19ef61a3c144
ms.sourcegitcommit: 448106b618fe243e418bbfc3daae7aee8d8553d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48264876"
---
# <a name="memory-properties"></a>Propriedades de memória
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Analysis Services pré-aloca um volume modesto de memória na inicialização para que solicitações possam ser manipuladas imediatamente. Mais memória é alocada como consulta e as cargas de trabalho de processamento aumentam. 
  
  Ao especificar definições de configuração, você pode controlar os limites nos quais a memória é liberada. Por exemplo, a configuração **HardMemoryLimit** especifica uma condição de falta de memória imposta automaticamente (por padrão, esse limite não é habilitado), em que novas solicitações são rejeitadas totalmente até que mais recursos estejam disponíveis.

Para saber mais sobre a memória máxima utilizada por instância do SQL Server Analysis Services por edição, consulte [edições e recursos com suporte do SQL Server](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits).
  
 As configurações a seguir se aplicam a servidores tabulares e multidimensionais, a menos que indicado o contrário.  
 
## <a name="default-memory-configuration"></a>Configuração de memória padrão

Sob a configuração padrão, cada instância do Analysis Services aloca uma pequena quantidade de RAM (40 MB a 50 MB) na inicialização, mesmo se a instância estiver ociosa. 

Lembre-se de que as definições de configuração são por instância. Se você estiver executando várias instâncias do Analysis Services, como uma instância tabular e multidimensional no mesmo hardware, cada instância alocará sua própria memória independentemente de outras instâncias.

A tabela a seguir descreve resumidamente as configurações de memória mais comumente usadas (com mais detalhes na seção de referência). Defina essas configurações somente se o Analysis Services estiver competindo por memória com outros aplicativos no mesmo servidor:

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
 Uma assinado 64 bits de precisão dupla de ponto flutuante propriedade de número que define o primeiro limite em que o Analysis Services começa a liberar a memória para objetos de baixa prioridade, como um cache usado raramente. Depois que a memória é alocada, o servidor não libera a memória abaixo desse limite. O valor padrão é 65; o que indica que o limite de memória baixo é 65% de memória física ou o espaço de endereço virtual, o que for menor.  
  
 **TotalMemoryLimit**  
 Define um limite que, quando alcançado, faz o servidor desalocar memória a fim de liberar espaço para outras solicitações. Quando este limite é atingido, a instância começa lentamente a limpar a memória de cache fechando sessões expiradas e descarregando cálculos não usados. O valor padrão de 80% de memória física ou o espaço de endereço virtual, o que for menor. **TotalMemoryLimit** sempre deve ser menor que **HardMemoryLimit**  
  
 **HardMemoryLimit**  
 Especifica um limite de memória depois do qual a instância finaliza sessões de usuário ativas agressivamente para reduzir o uso da memória. Todas as sessões finalizadas receberão um erro sobre o que está sendo cancelada por pressão de memória. O valor padrão, 0 (zero), significa que **HardMemoryLimit** será definido como um valor entre **TotalMemoryLimit** e a memória física total do sistema; se a memória física do sistema for maior que o espaço de endereço virtual do processo, o espaço de endereço virtual será usado para calcular **HardMemoryLimit**.  

**QueryMemoryLimit**   
Somente Azure Analysis Services. Uma propriedade avançada para controlar a quantidade de memória pode ser usado pelos resultados temporários durante uma consulta. Aplica-se somente a medidas DAX e consultas. Consultas MDX em servidores de modo Multidimensional não usam esse limite. Ele não leva em conta para alocações de memória geral usadas pela consulta. Especificado em porcentagem. O valor padrão 0 indica que nenhum limite é especificado.

 **VirtualMemoryLimit**  
  Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **VertiPaqPagingPolicy**  
  Apenas para instâncias tabulares, especifica o comportamento de paginação, caso o servidor fique com pouca memória. Estes são os valores válidos:  
  
Configuração  |Description  
---------|---------
**0**     |  (padrão para o Azure Analysis Services) Desabilita a paginação. Se a memória for insuficiente, o processamento falhará com um erro de memória insuficiente. Se você desabilitar a paginação, será preciso conceder privilégios do Windows à conta de serviço. Consulte [Configurar contas de serviço &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md) para obter instruções. 
**1**     |  (padrão para o SQL Server Analysis Services) Essa propriedade permite que a paginação no disco usando o arquivo de paginação do sistema operacional (Pagefile. sys).   
  
Quando definido como 1, o processamento apresenta menor probabilidade de falhar devido a restrições de memória, pois o servidor tentará paginar para o disco usando o método especificado por você. A definição da propriedade **VertiPaqPagingPolicy** não garante que erros de memória nunca ocorrerão. Erros de falta de memória ainda podem ocorrer sob as seguintes condições:  
  
-   Não há bastante memória para todos os dicionários. Durante o processamento, o servidor bloqueia os dicionários para cada coluna na memória, e todos eles juntos não podem ser maior que o valor especificado para **VertiPaqMemoryLimit**.  
  
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
**5** | Alocador híbrido. Esse alocador usará o LFH do Windows para \<= alocações de 16 KB e o Heap as para > alocações de 16 KB. 
**6** | Alocador TBB Intel. Disponível no Analysis Services do SQL Server 2016 SP1 (e posterior).
  
  
 **HeapTypeForObjects**  
  Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Estes são os valores válidos:
  
   Configuração | Description
--------|------------
**-1** | (padrão) Automático. O mecanismo decidirá qual delas usar.
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
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do servidor no Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
