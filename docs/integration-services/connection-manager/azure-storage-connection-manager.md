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
ms.openlocfilehash: 44193053e6a5f09b2864b95ded9c5ac933c4cf95
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726017"
---
# <a name="azure-storage-connection-manager"></a>Gerenciador de conexões do Armazenamento do Azure

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

O gerenciador de conexões do Armazenamento do Azure habilita a conexão de um pacote do SSIS (SQL Server Integration Services) com uma conta do Armazenamento do Azure. O gerenciador de conexões é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
Na caixa de diálogo **Adicionar Gerenciador de Conexões do SSIS**, selecione **AzureStorage** > **Adicionar**.  
  
As propriedades a seguir estão disponíveis.

- **Serviço:** especifica o serviço de armazenamento ao qual se conectar.
- **Nome da conta:** especifica o nome da conta de armazenamento.
- **Autenticação:** especifica o método de autenticação a ser usado. Há suporte para autenticação com AccessKey, ServicePrincipal e SharedAccessSignature.
    - **AccessKey:** para esse método de autenticação, especifique a **chave de conta**.
    - **ServicePrincipal:** Para esse método de autenticação, especifique a **ID do aplicativo**, a **Chave do aplicativo** e a **ID do locatário** da entidade de serviço.
      Para que a **Conexão de teste** funcione, a entidade de serviço precisa ser atribuída pelo menos à função de **Leitor de Dados do Storage Blob** para a conta de armazenamento.
      Para obter mais informações, confira [Conceder acesso ao blob do Azure e dados de fila com RBAC no portal do Azure](/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal).
    - **SharedAccessSignature:** para esse método de autenticação, especifique pelo menos o **Token** da assinatura de acesso compartilhado.
      Para testar a conexão, especifique também o escopo de recurso a ser testado. Esse escopo pode ser o **Serviço**, o **Contêiner** ou o **Blob**.
      Para **Contêiner** e **Blob**, especifique o nome do contêiner e o caminho do blob, respectivamente.
      Para obter mais informações, confira [Visão geral da assinatura de acesso compartilhado do Armazenamento do Azure](/azure/storage/common/storage-sas-overview).
- **Ambiente:** especifica o ambiente de nuvem que hospeda a conta de armazenamento.

## <a name="managed-identities-for-azure-resources-authentication"></a>Identidades gerenciadas para autenticação de recursos do Azure
Ao executar pacotes SSIS no [Azure-SSIS Integration Runtime no Azure Data Factory](/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), você pode usar a [identidade gerenciada](/azure/data-factory/connector-azure-sql-database#managed-identity) associada ao data factory para a autenticação do armazenamento do Azure. O factory designado pode acessar dados do banco de dados e copiá-los para a conta de armazenamento usando essa identidade.

Saiba mais sobre a autenticação de armazenamento do Azure em geral em [Autenticar o acesso ao Armazenamento do Azure usando o Azure Active Directory](/azure/storage/common/storage-auth-aad). Para usar a autenticação de identidade gerenciada para o Armazenamento do Azure:

1. [Encontre a identidade gerenciada do data factory no portal do Azure](/azure/data-factory/data-factory-service-identity). Acesse as **Propriedades** do data factory. Copie a **ID do Aplicativo da Identidade Gerenciada** (não a **ID de Objeto da Identidade Gerenciada**).

1. Conceda à identidade gerenciada as devidas permissões em sua conta de armazenamento. Para obter mais detalhes sobre as funções, confira [Gerenciar direitos de acesso aos dados do Armazenamento do Azure com o RBAC](/azure/storage/common/storage-auth-aad-rbac-portal).

    - **Como origem**, em Controle de acesso (IAM), conceda, pelo menos, a função de **Leitor de Dados do Storage Blob**.
    - **Como destino**, em Controle de acesso (IAM), conceda, pelo menos, a função de **Colaborador de Dados do Storage Blob**.

Em seguida, configure a autenticação de identidade gerenciada do gerenciador de conexões de Armazenamento do Azure. Veja a seguir as opções para fazer isso:

- **Configurar em tempo de design.** No Designer SSIS, clique duas vezes no gerenciador de conexões de Armazenamento do Azure para abrir o **Editor do gerenciador de conexões do Armazenamento do Azure**. Selecione **Usar identidade gerenciada para autenticar no Azure**.
    > [!NOTE]
    >  Atualmente, essa opção não entra em vigor (indicando que a autenticação de identidade gerenciada não funciona) quando você executa o pacote SSIS no SSIS Designer ou no SQL Server [!INCLUDE[msCoName](../../includes/msconame-md.md)].
    
- **Configurar no runtime.** Ao executar o pacote via [SSMS (SQL Server Management Studio)](../ssis-quickstart-run-ssms.md) ou a [atividade Executar Pacote SSIS do Azure Data Factory](/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), localize o gerenciador de conexões do Armazenamento do Azure. Atualize sua propriedade `ConnectUsingManagedIdentity` para `True`.
    > [!NOTE]
    >  No Azure-SSIS Integration Runtime, todos os outros métodos de autenticação (por exemplo, chave de acesso e entidade de serviço) pré-configurados no gerenciador de conexões do Armazenamento do Azure serão substituídos quando a autenticação de identidade gerenciada for usada para operações de armazenamento.

> [!NOTE]
>  Para configurar a autenticação de identidade gerenciada em pacotes existentes, a maneira preferencial é recompilar seu projeto SSIS com o [Designer SSIS mais recente](../../ssdt/download-sql-server-data-tools-ssdt.md) pelo menos uma vez. Reimplante esse projeto SSIS para o Azure-SSIS Integration Runtime, para que a nova propriedade do gerenciador de conexões `ConnectUsingManagedIdentity` seja automaticamente adicionada a todos os gerenciadores de conexões Armazenamento do Azure no projeto SSIS. Como alternativa, pode-se usar diretamente uma substituição de propriedade com o caminho de propriedade **\Package.Connections [{nome do seu gerenciador de conexões}].Properties[ConnectUsingManagedIdentity]** no runtime.

## <a name="secure-network-traffic-to-your-storage-account"></a>Proteger o tráfego de rede na sua conta de armazenamento
O Azure Data Factory agora é um [serviço confiável da Microsoft](/azure/storage/common/storage-network-security#trusted-microsoft-services) para armazenamento do Azure. Quando você usa a autenticação de identidade gerenciada, é possível proteger sua conta de armazenamento [limitando o acesso às redes selecionadas](/azure/storage/common/storage-network-security#change-the-default-network-access-rule) enquanto ainda permite que o seu data factory acesse sua conta de armazenamento. Para saber mais, confira [Gerenciar exceções](/azure/storage/common/storage-network-security#managing-exceptions).

## <a name="see-also"></a>Confira também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)