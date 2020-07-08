---
title: Inicializar uma assinatura com um instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 44ccd31700ab6bb3bf3500e93febc0209d9fa9ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716785"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Inicializar uma assinatura com um instantâneo

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

Este artigo descreve os processos que ocorrem quando uma publicação de replicação é inicializada. Um instantâneo inicial é aplicado aos Assinantes.

## <a name="snapshot-for-a-new-publication"></a>Instantâneo de uma nova publicação

Por padrão, um instantâneo é capturado após a criação de uma publicação.
O instantâneo é copiado para a pasta de instantâneos. Esse comportamento padrão ocorre para publicações de mesclagem criadas usando o Assistente para Nova Publicação.

### <a name="snapshot-is-applied-to-subscriber"></a>O instantâneo é aplicado ao Assinante

O novo instantâneo é aplicado ao Assinante por um agente. A aplicação ocorre durante a sincronização inicial da assinatura. O agente que faz a aplicação depende do tipo de publicação:

- Para publicações _transacionais_ ou de _instantâneo_:
  - O Distribution Agent.

- Para publicações de _mesclagem_:
  - O Merge Agent.

### <a name="type-of-publication"></a>Tipo de publicação

A tabela a seguir exibe o conteúdo do instantâneo para cada tipo de publicação.

&nbsp;

| Tipo de publicação à qual o instantâneo se destina | Conteúdo do instantâneo |
| :---------------------------------------- | :----------------------- |
| <ul> <li>Publicação de instantâneo</li> <li>Publicação transacional</li> <li>Mesclar publicação que não usa filtros parametrizados</li> </ul> | <ul> <li>Esquema</li> <li>Dados, em arquivos para o BCP (programa de cópia em massa)</li> <li>Restrições</li> <li>Propriedades estendidas</li> <li>Índices</li> <li>Gatilhos</li> <li>Tabelas do sistema necessárias para replicação</li> </ul> <br/>Confira [Criar e aplicar o instantâneo](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md). |
| <ul> <li>Mesclar publicação que usa filtros parametrizados</li> </ul> | <ul> <li>Instantâneo do esquema (scripts de replicação, objetos publicados, mas sem dados)</li> <li>Dados que pertencem à partição da assinatura</li> </ul> <br/>Confira [Instantâneos para publicações de mesclagem com filtros parametrizados](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). |
| | |

#### <a name="two-part-process-with-merge-publication-that-uses-parameterized-filters"></a>Processo de duas partes com publicação de mesclagem que usa filtros parametrizados

Para uma publicação de mesclagem que usa filtros com parâmetros, o instantâneo é criado usando o seguinte processo de duas partes:

1. É criado um instantâneo de esquema, que contém os seguintes itens:
   - Scripts de replicação.
   - Esquema dos objetos publicados.
   - _(Mas sem dados.)_

2. Cada assinatura é inicializada com um instantâneo. O instantâneo inclui os seguintes itens:
   - Scripts e esquema, copiados do instantâneo do esquema.
   - Dados que pertencem à partição da assinatura.

## <a name="type-of-replication"></a>Tipo de replicação

Os tipos de arquivo contidos no instantâneo dependem do tipo de replicação e dos artigos em sua publicação.

&nbsp;

| Tipo de replicação | Arquivos comuns de instantâneo |
| :------------------ | :-------------------- |
| Replicação de instantâneo ou<br/>Replicação transacional | &bullet; Esquema (.sch) <br/>&bullet; Dados (.bcp) <br/>&bullet; Índices e restrições (.dri) <br/>&bullet; Arquivos de instantâneo compactados (.cab) <br/>&bullet; Gatilhos (.tag), somente para atualizar um Assinante <br/><br/>&bullet; Restrições (.idx). |
| Replicação de mesclagem                                      | &bullet; Esquema (.sch) <br/>&bullet; Dados (.bcp) <br/>&bullet; Índices e restrições (.dri) <br/>&bullet; Arquivos de instantâneo compactados (.cab) <br/>&bullet; Gatilhos (.trg) <br/><br/>&bullet; Dados de tabela de sistema (.sys) <br/>&bullet; Tabelas de conflitos (.cft). |
| | |

### <a name="snapshot-folder"></a>Pasta do instantâneo

Os arquivos são transferidos ao serem copiados para a _pasta de instantâneo_ padrão ou para a _pasta alternativa_ para instantâneos.

A pasta de instantâneos é especificada quando o Distribuidor é configurado. A pasta alternativa é especificada quando a publicação é criada.

### <a name="resume-transfer-after-interruption"></a>Retomar transferência após a interrupção

A transferência de arquivos para uma pasta de instantâneos será retomada automaticamente se a transferência for interrompida por uma conexão não confiável.

Para fins de eficiência, a continuação não reenvia nenhum arquivo que já foi totalmente transferido antes da interrupção.

## <a name="snapshot-options"></a>Opções de instantâneo

Há várias opções disponíveis ao inicializar uma assinatura com um instantâneo. Você pode:

- Especificar um local alternativo para a pasta de instantâneo em vez do ou além do local da pasta de instantâneo padrão. Para obter mais informações, confira [Modificar opções de instantâneo](../../relational-databases/replication/snapshot-options.md).

- Compacte instantâneos para armazenamento em mídias removíveis ou para transferência em uma rede lenta. Para obter mais informações, consulte [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots).

- Execute scripts de Transact-SQL antes ou depois que o instantâneo seja aplicado. Para mais informações, consulte [Executar scripts antes e depois da aplicação do instantâneo](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).

- Transfira arquivos de instantâneo usando o Protocolo de Transferência de Arquivo (FTP). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).

## <a name="see-also"></a>Consulte Também

[Inicializar uma Assinatura](../../relational-databases/replication/initialize-a-subscription.md)

[Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md)
