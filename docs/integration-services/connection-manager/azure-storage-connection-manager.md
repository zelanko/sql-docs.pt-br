---
title: Gerenciador de Conexões do Armazenamento do Azure | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f171499471f8f94ad970446d31cf796f4ab55fb7
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028767"
---
# <a name="azure-storage-connection-manager"></a>Gerenciador de conexões do Armazenamento do Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  O **gerenciador de conexões do Armazenamento do Azure** habilita a conexão de um pacote do SSIS com uma conta do Armazenamento do Azure.
   
 O **gerenciador de conexões do Armazenamento do Azure** é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS** , selecione **AzureStorage**e clique em **Adicionar**.  
  
As seguintes propriedades estão disponíveis.

- **Serviço:** especifica o serviço de armazenamento ao qual se conectar.
- **Nome da conta:** especifica o nome da conta de armazenamento.
- **Autenticação:** especifica o método de autenticação a ser usado. As autenticações **AccessKey** e **ServicePrincipal** são compatíveis.
    - **AccessKey:** para esse método de autenticação, especifique a **chave de conta**.
    - **ServicePrincipal:** para esse método de autenticação, especifique a **ID do aplicativo**, a **Chave do aplicativo** e a **ID do locatário** da entidade de serviço.
      Para que a **conexão de teste** funcione, a entidade de serviço deve ser atribuída pelo menos à função de **Leitor de Dados do Storage Blob** para a conta de armazenamento.
      Confira [esta](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) página para saber mais detalhes.
- **Ambiente:** especifica o ambiente de nuvem que hospeda a conta de armazenamento.

## <a name="managed-identities-for-azure-resources-authentication"></a>Identidades gerenciadas para autenticação de recursos do Azure
Ao executar pacotes SSIS no [Azure-SSIS Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), você pode usar a [identidade gerenciada](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associada ao data factory para a autenticação do armazenamento do Azure. O factory designado pode acessar dados do banco de dados e copiá-los para a conta de armazenamento usando essa identidade.

Saiba mais sobre a autenticação de armazenamento do Azure em geral em [Autenticar o acesso ao Armazenamento do Azure usando o Azure Active Directory](https://docs.microsoft.com/azure/storage/common/storage-auth-aad). Para usar a autenticação de identidade gerenciada para o armazenamento do Azure, siga estas etapas para configurar sua conta de armazenamento:

1. **[Encontre a identidade gerenciada do data factory no portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)** . Acesse as **Propriedades** do data factory. Copie a **ID do Aplicativo da Identidade Gerenciada** (NÃO a **ID de Objeto da Identidade Gerenciada**).

1. **Conceda à identidade gerenciada as devidas permissões em sua conta de armazenamento**. Saiba mais sobre as funções em [Gerenciar os direitos de acesso aos dados de armazenamento do Azure com RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal).

    - **Como origem**, em Controle de acesso (IAM), conceda, pelo menos, a função de **Leitor de Dados do Storage Blob**.
    - **Como destino**, em Controle de acesso (IAM), conceda, pelo menos, a função de **Colaborador de Dados do Storage Blob**.

Em seguida, **configure a autenticação de identidade gerenciada** do gerenciador de conexões de armazenamento do Azure. Há duas opções para fazer isso.

1. Configurar em tempo de design. No Designer SSIS, clique duas vezes no gerenciador de conexões do Azure para abrir o **Editor do Gerenciador de Conexões de Armazenamento do Azure** e marque **Usar a identidade gerenciada para autenticar no Azure**.
    > [!NOTE]
    >  Atualmente, esta opção NÃO entra em vigor (indicando que a autenticação de identidade gerenciada não funciona) quando você executa o pacote SSIS no Designer do SSIS ou no [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.
    
1. Configurar em tempo de execução. Quando você executar o pacote por meio do [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) ou da [atividade Executar Pacote SSIS do Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), localize o gerenciador de conexões de armazenamento do Azure e atualize sua propriedade **ConnectUsingManagedIdentity** como **True**.
    > [!NOTE]
    >  No Azure-SSIS Integration Runtime, todos os outros métodos de autenticação (por exemplo, chave de acesso, entidade de serviço) pré-configurados no gerenciador de conexões do armazenamento do Azure serão **substituídos** quando a autenticação de identidade gerenciada for usada para operações de armazenamento.

> [!NOTE]
>  A maneira preferida para configurar a autenticação de identidade gerenciada em pacotes existentes, é recompilar o projeto do SSIS com o [Designer do SSIS mais recente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) pelo menos uma vez e reimplantar esse projeto do SSIS no Azure-SSIS Integration Runtime, de modo que a nova propriedade do gerenciador de conexões **ConnectUsingManagedIdentity** seja adicionada automaticamente a todos os gerenciadores de conexões de armazenamento do Azure no projeto do SSIS. Como alternativa, pode-se usar diretamente a substituição de propriedade com o caminho de propriedade **\Package.Connections [{nome do seu gerenciador de conexões}].Properties[ConnectUsingManagedIdentity]** no tempo de execução.

## <a name="see-also"></a>Consulte Também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)
