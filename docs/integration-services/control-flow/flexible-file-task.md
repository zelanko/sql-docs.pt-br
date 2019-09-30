---
title: Tarefa de Arquivo Flexível | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3aaa746be1453f874a77af6bbfdf318da0731623
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298280"
---
# <a name="flexible-file-task"></a>Tarefa Arquivo Flexível

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

A Tarefa de Arquivo Flexível permite que os usuários realizem operações de arquivo em vários serviços de armazenamento compatíveis.
Os serviços de armazenamento compatíveis no momento são

- Sistema de Arquivos Local
- [Armazenamento de Blobs do Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

A Tarefa de Arquivo Flexível é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para adicionar uma Tarefa de Arquivo Flexível a um pacote, arraste-a da Caixa de Ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes na tarefa ou clique com o botão direito do mouse na tarefa e selecione **Editar** para abrir a caixa de diálogo **Editor de Tarefa de Arquivo Flexível**.

A propriedade **Operation** especifica a operação de arquivo a ser executada.
Somente a operação **Copy** é compatível no momento.

Para a operação **Copy**, as seguintes propriedades estão disponíveis.

- **SourceConnectionType:** especifica o tipo do gerenciador de conexões de origem.
- **SourceConnection:** especifica o gerenciador de conexões de origem.
- **SourceFolderPath:** especifica o caminho da pasta de origem.
- **SourceFileName:** especifica o nome do arquivo de origem. Se deixada em branco, a pasta de origem será copiada.
- **SearchRecursively:** especifica se as subpastas devem ser copiadas de maneira recursiva.
- **DestinationConnectionType:** especifica o tipo do gerenciador de conexões de destino.
- **DestinationConnection:** especifica o gerenciador de conexões de destino.
- **DestinationFolderPath:** especifica o caminho da pasta de destino.
- **DestinationFileName:** especifica o nome do arquivo de destino.

***Observações sobre a configuração de permissão da entidade de serviço***

Para que a **conexão de teste** funcione (armazenamento de blobs ou Data Lake Storage Gen2), a entidade de serviço deve ser atribuída pelo menos à função de **Leitor de Dados do Storage Blob** para a conta de armazenamento.
Isso é feito com o [RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal).

Para o armazenamento de blobs, as permissões de leitura e gravação são concedidas por meio da atribuição de pelo menos as funções de **Leitor de Dados do Storage Blob** e **Colaborador de Dados do Storage Blob**, respectivamente.

Para o Azure Data Lake Storage Gen2, a permissão é determinada pelo RBAC e pelas [ACLs](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer).
Preste atenção nas ACLs que são configuradas usando a OID (ID de objeto) da entidade de serviço para o registro do aplicativo, conforme detalhado [aqui](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal).
Isso é diferente da ID do aplicativo (cliente) que é usada com a configuração de RBAC.
Quando uma entidade de segurança recebe permissões de dados RBAC por meio de uma função interna ou por meio de uma função personalizada, essas permissões são avaliadas primeiro após a autorização de uma solicitação.
Se a operação solicitada for autorizada pelas atribuições de RBAC da entidade de segurança, a autorização será imediatamente resolvida e nenhuma verificação de ACL adicional será executada.
Como alternativa, se a entidade de segurança não tiver uma atribuição de RBAC ou se a operação da solicitação não corresponder à permissão atribuída, as verificações de ACL serão executadas para determinar se a entidade de segurança está autorizada a executar a operação solicitada.

- Para a permissão de leitura, conceda pelo menos a permissão de **execução** no sistema de arquivos de origem, juntamente com a permissão de **Leitura** para os arquivos a serem copiados. Como alternativa, conceda pelo menos a função de **Leitor de dados do blob de armazenamento** com RBAC.
- Para a permissão de gravação, conceda pelo menos a permissão de **execução** no sistema de arquivos do coletor, juntamente com a permissão de **gravação** para a pasta do coletor. Como alternativa, conceda pelo menos a função de **Colaborador de dados do blob de armazenamento** com RBAC.

Consulte [este](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control) artigo para obter detalhes.
