---
title: MSSQLSERVER_7984 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 7984 (Database Engine error)
ms.assetid: e3192f56-e4e2-41da-b132-65f1e7540b1a
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 6c8208bf310fa88e8c11fcb40cf7191458492694
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver7984"></a>MSSQLSERVER_7984
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7984|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_PRE_CHECKS_BAD_PAGE_TYPE|  
|Texto da mensagem|Verificações prévias de tabela do sistema: ID de objeto O_ID. A página P_ID tem um tipo PAGETYPE inesperado. Instrução de verificação encerrada devido a um erro irreparável.|  
  
## <a name="explanation"></a>Explicação  
Uma página com um tipo diferente de DATA_PAGE foi encontrada no nível de dados do objeto especificado. Esse erro ocorre durante a primeira fase das verificações do comando DBCC CHECKDB. Nessa fase, DBCC CHECKDB executa verificações primitivas nas páginas de dados de tabelas base do sistema que são críticas.  
  
> [!NOTE]  
> Se forem encontrados erros nas tabelas do sistema, não será possível corrigi-los; por isso, o comando DBCC CHECKDB é encerrado imediatamente.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Não aplicável. Não é possível corrigir esse erro automaticamente. Se você não conseguir restaurar o banco de dados a partir de um backup, entre em contato com o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] (CSS).  
  
