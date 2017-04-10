---
title: "Gerenciador de conex&#245;es do Azure Data Lake Store | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.DTS.DESIGNER.AFPADLSCM.F1"
  - "sql14.dts.designer.afpadlscm.f1"
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Gerenciador de conex&#245;es do Azure Data Lake Store
  O **Gerenciador de conexões de Azure Data Lake Store** permite que um pacote SSIS se conecte a um serviço do Azure Data Lake Store por meio de dois tipos de autenticação: identidade de usuário do Azure AD e a identidade de serviço do Azure AD.  
  
 O **Gerenciador de conexões de Azure Data Lake Store** é um componente do Feature Pack do SSIS (SQL Server Integration Services) para Azure do SQL Server 2016. Baixe o Feature Pack [daqui](http://go.microsoft.com/fwlink/?LinkID=626967).  

>   [!NOTE] Para garantir que o Gerenciador de conexões do Azure Data Lake Store e os componentes que o utilizam, isto é, a Fonte do Azure Data Lake Store e o Destino do Azure Data Lake Store, possam se conectar aos serviços, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar o Gerenciador de conexões do Azure Data Lake Store

 
1.  Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS**, selecione **AzureDataLake**e clique em **Adicionar**.  
  
2.  Na caixa de diálogo Editor de Gerenciador de conexões do Azure Data Lake Store, digite a URL do host do armazenamento do Azure Data Lake Store no campo **Host ADLS**. Por exemplo: https://test.azuredatalakestore.net ou test.azuredatalakestore.net.
  
3.  Escolha o tipo de autenticação correspondente para acessar dados do Azure Data Lake Store.

    1.  Se você selecionou a opção de autenticação por **identidade de usuário do Azure AD**, faça o seguinte:
        1. Especifique os valores para o **nome de usuário** e o campo de **senha**. 
    
        2. Clique no botão **Testar Conexão** para testar a conexão. Se você e o administrador de locatários não deixaram SSIS acessar os dados do Azure Data Lake Store antes, você precisará clicar no botão **Aceitar** para SSIS acessar os dados do Azure Data Lake Store na caixa de diálogo. Para obter mais informações sobre esta experiência de consentimento, consulte [integrando aplicativos com o Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] Para a opção de autenticação por Identidade do Usuário do Azure AD, a autenticação multifator e a conta da Microsoft não têm suporte.
    
    2. Se você selecionou a opção de autenticação por **identidade de serviço do Azure AD**, faça o seguinte:
        1. Crie um aplicativo AAD e uma entidade de serviço que pode acessar os recursos do Azure Data Lake.
    
        2. Atribua este aplicativo AAD correspondente permissões para acessar os recursos do Azure Data Lake. Para obter mais informações sobre essa opção de autenticação, consulte [Use o portal para criar a entidade de serviço e o aplicativo do Active Directory que pode acessar recursos](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal).
    
        3. Especifique valores para **Id do cliente**, **chave secreta** e **nome do locatário**.
    
        4. Clique no botão **Testar Conexão** para testar a conexão.  
  
6.  Clique em **OK** para fechar a caixa de diálogo.  
  
    Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .  
  
  