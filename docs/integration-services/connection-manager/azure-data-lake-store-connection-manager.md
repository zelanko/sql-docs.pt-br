---
title: Gerenciador de conexões do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.openlocfilehash: 569341b07d373aaf1d0739a400537ca3b7998a80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66462643"
---
# <a name="azure-data-lake-store-connection-manager"></a>Gerenciador de conexões do Azure Data Lake Store

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Um pacote do SSIS (SQL Server Integration Services) pode usar o Gerenciador de Conexões do Azure Data Lake Store para se conectar a uma conta do Azure Data Lake Storage Gen1 com um dos dois tipos de autenticação a seguir:
-   Identidade do Usuário do Azure AD
-   Identidade do Serviço do Azure AD 

O Gerenciador de Conexões do Azure Data Lake Store é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

> [!NOTE]
> Para garantir que o Gerenciador de Conexões do Azure Data Lake Store e os componentes que o utilizam, isto é, a fonte do Data Lake Storage Gen1 e o destino do Data Lake Storage Gen1, possam se conectar aos serviços, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar o Gerenciador de conexões do Azure Data Lake Store

1.  Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS**, selecione **AzureDataLake** e selecione **Adicionar**. A caixa de diálogo **Editor de conexões do Azure Data Lake Store** se abre.
  
2.  Na caixa de diálogo **Editor do Gerenciador de Conexões do Azure Data Lake Store**, no campo **Host ADLS**, forneça a URL do host do Data Lake Storage Gen1. Por exemplo: `https://test.azuredatalakestore.net` ou `test.azuredatalakestore.net`.
  
3.  No campo **Autenticação**, escolha o tipo de autenticação apropriado para acessar os dados no Data Lake Storage Gen1.

    1.  Se você selecionou a opção de autenticação **Identidade de Usuário do Azure AD**, faça o seguinte:
        1. Forneça valores para os campos **Nome de Usuário** e **Senha**. 
    
        2. Selecione **Testar Conexão** para testar a conexão. Se você ou o administrador do locatário não consentiu anteriormente em permitir que o SSIS acessasse os dados do Data Lake Storage Gen1, selecione **Aceitar** quando solicitado. Para obter mais informações sobre esta experiência de consentimento, consulte [integrando aplicativos com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad).
    
        > [!NOTE] 
        > Quando você seleciona a opção de autenticação por **Identidade do Usuário do Azure AD**, a autenticação multifator e a autenticação por conta da Microsoft não têm suporte.
    
    2. Se você selecionou a opção de autenticação **Identidade do Serviço do Azure AD**, faça o seguinte:
        1. Crie uma entidade de serviço e um aplicativo do AAD (Azure Active Directory) para acessar os dados do Data Lake Storage Gen1.
    
        2. Atribua as permissões apropriadas para permitir que este aplicativo do AAD acesse seus recursos do Data Lake Storage Gen1. Para obter mais informações sobre essa opção de autenticação, consulte [Use o portal para criar a entidade de serviço e o aplicativo do Active Directory que pode acessar recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).
    
        3. Forneça valores para os campos **Id do cliente**, **Chave Secreta** e **Nome do Locatário**.
    
        4. Selecione **Testar Conexão** para testar a conexão.  
  
6.  Selecione **OK** para fechar a caixa de diálogo **Editor do Gerenciador de Conexões do Azure Data Lake Store**.  

## <a name="view-the-properties-of-the-connection-manager"></a>Exibir as propriedades do gerenciador de conexões
Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .  
  
  
