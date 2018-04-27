---
title: Conectar-se ao banco de dados do Catálogo do SSISDB no Azure | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c9316c291ac650628bff880303c49822eca99700
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>Conectar-se ao banco de dados do Catálogo do SSISDB no Azure

Obtenha as informações de conexão necessárias para se conectar ao banco de dados de catálogo SSISDB hospedado no servidor de Banco de Dados SQL do Azure. Você precisa dos seguintes itens para se conectar:
- nome do servidor totalmente qualificado
- nome do banco de dados
- informações de logon 

> [!IMPORTANT]
> No momento, não é possível criar o banco de dados do Catálogo do SSISDB no Banco de Dados SQL do Azure, independentemente da criação do Azure-SSIS Integration Runtime no Azure Data Factory versão 2. É o Azure-SSIS IR que executa pacotes do SSIS no Azure. Para obter mais informações, consulte [Implantar pacotes do SSIS para o Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal). 

## <a name="prerequisites"></a>Prerequisites
Antes de começar, verifique se você tem a versão 17.2 ou posterior do SSMS (SQL Server Management Studio). Se o banco de dados de catálogo do SSISDB estiver hospedado na Instância Gerenciada do Banco de Dados SQL (versão prévia), verifique se você tem a versão 17.6 ou posterior do SSMS. Para baixar a versão mais recente do SSMS, veja [Baixar o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="get-the-connection-info-from-the-azure-portal"></a>Obter as informações de conexão do Portal do Azure
1. Faça logon no [portal do Azure](https://portal.azure.com/).
2. No Portal do Azure, selecione **Bancos de Dados SQL** no menu à esquerda e selecione o banco de dados `SSISDB` na página **Bancos de dados SQL**. 
3. Na página **Visão geral** do banco de dados `SSISDB`, examine o nome totalmente qualificado do servidor conforme mostrado na imagem a seguir. Para mostrar a opção **Clique para copiar**, passe o mouse sobre o nome do servidor.

    ![Informações de conexão do servidor](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. Se você tiver esquecido as informações de logon para o servidor de Banco de Dados SQL, navegue até a página do servidor de Banco de Dados SQL. Lá você pode exibir o nome do administrador do servidor e, se necessário, redefinir a senha.

## <a name="connect-with-ssms"></a>Conectar-se ao SSMS
1. Abra o SQL Server Management Studio.

2. **Conecte-se ao servidor**. Na caixa de diálogo **Conectar-se ao Servidor**, insira as seguintes informações:

   | Configuração       | Valor sugerido | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de Banco de Dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome do servidor totalmente qualificado | O nome deve estar neste formato: **mysqldbserver.database.windows.net**. |
   | **Autenticação** | Autenticação do SQL Server | Este guia de início rápido usa a autenticação do SQL. |
   | **Logon** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |

    ![Conectar-se ao servidor com o SSMS](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-1.png)

3. **Conecte-se ao banco de dados SSISDB**. Selecione **Opções** para expandir a caixa de diálogo **Conectar ao Servidor**. Na caixa de diálogo **conectar ao servidor**, selecione a guia **Propriedades de Conexão**. No campo **Conectar-se ao banco de dados**, selecione ou insira `SSISDB`.

    > [!IMPORTANT]
    > Se você não selecionar `SSISDB` quando se conectar, você poderá não ver o Catálogo do SSIS no Pesquisador de Objetos.

    ![Selecionar o banco de dados SSISDB para a conexão](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-2.png)

4. Depois, selecione **Conectar**.

5. No Pesquisador de Objetos, expanda **Catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados do Catálogo do SSIS.

    ![Localizar o banco de dados SSISDB no Pesquisador de Objetos do SSMS](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-3.png)

## <a name="next-steps"></a>Próximas etapas
- Implante um pacote. Para obter mais informações, consulte [Implantar um projeto do SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-deploy-ssms.md).
- Execute um pacote. Para obter mais informações, consulte [Executar um pacote SSIS com o SSMS (SQL Server Management Studio)](../ssis-quickstart-run-ssms.md).
- Agende um pacote. Para obter mais informações, consulte [Agendar execução de pacote SSIS no Azure](ssis-azure-schedule-packages.md)
