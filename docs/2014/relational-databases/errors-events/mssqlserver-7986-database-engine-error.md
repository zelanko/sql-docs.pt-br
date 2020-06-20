---
title: MSSQLSERVER_7986 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7986 (Database Engine error)
ms.assetid: ae64276c-4e1e-4ef3-9ee9-ebeb2f61e565
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 05577850e65e7bb180aebf2d535d7d59e3fb1986
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85032023"
---
# <a name="mssqlserver_7986"></a>MSSQLSERVER_7986
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|7986|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_PRE_CHECKS_CROSS_OBJECT_LINKAGE|  
|Texto da mensagem|Verificações prévias de tabela do sistema: a ID de objeto O_ID tem vínculos de cadeia entre objetos. A página P_ID1 aponta para P_ID2 na ID de unidade de alocação A_ID1 (deve ser A_ID2). Instrução de verificação encerrada devido a erro irreparável.|  
  
## <a name="explanation"></a>Explicação  
 A primeira fase de um DBCC CHECKDB envolve a execução de verificações primitivas nas páginas de dados das tabelas de sistema críticas. Se forem encontrados erros, não será possível corrigi-los; por isso, DBCC CHECKDB é encerrado imediatamente. O ponteiro de próxima página da página *P_ID1* no nível de dados do objeto especificado aponta para uma página, a *P_ID2*, em um objeto diferente.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
 Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
 Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
 Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
 Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
 Não aplicável. Não é possível corrigir esse erro automaticamente. Se você não conseguir restaurar o banco de dados com base em um backup, contate o CSS (Suporte e Atendimento ao Cliente) [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
  
