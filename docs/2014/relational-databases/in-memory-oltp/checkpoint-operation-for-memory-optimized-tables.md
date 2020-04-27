---
title: Operação de ponto de verificação para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ddcdec0f624c1d6f70c57e593eaf9da66cbe0419
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63065524"
---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>Operação de ponto de verificação para tabelas com otimização de memória
  Um ponto de verificação precisa ser executado periodicamente para dados com otimização de memória nos arquivos delta e de dados para avançar a parte ativa do log de transações. O ponto de verificação permite que as tabelas com otimização de memória sejam restauradas ou recuperadas no último ponto de verificação com êxito e, em seguida, a parte ativa do log de transações é aplicada de modo a atualizar as tabelas com otimização de memória para concluir a recuperação. A operação de ponto de verificação para tabelas baseadas em disco e tabelas com otimização de memória são operações distintas. A tabela a seguir descreve cenários diferentes e o comportamento do ponto de verificação para tabelas baseadas em disco e com otimização de memória:  
  
## <a name="manual-checkpoint"></a>Ponto de verificação manual  
 Quando você emite um ponto de verificação manual, o ponto de verificação é fechado para tabelas baseadas em disco e com otimização de memória. O arquivo de dados ativo é fechado mesmo que possa ser parcialmente preenchido.  
  
## <a name="automatic-checkpoint"></a>Ponto de verificação automático  
 O ponto de verificação automático é implementado de maneira distinta para tabelas baseadas em disco e tabelas com otimização de memória, pois os dados são mantidos de formas diferentes.  
  
 Para tabelas baseadas em disco, um ponto de verificação automático é obtido com base na opção de configuração de intervalo de recuperação (para obter mais informações, consulte [Alterar o tempo de recuperação de destino de um banco de dados &#40;SQL Server&#41;](../logs/change-the-target-recovery-time-of-a-database-sql-server.md)).  
  
 Para tabelas com otimização de memória, um ponto de verificação automático é obtido quando o arquivo de log de transações se torna maior que 512 MB desde o último ponto de verificação. 512 MB inclui registros de log de transações para tabelas baseadas em disco e com otimização de memória.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
