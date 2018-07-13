---
title: MSSQLSERVER_7987 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 7987 (Database Engine error)
ms.assetid: 314aebf1-6cdf-488d-a274-ce967fadb57b
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: daacaa2002700ff4c51d6551ba81ef46d27f2b45
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37418175"
---
# <a name="mssqlserver7987"></a>MSSQLSERVER_7987
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7987|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_PRE_CHECKS_CHAIN_LINKAGE_MISMATCH|  
|Texto da mensagem|Verificações prévias de tabela do sistema: a ID de objeto O_ID tem incompatibilidade de vínculos de cadeia. P_ID1 ->next = P_ID2, mas P_ID2 ->prev = P_ID3. Instrução de verificação encerrada devido a um erro irreparável.|  
  
## <a name="explanation"></a>Explicação  
 A primeira fase de um DBCC CHECKDB envolve a execução de verificações primitivas nas páginas de dados das tabelas de sistema críticas. Se forem encontrados erros, não será possível corrigi-los; por isso, DBCC CHECKDB é encerrado imediatamente.  
  
 O ponteiro de próxima página da página *P_ID1* aponta para a página *P_ID2*, no entanto, o ponteiro de página anterior da página *P_ID2* aponta para a página *P_ID3*, mas não retorna para a página *P_ID1* como deveria.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
 Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
 Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
 Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
 Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
 Não aplicável. Não é possível corrigir esse erro automaticamente. Se você não conseguir restaurar o banco de dados a partir de um backup, entre em contato com o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] (CSS).  
  
  
