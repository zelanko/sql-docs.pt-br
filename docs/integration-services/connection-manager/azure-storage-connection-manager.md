---
title: Gerenciador de conexões do Armazenamento do Azure | Microsoft Docs
description: O gerenciador de conexões do Armazenamento do Azure habilita a conexão de um pacote do SSIS com uma conta do Armazenamento do Azure.
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8fd8b9b94d809a304e2f9347edba67d5ff7d9b85
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294457"
---
# <a name="azure-storage-connection-manager"></a>Gerenciador de conexões do Armazenamento do Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

O gerenciador de conexões do Armazenamento do Azure habilita a conexão de um pacote do SSIS (SQL Server Integration Services) com uma conta do Armazenamento do Azure. O gerenciador de conexões é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
Na caixa de diálogo **Adicionar Gerenciador de Conexões do SSIS**, selecione **AzureStorage** > **Adicionar**.  
  
As propriedades a seguir estão disponíveis.

- **Serviço:** especifica o serviço de armazenamento ao qual se conectar.
- **Nome da conta:** especifica o nome da conta de armazenamento.
- **Autenticação:** especifica o método de autenticação a ser usado. As autenticações AccessKey e ServicePrincipal são compatíveis.
    - **AccessKey:** para esse método de autenticação, especifique a **chave de conta**.
    - **ServicePrincipal:** Para esse método de autenticação, especifique a **ID do aplicativo**, a **Chave do aplicativo** e a **ID do locatário** da entidade de serviço.
      Para que a **Conexão de teste** funcione, a entidade de serviço precisa ser atribuída pelo menos à função de **Leitor de Dados do Storage Blob** para a conta de armazenamento.
      Para obter mais informações, confira [Conceder acesso ao blob do Azure e dados de fila com RBAC no portal do Azure](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal).
- **Ambiente:** especifica o ambiente de nuvem que hospeda a conta de armazenamento.

## <a name="managed-identities-for-azure-resources-authentication"></a>Identidades gerenciadas para autenticação de recursos do Azure
Ao executar pacotes SSIS no [Azure-SSIS Integration Runtime no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), você pode usar a [identidade gerenciada](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associada ao data factory para a autenticação do armazenamento do Azure. O factory designado pode acessar dados do banco de dados e copiá-los para a conta de armazenamento usando essa identidade.

Saiba mais sobre a autenticação de armazenamento do Azure em geral em [Autenticar o acesso ao Armazenamento do Azure usando o Azure Active Directory](https://docs.microsoft.com/azure/storage/common/storage-auth-aad). Para usar a autenticação de identidade gerenciada para o Armazenamento do Azure:

1. [Encontre a identidade gerenciada do data factory no portal do Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). Acesse as **Propriedades** do data factory. Copie a **ID do Aplicativo da Identidade Gerenciada** (não a **ID de Objeto da Identidade Gerenciada**).

1. Conceda à identidade gerenciada as devidas permissões em sua conta de armazenamento. Para obter mais detalhes sobre as funções, confira [Gerenciar direitos de acesso aos dados do Armazenamento do Azure com o RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal).

    - **Como origem**, em Controle de acesso (IAM), conceda, pelo menos, a função de **Leitor de Dados do Storage Blob**.
    - **Como destino**, em Controle de acesso (IAM), conceda, pelo menos, a função de **Colaborador de Dados do Storage Blob**.

Em seguida, configure a autenticação de identidade gerenciada do gerenciador de conexões de Armazenamento do Azure. Veja a seguir as opções para fazer isso:

- **Configurar em tempo de design.** No Designer SSIS, clique duas vezes no gerenciador de conexões de Armazenamento do Azure para abrir o **Editor do gerenciador de conexões do Armazenamento do Azure**. Selecione **Usar identidade gerenciada para autenticar no Azure**.
    > [!NOTE]
    >  Atualmente, essa opção não entra em vigor (indicando que a autenticação de identidade gerenciada não funciona) quando você executa o pacote SSIS no SSIS Designer ou no SQL Server [!INCLUDE[msCoName](../../includes/msconame-md.md)].
    
- **Configurar no tempo de execução.** Ao executar o pacote via [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) ou a [atividade Executar Pacote SSIS do Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), localize o gerenciador de conexões do Armazenamento do Azure. Atualize sua propriedade `ConnectUsingManagedIdentity` para `True`.
    > [!NOTE]
    >  No Azure-SSIS Integration Runtime, todos os outros métodos de autenticação (por exemplo, chave de acesso e entidade de serviço) pré-configurados no gerenciador de conexões do Armazenamento do Azure serão substituídos quando a autenticação de identidade gerenciada for usada para operações de armazenamento.

> [!NOTE]
>  Para configurar a autenticação de identidade gerenciada em pacotes existentes, a maneira preferencial é recompilar seu projeto SSIS com o [Designer SSIS mais recente](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) pelo menos uma vez. Reimplante esse projeto SSIS para o Azure-SSIS Integration Runtime, para que a nova propriedade do gerenciador de conexões `ConnectUsingManagedIdentity` seja automaticamente adicionada a todos os gerenciadores de conexões Armazenamento do Azure no projeto SSIS. Como alternativa, pode-se usar diretamente uma substituição de propriedade com o caminho de propriedade **\Package.Connections [{nome do seu gerenciador de conexões}].Properties[ConnectUsingManagedIdentity]** no tempo de execução.

## <a name="see-also"></a>Confira também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)
