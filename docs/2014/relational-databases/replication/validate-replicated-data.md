---
title: Validar os dados replicados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- inline data validation [SQL Server replication]
- administering replication, validating data
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication]
- merge replication data validation [SQL Server replication], about data validation
- validating replicated data
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
caps.latest.revision: 45
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0fad815b99f6daf9ba14e765f394cfe1e416aaa6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211216"
---
# <a name="validate-replicated-data"></a>Validar os dados replicados
  A replicação transacional e de mesclagem permitem validar os dados no Assinante que correspondem aos dados no Publicador. A validação pode ser executada para assinaturas específicas ou para todas as assinaturas em uma publicação. Especifique um dos seguintes tipos de validação e o Distribution Agent ou o Merge Agent validarão os dados na próxima vez que executarem:  
  
-   Somente número de linhas. Faz a validação se a tabela no Assinante tem o mesmo número de linhas que a tabela no Publicador, mas não faz a validação da correspondência de conteúdo das linhas. A validação de número de linhas fornece uma abordagem superficial à validação que pode alertá-lo sobre problemas com seus dados.  
  
-   Número de linhas e soma de verificação binária. Além de contar o número de linhas no Publicador e no Assinante, uma soma de verificação de todos os dados é calculada usando o algoritmo de soma de verificação. Se a contagem de linhas falhar, a soma de verificação não será executada.  
  
 Além de validar se esses dados no Assinante e no Publicador são correspondentes, a replicação de mesclagem fornece a capacidade de validar se os dados estão particionados corretamente em cada Assinante. Para obter mais informações, consulte [Validate Partition Information for a Merge Subscriber](validate-partition-information-for-a-merge-subscriber.md) (Validar informações de partição para um assinante de mesclagem).  
  
 **Para validar os dados**  
  
 Para validar todos os artigos de uma assinatura, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimentos armazenados ou RMO (Replication Management Objects). Para obter mais informações, consulte [Validate Data at the Subscriber](validate-data-at-the-subscriber.md). Para validar os artigos individuais em publicações transacionais ou de instantâneo, é preciso usar procedimentos armazenados.  
  
## <a name="data-validation-results"></a>Resultados da validação de dados  
 Quando a validação estiver completa, o Distribution Agent ou o Merge Agent registra mensagens relativas ao êxito ou falha (a replicação não informa quais as linhas que falharam). Essas mensagens podem ser exibidas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Replication Monitor e nas tabelas do sistema de replicação. O tópico de instruções listado acima mostra como executar a validação e exibir os resultados.  
  
 Para controlar as falhas de validação, considere o seguinte:  
  
-   Configure o alerta de replicação chamado **Replicação: Falha na validação de dados do assinante** para que você seja notificado da falha. Para obter mais informações, consulte [configurar alertas de replicação predefinidos &#40;SQL Server Management Studio & #41(administration/configure-predefined-replication-alerts-sql-server-management-studio.md).  
  
-   O fato da validação falhar é um problema para o seu aplicativo? Se a falha de validação é um problema, atualize manualmente os dados para serem sincronizados ou reinicialize a assinatura:  
  
    -   Os dados podem ser atualizados usando o [utilitário tablediff](../../tools/tablediff-utility.md). Para mais informações sobre como usar esse utilitário, consulte [Comparar tabelas replicadas para diferenças &#40;Programação de replicação&#41;](administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    -   Para mais informações sobre reinicialização, consulte [Reinicializar as assinaturas](reinitialize-subscriptions.md).  
  
## <a name="considerations-for-data-validation"></a>Considerações sobre a validação de dados  
 Considere os seguintes problemas ao validar dados:  
  
-   Você deve cessar todas as atividades nos Assinantes antes de validar os dados (não é necessário parar as atividades do Publicador, enquanto ocorre a validação).  
  
-   Como as somas de verificação e as somas de verificações binárias podem requerer recursos extensos do processador ao validar conjuntos de dados muito grandes, você deverá agendar a validação quando houver um mínimo de atividade nos servidores usados na replicação.  
  
-   A replicação somente valida tabelas; não realizando a validação se os artigos somente esquema (como os procedimentos armazenados) são os mesmos no Publicador e no Assinante.  
  
-   A soma de verificação binária pode ser usada com qualquer tabela publicada. A soma de verificação não pode validar as tabelas com filtros de colunas ou estruturas de tabelas lógicas nas quais os deslocamentos são diferentes (por causa das instruções ALTER TABLE que cancelam ou adicionam colunas).  
  
-   Validação de replicação usa o `checksum` e **binary_checksum** funções. Para informações sobre seu comportamento, consulte [CHECKSUM &#40;Transact-SQL&#41;](/sql/t-sql/functions/checksum-transact-sql) e [BINARY_CHECKSUM  &#40;Transact-SQL&#41;](/sql/t-sql/functions/binary-checksum-transact-sql).  
  
-   A validação com o uso de soma de verificação binária ou soma de verificação pode reportar incorretamente uma falha se os tipos de dados forem diferentes no Assinante e no Publicador. Isso poderá acontecer se você fizer o seguinte:  
  
    -   Definir explicitamente opções de esquema para mapear tipos de dados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Definir o nível de compatibilidade de uma publicação de mesclagem para uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e as tabelas publicadas contiverem um ou mais tipos de dados que devem ser mapeados para essa versão.  
  
    -   Inicialize manualmente uma assinatura que estiver usando tipos de dados diferentes no Assinante.  
  
-   As validações da soma de verificação binária e de soma de verificação não oferecem suporte para assinaturas transformáveis na replicação transacional.  
  
-   A validação não oferece suporte para os dados replicados em não assinantes do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="how-data-validation-works"></a>Como a validação de dados trabalha  
 O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz a validação dos dados calculando o número de linhas ou uma soma de verificação no Publicador e comparando esses valores com o número de linhas ou a soma de verificação do Assinante. Um valor é calculado para a publicação inteira e um valor é calculado para a tabela de assinatura inteira, mas os dados em `text`, `ntext` ou as colunas de `image` não são incluídas nos cálculos.  
  
 Enquanto os cálculos estão sendo realizados, são colocados temporariamente bloqueios compartilhados em tabelas, nas quais as contagens de linhas ou as somas de verificações estão sendo executadas, mas são completadas rapidamente e os bloqueios compartilhados removidos, normalmente em questão de segundos.  
  
 Quando as somas de verificação binárias são usadas, ocorre uma verificação de redundância (CRC) de 32 bits coluna a coluna, em vez de uma CRC na linha física da página de dados. Isso permite que as colunas da tabela estejam em qualquer ordem física na página de dados, mas sejam calculadas no mesmo CRC da linha. A validação de soma de verificação binária pode ser usada quando há filtros de linha ou de coluna na publicação.  
  
## <a name="see-also"></a>Consulte também  
 [Best Practices for Replication Administration](administration/best-practices-for-replication-administration.md)  
  
  
