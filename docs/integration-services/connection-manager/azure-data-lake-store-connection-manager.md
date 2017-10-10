---
title: "Gerenciador de Conexão do repositório Azure Data Lake | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 5acf2de3fccc2f5180358f87bd02591811c59c72
ms.contentlocale: pt-br
ms.lasthandoff: 10/10/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Gerenciador de conexões do Azure Data Lake Store
Um pacote do SQL Server Integration Services (SSIS) pode usar o Gerenciador de conexão do repositório Azure Data Lake para se conectar a um serviço de repositório Azure Data Lake com um dos seguintes dois tipos de autenticação:
-   Identidade de usuário do AD do Azure
-   Identidade de serviço do AD do Azure 

O Gerenciador de conexão do repositório Azure Data Lake é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

>   [!NOTE]
> Para garantir que o Gerenciador de conexões do Azure Data Lake Store e os componentes que o utilizam, isto é, a Fonte do Azure Data Lake Store e o Destino do Azure Data Lake Store, possam se conectar aos serviços, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar o Gerenciador de conexões do Azure Data Lake Store

1.  No **adicionar Gerenciador de Conexão SSIS** caixa de diálogo, selecione **AzureDataLake**e, em seguida, selecione **adicionar**. O **Editor do Gerenciador de Conexão do Azure Data Lake repositório** caixa de diálogo é aberta.
  
2.  No **Editor do Gerenciador de Conexão do Azure Data Lake repositório** na caixa de **ADLS Host** campo, forneça a URL de host do repositório Azure Data Lake. Por exemplo: `https://test.azuredatalakestore.net` ou `test.azuredatalakestore.net`.
  
3.  No **autenticação** campo, escolha o tipo de autenticação apropriado para acessar os dados no repositório Azure Data Lake.

    1.  Se você selecionar o **identidade de usuário do AD do Azure** autenticação opção, faça o seguinte:
        1. Forneça valores para o **nome de usuário** e **senha** campos. 
    
        2. Para testar a conexão, selecione **Testar Conexão**. Se você ou o administrador de inquilinos anteriormente não consentimento para permitir que o SSIS para acessar os dados do repositório Azure Data Lake, selecione **aceitar** quando solicitado. Para obter mais informações sobre esta experiência de consentimento, consulte [integrando aplicativos com o Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Quando você seleciona o **identidade de usuário do AD do Azure** opção authentication, autenticação multifator e autenticação de conta da Microsoft não são suportados.
    
    2. Se você selecionar o **identidade de serviço do AD do Azure** autenticação opção, faça o seguinte:
        1. Crie um aplicativo do Azure Active Directory (AAD) e o serviço principal para acessar os dados do Azure Data Lake.
    
        2. Atribua permissões apropriadas para permitir que este aplicativo AAD acessar os recursos do Azure Data Lake. Para obter mais informações sobre essa opção de autenticação, consulte [Use o portal para criar a entidade de serviço e o aplicativo do Active Directory que pode acessar recursos](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal).
    
        3. Forneça valores para o **Id do cliente**, **chave secreta**, e **nome do locatário** campos.
    
        4. Para testar a conexão, selecione **Testar Conexão**.  
  
6.  Selecione **Okey** para fechar o **Editor do Gerenciador de Conexão do Azure Data Lake repositório** caixa de diálogo.  
  
Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .  
  
  
