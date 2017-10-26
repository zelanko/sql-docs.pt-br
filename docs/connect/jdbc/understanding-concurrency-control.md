---
title: "Noções básicas sobre o controle de simultaneidade | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 52c954cb3acc87753f9ede5a0fc786bd9ed9b755
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-concurrency-control"></a>Entendendo controle de simultaneidade
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O controle de simultaneidade refere-se às várias técnicas que são usadas para preservar a integridade dos bancos de dados quando vários usuários estão atualizando linhas ao mesmo tempo. A simultaneidade incorreta pode conduzir a problemas como leituras sujas, leituras de fantasma e leituras não repetíveis. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece interfaces a todas as técnicas de simultaneidade usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para resolver esses problemas.  
  
> [!NOTE]  
>  Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] simultaneidade, consulte "Gerenciando o acesso simultâneo a dados" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
## <a name="remarks"></a>Comentários  
 O driver JDBC oferece suporte aos seguintes tipos de simultaneidade:  
  
|Tipo de simultaneidade|Características|Bloqueios de linha|Description|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|Somente Leitura|Não|Não são permitidas atualizações pelo cursor e não é mantido nenhum bloqueio nas linhas que compõem o conjunto de resultados.|  
|CONCUR_UPDATABLE|Gravação de leitura otimista|Não|O banco de dados assumir contenção de linha é improvável, mas possível. A integridade de linha é verificada com uma comparação de carimbo de data e hora.|  
|CONCUR_SS_SCROLL_LOCKS|Gravação de leitura pessimista|Sim|O banco de dados assumir contenção de linha é provável. A integridade de linha é assegurada com bloqueio de linha.|  
|CONCUR_SS_OPTIMISTIC_CC|Gravação de leitura otimista|Não|O banco de dados assumir contenção de linha é improvável, mas possível. A integridade da linha é verificada com uma comparação de carimbo de data/hora.<br /><br /> Para [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] e posterior, o servidor alterará esse tipo para CONCUR_SS_OPTIMISTIC_CCVAL se a tabela não contém uma coluna de carimbo de hora.<br /><br /> Para [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], se a tabela subjacente tiver uma coluna de carimbo de hora, OPTIMISTIC WITH ROW VERSIONING será usado mesmo se OPTIMISTIC WITH VALUES for especificado. Se OPTIMISTIC WITH ROW VERSIONING for especificado e a tabela não tiver carimbos de data e hora, OPTIMISTIC WITH VALUES será usado.|  
|CONCUR_SS_OPTIMISTIC_CCVAL|Gravação de leitura otimista|Não|O banco de dados assumir contenção de linha é improvável, mas possível. A integridade de linha é verificada com uma comparação de dados da linha.|  
  
## <a name="result-sets-that-are-not-updateable"></a>Conjuntos de resultados que não são atualizáveis  
 Um conjunto de resultados atualizável é um conjunto de resultados no qual linhas podem ser inseridas, atualizadas e excluídas. Nos casos a seguir, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] não é possível criar um cursor atualizável. A exceção gerada é "O conjunto de resultados não é atualizável".  
  
|Causa|Description|Recurso|  
|-----------|-----------------|------------|  
|A instrução não é criada usando a sintaxe do JDBC 2.0 (ou posterior)|O JDBC 2.0 introduziu novos métodos para criar instruções. Se a sintaxe do JDBC 1.0 for usada, o conjunto de resultados seguirá o padrão somente leitura.|Especifique o tipo de conjunto de resultados e simultaneidade ao criar a instrução.|  
|A instrução é criada usando TYPE_SCROLL_INSENSITIVE|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]cria um cursor de instantâneo estático. Ele é desconectado das linhas de tabela subjacentes para ajudar a proteger o cursor de atualizações de linha feitas por outros usuários.|Use TYPE_SCROLL_SENSITIVE, TYPE_SS_SCROLL_KEYSET, TYPE_SS_SCROLL_DYNAMIC ou TYPE_FORWARD_ONLY com CONCUR_UPDATABLE para evitar criar um cursor estático.|  
|O design de tabela impede um cursor KEYSET ou DYNAMIC|A tabela subjacente não tem chave exclusiva para permitir [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para identificar exclusivamente uma linha.|Acrescente chaves exclusivas à tabela para fornecer identificação exclusiva de cada linha.|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando conjuntos de resultados com o JDBC Driver](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  

