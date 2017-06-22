---
title: "Operação de ponto de verificação para tabelas com otimização de memória | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 04176fec3cc190cba1a89a11780d84561512431a
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>Operação de ponto de verificação para tabelas com otimização de memória
  Um ponto de verificação precisa ser executado periodicamente para dados com otimização de memória nos arquivos delta e de dados para avançar a parte ativa do log de transações. O ponto de verificação permite que as tabelas com otimização de memória sejam restauradas ou recuperadas no último ponto de verificação com êxito e, em seguida, a parte ativa do log de transações é aplicada de modo a atualizar as tabelas com otimização de memória para concluir a recuperação. A operação de ponto de verificação para tabelas baseadas em disco e tabelas com otimização de memória são operações distintas. A tabela a seguir descreve cenários diferentes e o comportamento do ponto de verificação para tabelas baseadas em disco e com otimização de memória:  
  
## <a name="manual-checkpoint"></a>Ponto de verificação manual  
 Quando você emite um ponto de verificação manual, o ponto de verificação é fechado para tabelas baseadas em disco e com otimização de memória. O arquivo de dados ativo é fechado mesmo que possa ser parcialmente preenchido.  
  
## <a name="automatic-checkpoint"></a>Ponto de verificação automático  
 O ponto de verificação automático é implementado de maneira distinta para tabelas baseadas em disco e tabelas com otimização de memória, pois os dados são mantidos de formas diferentes.  
  
 Para tabelas baseadas em disco, um ponto de verificação automático é obtido com base na opção de configuração de intervalo de recuperação (para obter mais informações, consulte [Alterar o tempo de recuperação de destino de um banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)).  
  
 Para tabelas com otimização de memória, um ponto de verificação automático é obtido quando o arquivo de log de transação se torna maior que 1,5 GB desde o último ponto de verificação. Esse tamanho de 1,5 GB inclui registros de log de transação para tabelas baseadas em disco e memória otimizada.  
  
## <a name="see-also"></a>Consulte também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
