---
title: Configurando o armazenamento para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 93698be4738ef2a28c79581d0957f695b036c911
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62990634"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Configuração do armazenamento para tabelas com otimização de memória
  Você precisa configurar a capacidade de armazenamento e operações de entrada/saída por segundo (IOPS).  
  
## <a name="storage-capacity"></a>Capacidade de Armazenamento  
 Use as informações em [Estimar requisitos de memória para tabelas com otimização de memória](memory-optimized-tables.md) para estimar o tamanho na memória das tabelas com otimização de memória duráveis do banco de dados. Como os índices não são mantidos para tabelas com otimização de memória, não incluem o tamanho dos índices. Depois de determinar o tamanho, você precisa fornecer espaço em disco que é quatro vezes o tamanho das tabelas duráveis na memória.  
  
## <a name="storage-performance"></a>Desempenho de armazenamento  
 
  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] pode aumentar significativamente a taxa de transferência da carga de trabalho. Portanto, é importante garantir que a E/A não seja um gargalo.  
  
-   Ao migrar tabelas baseadas em disco para tabelas com otimização de memória, verifique se o log de transações está em uma mídia de armazenamento compatível com atividade de log de transações aumentada. Por exemplo, se a mídia de armazenamento oferece suporte a operações de log de transações a 100 MB/s e as tabelas com otimização de memória resultam em um desempenho cinco vezes maior, a mídia de armazenamento do log de transações deve ser capaz de oferecer suporte também à melhoria de desempenho cinco vezes maior, para evitar que a atividade de log de transações se torne um gargalo de desempenho.  
  
-   Tabelas com otimização de memória persistem em arquivos distribuídos em um ou mais contêineres. Cada contêiner deve ser normalmente mapeado para seu próprio eixo e é usado para obter uma maior capacidade de armazenamento e um melhor desempenho. Você precisa garantir que o IOPS sequencial da mídia de armazenamento possa dar suporte a um aumento de 3 vezes na taxa de transferência do log de transações.  
  
     Por exemplo, se tabelas com otimização de memória geram 500 MB/s de atividade no log de transações, o armazenamento para tabelas com otimização de memória deve oferecer suporte a 1,5 GB/s. A necessidade de dar suporte a um aumento de 3 vezes na taxa de transferência do log de transações vem da observação de que os pares de arquivos Delta e de dados são gravados primeiro com os dados iniciais e, em seguida, precisam ser lidos/regravados como parte de uma operação de mesclagem.  
  
     Outro fator na estimativa de taxa de transferência de armazenamento é o tempo de recuperação para tabelas com otimização de memória. Dados de tabelas duráveis devem ser lidos na memória antes de um banco de dados ser disponibilizado para aplicativos. Normalmente, carregar dados em tabelas com otimização de memória pode ser feito na velocidade do IOPS. Portanto, se o armazenamento total para tabelas duráveis com otimização de memória for de 60 GB e você desejar ser capaz de carregar esses dados em 1 minuto, o IOPS do armazenamento deverá ser definido em 1 GB/s.  
  
-   Se você tiver um número par de eixos, deverá criar duas vezes o número de contêineres, cada par mapeado para o mesmo eixo. Isso é necessário para distribuir o IOPS e o armazenamento. Para obter mais informações, consulte [o grupo de arquivos com otimização de memória](the-memory-optimized-filegroup.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
