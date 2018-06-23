---
title: Configurando o armazenamento para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 4d13b8b46066eb6c2c8c855859fdab0114269700
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005877"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Configuração do armazenamento para tabelas com otimização de memória
  Você precisa configurar a capacidade de armazenamento e operações de entrada/saída por segundo (IOPS).  
  
## <a name="storage-capacity"></a>Capacidade de armazenamento  
 Use as informações em [Estimar requisitos de memória para tabelas com otimização de memória](memory-optimized-tables.md) para estimar o tamanho na memória das tabelas com otimização de memória duráveis do banco de dados. Como os índices não são mantidos para tabelas com otimização de memória, não incluem o tamanho dos índices. Depois de determinar o tamanho, você precisa fornecer espaço em disco que é quatro vezes o tamanho das tabelas duráveis na memória.  
  
## <a name="storage-performance"></a>Desempenho do armazenamento  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] pode aumentar significativamente a taxa de transferência da carga de trabalho. Portanto, é importante garantir que a E/A não seja um gargalo.  
  
-   Ao migrar tabelas baseadas em disco para tabelas com otimização de memória, verifique se o log de transações está em uma mídia de armazenamento compatível com atividade de log de transações aumentada. Por exemplo, se a mídia de armazenamento oferece suporte a operações de log de transações a 100 MB/s e as tabelas com otimização de memória resultam em um desempenho cinco vezes maior, a mídia de armazenamento do log de transações deve ser capaz de oferecer suporte também à melhoria de desempenho cinco vezes maior, para evitar que a atividade de log de transações se torne um gargalo de desempenho.  
  
-   Tabelas com otimização de memória persistem em arquivos distribuídos em um ou mais contêineres. Cada contêiner deve ser normalmente mapeado para seu próprio eixo e é usado para obter uma maior capacidade de armazenamento e um melhor desempenho. Você precisa garantir que o IOPS sequencial da mídia de armazenamento possa oferecer suporte 3 vezes maior em produtividade de logs de transações.  
  
     Por exemplo, se tabelas com otimização de memória gerarem 500MB/s de atividade no log de transações, o armazenamento para tabelas com otimização de memória deve suportar 1,5 GB/s. A necessidade de oferecer suporte 3 vezes aumento na produtividade do log de transações é proveniente da observação de que os pares de arquivos de dados e delta são gravados primeiro com os dados iniciais e, em seguida, precisam ser leitura/regravação como parte de uma operação de mesclagem.  
  
     Outro fator na estimativa de taxa de transferência de armazenamento é o tempo de recuperação para tabelas com otimização de memória. Dados de tabelas duráveis devem ser lidos na memória antes de um banco de dados ser disponibilizado para aplicativos. Normalmente, carregar dados em tabelas com otimização de memória pode ser feito na velocidade do IOPS. Portanto, se o armazenamento total para tabelas duráveis com otimização de memória for de 60 GB e você desejar ser capaz de carregar esses dados em 1 minuto, o IOPS do armazenamento deverá ser definido em 1 GB/s.  
  
-   Se você tiver um número par de eixos, deverá criar duas vezes o número de contêineres, cada par mapeado para o mesmo eixo. Isso é necessário para distribuir o IOPS e o armazenamento. Para obter mais informações, consulte [os arquivos de otimização de memória](the-memory-optimized-filegroup.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  