---
title: Nova inicialização de par (replicação ponto a ponto) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51e5ec3832d497f342c4fc3132a75261f6c3c154
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63022684"
---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>Inicialização de Novo Computador Par (replicação ponto a ponto)
  Use a página **Inicialização de Novo Computador Par** para especificar como os bancos de dados do mesmo nível foram inicializados. (Os pares devem ser inicializados antes que você conclua esse assistente.) Os pares são inicializados manualmente ou por meio da funcionalidade **inicializar com backup** fornecida pela replicação transacional. (A replicação transacional ponto a ponto não oferece suporte a inicialização de pares usando um instantâneo.) Se computadores diferentes do mesmo nível precisarem ser inicializados usando métodos diferentes, será necessário adicioná-los separadamente executando o assistente várias vezes.  
  
## <a name="options"></a>Opções  
 **Especifique como os novos bancos de dados pares foram inicializados**  
 O esquema e os dados de todos os objetos publicados devem estar presentes em cada computador par. Selecione uma das seguintes opções:  
  
-   Selecione a primeira opção se você criou manualmente o esquema a para objetos publicados ou se restaurou um backup e nenhuma alteração de dados foi feita no primeiro banco de dados de publicação desde que o backup foi feito. Se você criou o esquema manualmente, deve assegurar que todos os dados exigidos estão presentes em cada computador par. Essa opção corresponde a um valor **suporte para replicação somente** para a propriedade de assinatura **sync_type**.  
  
-   Selecione a segunda opção se você restaurou um backup e nenhuma alteração de dados foi feita no primeiro banco de dados de publicação desde que o backup foi feito. Agora, a replicação deve entregar as alterações do primeiro banco de dados de publicação que não foi incluído no backup. Essa opção corresponde a um valor **inicializar com backup** para a propriedade de assinatura **sync_type**.  
  
     Quando uma publicação é habilitada para replicação ponto a ponto, a propriedade de publicação **allow_initialize_from_backup** é definida. A replicação começa a controlar as alterações imediatamente no primeiro banco de dados de publicação. Portanto, essas alterações podem ser entregues a um banco de dados restaurado em um ou mais pares se a opção **inicializar com backup** estiver selecionada. Clique no botão **Procurar** para localizar o backup usado e a replicação lerá o LSN (número de sequência de log) do backup. Todas as alterações no primeiro banco de dados de publicação que têm um LSN mais alto serão entregues a cada computador par.  
  
     Essa opção pode não estar disponível se você estiver criando ou adicionando a uma topologia que inclui [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. A tabela a seguir mostra se a opção estará disponível quando você estiver adicionando um nó a uma topologia existente.  
  
    |Novo nó|Primeiro nó|Nós adicionais|Opção|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Desabilitado|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|Nenhum|Desabilitado|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Desabilitado|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Nenhum|habilitado|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|Nenhum|habilitado|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|habilitado|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Nenhum|habilitado|  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar uma topologia ponto a ponto &#40;programação Transact-SQL de replicação&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)  
  
  
