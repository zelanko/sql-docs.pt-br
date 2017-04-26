---
title: MSSQLSERVER_2576 | Microsoft Docs
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
- 2576 (Database Engine error)
ms.assetid: b727cc2f-c76c-46f8-bbbe-5e7a05a6eabf
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b96de1b2a8056f4b88ba6df9259607e0d94aa427
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver2576"></a>MSSQLSERVER_2576
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2576|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_IAM_PARENT_PAGE_WAS_NOT_SEEN|  
|Texto da mensagem|A página IAM P_ID1 é apontada pelo ponteiro anterior da página IAM P_ID2 na ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE), mas não foi detectada na varredura.|  
  
## <a name="explanation"></a>Explicação  
Uma página IAM ou entrada de metadados não foi localizada, ainda que exista uma referência à página como o link de página anterior em outra página IAM de uma cadeia IAM. Se a página *P_ID1* for (0:0), a página IAM, *P_ID2*, corresponderá ao início de uma cadeia IAM e a entrada de metadados da cadeia IAM estará ausente.  
  
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
REPAIR tentará recompilar a cadeia IAM que envolve a página *P_ID2*. A reconstrução da cadeia pode envolver a remoção de páginas ou a remoção da cadeia inteira caso os metadados estejam corrompidos.  
  
> [!CAUTION]  
> Essa correção pode causar perda de dados.  
  

