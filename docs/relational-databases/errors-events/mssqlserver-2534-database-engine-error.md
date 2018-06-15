---
title: MSSQLSERVER_2534 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2534 (Database Engine error)
ms.assetid: 121cf99d-0722-494c-be24-3369c1a0badc
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 679070a4268378d476d55316d7c881cefa23cc17
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34322477"
---
# <a name="mssqlserver2534"></a>MSSQLSERVER_2534
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2534|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_PAGE_ALLOCATED_TO_OTHER_OBJECT|  
|Texto da mensagem|Erro de tabela: a página P_ID, cujo cabeçalho indica que está alocada na ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE), está alocada por outro objeto.|  
  
## <a name="explanation"></a>Explicação  
O cabeçalho da página contém a ID de unidade de alocação *A_ID*, mas nenhuma das páginas IAM dessa unidade de alocação alocou a página. Por isso, o cabeçalho da página contém a ID de unidade de alocação errada, e a página terá um erro de compatibilidade MSSQLServer_2533 que corresponde à ID de unidade de alocação para a qual a página está efetivamente alocada.  
  
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
REPAIR reconstruirá o índice se houver um.  
  
> [!CAUTION]  
> A execução de REPAIR para o erro de compatibilidade [MSSQLSERVER_2533](~/relational-databases/errors-events/mssqlserver-2533-database-engine-error.md) desaloca a página antes da recompilação.  
  
> [!CAUTION]  
> Essa correção pode causar perda de dados.  
  
