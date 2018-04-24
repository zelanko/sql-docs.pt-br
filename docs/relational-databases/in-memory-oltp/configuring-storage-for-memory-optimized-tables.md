---
title: Configurando o armazenamento para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 10/25/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c33ef5aa3bfa5598ed306af4836d7d8f36f53233
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Configuração do armazenamento para tabelas com otimização de memória
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você precisa configurar a capacidade de armazenamento e operações de entrada/saída por segundo (IOPS).  
  
## <a name="storage-capacity"></a>Capacidade de armazenamento  
 Use as informações em [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) para estimar o tamanho na memória das tabelas com otimização de memória duráveis do banco de dados. Como os índices não são mantidos para tabelas com otimização de memória, não incluem o tamanho dos índices. Depois de determinar o tamanho, você precisa fornecer espaço em disco que é quatro vezes o tamanho das tabelas duráveis na memória.  
  
## <a name="storage-iops"></a>IOPS de armazenamento  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] pode aumentar significativamente a taxa de transferência da carga de trabalho. Portanto, é importante garantir que a E/A não seja um gargalo.  
  
-   Ao migrar tabelas baseadas em disco para tabelas com otimização de memória, verifique se o log de transações está em uma mídia de armazenamento compatível com atividade de log de transações aumentada. Por exemplo, se a mídia de armazenamento oferece suporte a operações de log de transações a 100 MB/s e as tabelas com otimização de memória resultam em um desempenho cinco vezes maior, a mídia de armazenamento do log de transações deve ser capaz de oferecer suporte também à melhoria de desempenho cinco vezes maior, para evitar que a atividade de log de transações se torne um gargalo de desempenho.  
  
-   Tabelas com otimização de memória são persistidas em arquivos de ponto de verificação, que são distribuídos em um ou mais contêineres. Cada contêiner normalmente deve ser mapeado para seu próprio dispositivo de armazenamento e é usado para uma maior capacidade de armazenamento e um melhor IOPS. Você precisa garantir que o IOPS sequencial da mídia de armazenamento pode dar suporte a até 3 vezes mais a taxa de transferência do log de transações. As gravações em arquivos de ponto de verificação são 256 KB para arquivos de dados e 4 KB para arquivos delta.
  
     - Por exemplo, se tabelas com otimização de memória gerarem 500 MB/s sustentados de atividade no log de transações, o armazenamento das tabelas com otimização de memória deverá dar suporte para um IOPS de 1,5 GB/s. A necessidade de dar suporte a três vezes a taxa de transferência sustentada do log de transações surge da observação de que os pares de arquivos de dados e delta são gravados primeiro com os dados iniciais e, em seguida, precisam ser lidos/regravados como parte de uma operação de mesclagem.  
  
- Outro fator na estimativa de IOPS para armazenamento é o tempo de recuperação para tabelas com otimização de memória. Dados de tabelas duráveis devem ser lidos na memória antes de um banco de dados ser disponibilizado para aplicativos. Normalmente, carregar dados em tabelas com otimização de memória pode ser feito na velocidade do IOPS. Portanto, se o armazenamento total para tabelas duráveis com otimização de memória for de 60 GB e você desejar ser capaz de carregar esses dados em 1 minuto, o IOPS do armazenamento deverá ser definido em 1 GB/s.  
  
-   Arquivos de ponto de verificação normalmente são distribuídos uniformemente em todos os contêineres, se houver espaço. Com o SQL Server 2014, você precisa provisionar um número ímpar de contêineres para alcançar uma distribuição uniforme – a partir do 2016, números ímpar e par de contêineres levam a uma distribuição uniforme.
  
## <a name="encryption"></a>Criptografia  
 No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o armazenamento de tabelas com otimização de memória será criptografado como parte da habilitação de TDE do banco de dados. Para obter mais informações, veja [TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md). No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], os arquivos de ponto de verificação não são criptografados, mesmo se a TDE estiver habilitada no banco de dados.
  
## <a name="see-also"></a>Consulte Também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
