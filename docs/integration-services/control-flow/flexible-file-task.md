---
description: Tarefa Arquivo Flexível
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
ms.openlocfilehash: c93cecf5b261a888375ead03aac1eec07b76c63d
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196490"
---
# <a name="flexible-file-task"></a>Tarefa Arquivo Flexível

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

A Tarefa de Arquivo Flexível permite que os usuários realizem operações de arquivo em vários serviços de armazenamento compatíveis.
Os serviços de armazenamento compatíveis no momento são

- Sistema de Arquivos Local
- [Armazenamento de Blobs do Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](/azure/storage/blobs/data-lake-storage-introduction)

A Tarefa de Arquivo Flexível é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para adicionar uma Tarefa de Arquivo Flexível a um pacote, arraste-a da Caixa de Ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes na tarefa ou clique com o botão direito do mouse na tarefa e selecione **Editar** para abrir a caixa de diálogo **Editor de Tarefa de Arquivo Flexível**.

A propriedade **Operation** especifica a operação de arquivo a ser executada.
As operações com suporte atualmente são:
- Operação **Copy**
- Operação **Delete**

Para a operação **Copy**, as seguintes propriedades estão disponíveis.

- **SourceConnectionType:** especifica o tipo do gerenciador de conexões de origem.
- **SourceConnection:** especifica o gerenciador de conexões de origem.
- **SourceFolderPath:** especifica o caminho da pasta de origem.
- **SourceFileName:** especifica o nome do arquivo de origem. Se deixada em branco, a pasta de origem será copiada. Os seguintes curingas são permitidos no nome do arquivo de origem: `*` (corresponde a zero ou mais caracteres), `?` (corresponde a zero ou a um só caractere) e `^` (caractere de escape).
- **SearchRecursively:** especifica se as subpastas devem ser copiadas de maneira recursiva.
- **DestinationConnectionType:** especifica o tipo do gerenciador de conexões de destino.
- **DestinationConnection:** especifica o gerenciador de conexões de destino.
- **DestinationFolderPath:** especifica o caminho da pasta de destino.
- **DestinationFileName:** especifica o nome do arquivo de destino. Se esse campo for deixado em branco, os nomes do arquivo de origem serão usados.

Para a operação **Delete**, as seguintes propriedades estão disponíveis.
- **ConnectionType:** especifica o tipo do gerenciador de conexões.
- **Connection:** especifica o gerenciador de conexões.
- **FolderPath:** especifica o caminho da pasta.
- **FileName:** especifica o nome do arquivo. Se deixada em branco, a pasta será excluída. No Armazenamento de Blobs do Azure, não há suporte para a exclusão de pastas. Os seguintes curingas são permitidos no nome do arquivo: `*` (corresponde a zero ou mais caracteres), `?` (corresponde a zero ou a um só caractere) e `^` (caractere de escape).
- **DeleteRecursively:** especifica se os arquivos serão excluídos recursivamente.

***Observações sobre a configuração de permissão da entidade de serviço***

Para que a **conexão de teste** funcione (armazenamento de blobs ou Data Lake Storage Gen2), a entidade de serviço deve ser atribuída pelo menos à função de **Leitor de Dados do Storage Blob** para a conta de armazenamento.
Isso é feito com o [RBAC](/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal).

Para o armazenamento de blobs, as permissões de leitura e gravação são concedidas por meio da atribuição de pelo menos as funções de **Leitor de Dados do Storage Blob** e **Colaborador de Dados do Storage Blob**, respectivamente.

Para o Azure Data Lake Storage Gen2, a permissão é determinada pelo RBAC e pelas [ACLs](/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer).
Preste atenção nas ACLs que são configuradas usando a OID (ID de objeto) da entidade de serviço para o registro do aplicativo, conforme detalhado [aqui](/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal).
Isso é diferente da ID do aplicativo (cliente) que é usada com a configuração de RBAC.
Quando uma entidade de segurança recebe permissões de dados RBAC por meio de uma função interna ou por meio de uma função personalizada, essas permissões são avaliadas primeiro após a autorização de uma solicitação.
Se a operação solicitada for autorizada pelas atribuições de RBAC da entidade de segurança, a autorização será imediatamente resolvida e nenhuma verificação de ACL adicional será executada.
Como alternativa, se a entidade de segurança não tiver uma atribuição de RBAC ou se a operação da solicitação não corresponder à permissão atribuída, as verificações de ACL serão executadas para determinar se a entidade de segurança está autorizada a executar a operação solicitada.

- Para a permissão de leitura, conceda pelo menos a permissão de **execução** no sistema de arquivos de origem, juntamente com a permissão de **Leitura** para os arquivos a serem copiados. Como alternativa, conceda pelo menos a função de **Leitor de dados do blob de armazenamento** com RBAC.
- Para a permissão de gravação, conceda pelo menos a permissão de **execução** no sistema de arquivos do coletor, juntamente com a permissão de **gravação** para a pasta do coletor. Como alternativa, conceda pelo menos a função de **Colaborador de dados do blob de armazenamento** com RBAC.

Consulte [este](/azure/storage/blobs/data-lake-storage-access-control) artigo para obter detalhes.