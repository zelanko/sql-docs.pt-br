---
title: MSSQLSERVER_2577 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2577 (Database Engine error)
ms.assetid: f53256a2-2fb0-47fd-9ed9-c45389104145
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1244598f5e9b836eb3d3aefa1bd13011d527bfdc
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2577"></a>MSSQLSERVER_2577
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2577|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_IAM_CHAIN_SEQUENCE_OUT_OF_ORDER|  
|Texto da mensagem|Os números de sequência de cadeia estão fora de ordem na cadeia de página IAM para a ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE). A página P_ID1 com número de sequência SEQUENCE1 aponta para a página P_ID2 com número de sequência SEQUENCE2.|  
  
## <a name="explanation"></a>Explicação  
Toda página IAM tem um número de sequência. O número de sequência é a posição da página IAM na cadeia IAM. A regra é que os números de sequência aumentam em um para cada página IAM. A página IAM, *P_ID2*, tem um número de sequência que não segue essa regra.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Se não houver um backup limpo, execute DBCC CHECKDB sem uma cláusula REPAIR para determinar a extensão do dano. DBCC CHECKDB recomendará uma cláusula REPAIR para ser usada. Execute DBCC CHECKDB com a cláusula REPAIR apropriada para reparar o dano.  
  
> [!CAUTION]  
> Se você não tiver certeza do efeito de DBCC CHECKDB com uma cláusula REPAIR sobre seus dados, contate o provedor de suporte antes de executar essa instrução.  
  
Se a execução de DBCC CHECKDB com uma das cláusulas REPAIR não corrigir o problema, contate seu provedor de suporte.  
  
### <a name="results-of-running-repair-options"></a>Resultados da execução de opções REPAIR  
A execução de REPAIR reconstruirá a cadeia IAM. Primeiro, a cláusula REPAIR divide a cadeia IAM existente em duas metades. A primeira metade da cadeia terminará com uma página IAM, *P_ID1*. O próximo ponteiro da página *P_ID1* será definido como (0:0). A segunda metade da cadeia iniciará com a página IAM, *P_ID2*. O ponteiro anterior da página *P_ID2* será definido como (0:0).  
  
Em seguida, a cláusula REPAIR conectará as duas metades da cadeia para gerar novamente os números de sequência da cadeia IAM. Nenhuma página IAM que não puder ser corrigida será desalocada.  
  
> [!CAUTION]  
> Essa correção pode causar perda de dados.  
  

