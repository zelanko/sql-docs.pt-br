---
title: Validar os dados replicados | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 987f1e5f8afb8afd6093518c2c3cbc7bef078ede
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711794"
---
# <a name="validate-replicated-data"></a>Validar os dados replicados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A replicação transacional e de mesclagem permitem validar os dados no Assinante que correspondem aos dados no Publicador. A validação pode ser executada para assinaturas específicas ou para todas as assinaturas em uma publicação. Especifique um dos seguintes tipos de validação e o Distribution Agent ou o Merge Agent validarão os dados na próxima vez que executarem:  
  
-   Somente número de linhas. Faz a validação se a tabela no Assinante tem o mesmo número de linhas que a tabela no Publicador, mas não faz a validação da correspondência de conteúdo das linhas. A validação de número de linhas fornece uma abordagem superficial à validação que pode alertá-lo sobre problemas com seus dados.  
  
-   Número de linhas e soma de verificação binária. Além de contar o número de linhas no Publicador e no Assinante, uma soma de verificação de todos os dados é calculada usando o algoritmo de soma de verificação. Se a contagem de linhas falhar, a soma de verificação não será executada.  
  
 Além de validar se esses dados no Assinante e no Publicador são correspondentes, a replicação de mesclagem fornece a capacidade de validar se os dados estão particionados corretamente em cada Assinante. Para obter mais informações, consulte [Validate Partition Information for a Merge Subscriber](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md) (Validar informações de partição para um assinante de mesclagem).  
  
 **Para validar os dados**  
  
 Para validar todos os artigos de uma assinatura, use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimentos armazenados ou RMO (Replication Management Objects). Para obter mais informações, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md). Para validar os artigos individuais em publicações transacionais ou de instantâneo, é preciso usar procedimentos armazenados.  
  
## <a name="data-validation-results"></a>Resultados da validação de dados  
 Quando a validação estiver completa, o Distribution Agent ou o Merge Agent registra mensagens relativas ao êxito ou falha (a replicação não informa quais as linhas que falharam). Essas mensagens podem ser exibidas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Replication Monitor e nas tabelas do sistema de replicação. O tópico de instruções listado acima mostra como executar a validação e exibir os resultados.  
  
 Para controlar as falhas de validação, considere o seguinte:  
  
-   Configure o alerta de replicação chamado **Replicação: Falha na validação de dados do assinante** para que você seja notificado da falha. Para mais informações, consulte [Como configurar alertas de replicação predefinidos &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md).  
  
-   O fato da validação falhar é um problema para o seu aplicativo? Se a falha de validação é um problema, atualize manualmente os dados para serem sincronizados ou reinicialize a assinatura:  
  
    -   Os dados podem ser atualizados usando o [utilitário tablediff](../../tools/tablediff-utility.md). Para mais informações sobre como usar esse utilitário, consulte [Comparar tabelas replicadas para diferenças &#40;Programação de replicação&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    -   Para mais informações sobre reinicialização, consulte [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## <a name="considerations-for-data-validation"></a>Considerações sobre a validação de dados  
 Considere os seguintes problemas ao validar dados:  
  
-   Você deve cessar todas as atividades nos Assinantes antes de validar os dados (não é necessário parar as atividades do Publicador, enquanto ocorre a validação).  
  
-   Como as somas de verificação e as somas de verificações binárias podem requerer recursos extensos do processador ao validar conjuntos de dados muito grandes, você deverá agendar a validação quando houver um mínimo de atividade nos servidores usados na replicação.  
  
-   A replicação somente valida tabelas; não realizando a validação se os artigos somente esquema (como os procedimentos armazenados) são os mesmos no Publicador e no Assinante.  
  
-   A soma de verificação binária pode ser usada com qualquer tabela publicada. A soma de verificação não pode validar as tabelas com filtros de colunas ou estruturas de tabelas lógicas nas quais os deslocamentos são diferentes (por causa das instruções ALTER TABLE que cancelam ou adicionam colunas).  
  
-   A validação de replicação usa as funções **checksum** e **binary_checksum** . Para informações sobre seu comportamento, consulte [CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md) e [BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md).  
  
-   A validação com o uso de soma de verificação binária ou soma de verificação pode reportar incorretamente uma falha se os tipos de dados forem diferentes no Assinante e no Publicador. Isso poderá acontecer se você fizer o seguinte:  
  
    -   Definir explicitamente opções de esquema para mapear tipos de dados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Definir o nível de compatibilidade de uma publicação de mesclagem para uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e as tabelas publicadas contiverem um ou mais tipos de dados que devem ser mapeados para essa versão.  
  
    -   Inicialize manualmente uma assinatura que estiver usando tipos de dados diferentes no Assinante.  
  
-   As validações da soma de verificação binária e de soma de verificação não oferecem suporte para assinaturas transformáveis na replicação transacional.  
  
-   A validação não oferece suporte para os dados replicados em não assinantes do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="how-data-validation-works"></a>Como a validação de dados trabalha  
 O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz a validação dos dados calculando o número de linhas ou uma soma de verificação no Publicador e comparando esses valores com o número de linhas ou a soma de verificação do Assinante. Um valor é calculado para a publicação inteira e um valor é calculado para a tabela de assinatura inteira, mas os dados em **text**, **ntext**ou as colunas de **image** não são incluídas nos cálculos.  
  
 Enquanto os cálculos estão sendo realizados, são colocados temporariamente bloqueios compartilhados em tabelas, nas quais as contagens de linhas ou as somas de verificações estão sendo executadas, mas são completadas rapidamente e os bloqueios compartilhados removidos, normalmente em questão de segundos.  
  
 Quando as somas de verificação binárias são usadas, ocorre uma verificação de redundância (CRC) de 32 bits coluna a coluna, em vez de uma CRC na linha física da página de dados. Isso permite que as colunas da tabela estejam em qualquer ordem física na página de dados, mas sejam calculadas no mesmo CRC da linha. A validação de soma de verificação binária pode ser usada quando há filtros de linha ou de coluna na publicação.  
  
## <a name="see-also"></a>Consulte Também  
 [Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
