---
title: "Configurando o armazenamento para tabelas com otimização de memória | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0250c8370960dc17adf13c020c51bfc603b111c8
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Configuração do armazenamento para tabelas com otimização de memória
  Você precisa configurar a capacidade de armazenamento e operações de entrada/saída por segundo (IOPS).  
  
## <a name="storage-capacity"></a>Capacidade de armazenamento  
 Use as informações em [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) para estimar o tamanho na memória das tabelas com otimização de memória duráveis do banco de dados. Como os índices não são mantidos para tabelas com otimização de memória, não incluem o tamanho dos índices. Depois de determinar o tamanho, você precisa fornecer espaço em disco que é quatro vezes o tamanho das tabelas duráveis na memória.  
  
## <a name="storage-iops"></a>IOPS de armazenamento  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] pode aumentar significativamente a taxa de transferência da carga de trabalho. Portanto, é importante garantir que a E/A não seja um gargalo.  
  
-   Ao migrar tabelas baseadas em disco para tabelas com otimização de memória, verifique se o log de transações está em uma mídia de armazenamento compatível com atividade de log de transações aumentada. Por exemplo, se a mídia de armazenamento oferece suporte a operações de log de transações a 100 MB/s e as tabelas com otimização de memória resultam em um desempenho cinco vezes maior, a mídia de armazenamento do log de transações deve ser capaz de oferecer suporte também à melhoria de desempenho cinco vezes maior, para evitar que a atividade de log de transações se torne um gargalo de desempenho.  
  
-   Tabelas com otimização de memória persistem em arquivos distribuídos em um ou mais contêineres. Cada contêiner normalmente deverá ser mapeado para seu próprio eixo e é usado para obter uma maior capacidade de armazenamento e um melhor IOPS. Você precisa garantir que o IOPS sequencial da mídia de armazenamento possa oferecer suporte 3 vezes maior em produtividade de logs de transações.  
  
     Por exemplo, se tabelas com otimização de memória gerarem 500 MB/s de atividade no log de transações, o armazenamento de tabelas com otimização de memória deverá ter suporte para 1,5 GB/s IOPS. A necessidade de oferecer suporte a 3 vezes o aumento na produtividade dos logs de transações é proveniente da observação de que os pares de arquivos de dados e delta são gravados primeiro com os dados iniciais e, em seguida, precisam ser leitura/regravação como parte de uma operação de mesclagem.  
  
     Outro fator na estimativa de IOPS para armazenamento é o tempo de recuperação para tabelas com otimização de memória. Dados de tabelas duráveis devem ser lidos na memória antes de um banco de dados ser disponibilizado para aplicativos. Normalmente, carregar dados em tabelas com otimização de memória pode ser feito na velocidade do IOPS. Portanto, se o armazenamento total para tabelas duráveis com otimização de memória for de 60 GB e você desejar ser capaz de carregar esses dados em 1 minuto, o IOPS do armazenamento deverá ser definido em 1 GB/s.  
  
-   Se você tiver um número par de eixos, diferentemente do SQL Server 2014, os arquivos de ponto de verificação serão distribuídos uniformemente em todos os eixos.  
  
## <a name="encryption"></a>Criptografia  
 No [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o armazenamento de tabelas com otimização de memória será criptografado como parte da habilitação de TDE do banco de dados. Para obter mais informações, veja [TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption-tde.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
