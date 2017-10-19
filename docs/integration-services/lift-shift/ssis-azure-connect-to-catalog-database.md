---
title: "Conecte-se ao banco de dados de catálogo do SSISDB no Azure | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: ac121e600c3c616006d79892c50f796ca7cd6b3f
ms.contentlocale: pt-br
ms.lasthandoff: 10/13/2017

---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>Conecte-se ao banco de dados de catálogo do SSISDB no Azure

Obtenha as informações de conexão que você precisa se conectar ao banco de dados de catálogo do SSISDB hospedado em um servidor de banco de dados SQL. Você precisa dos seguintes itens para se conectar:
- nome totalmente qualificado do servidor
- Nome do banco de dados
- informações de logon 

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, verifique se que você tem a versão mais recente do SQL Server Management Studio ou 17.2. Para baixar a versão mais recente do SSMS, consulte [baixar o SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="get-the-connection-info-from-the-azure-portal"></a>Obter as informações de conexão do portal do Azure
1. Faça logon no [portal do Azure](https://portal.azure.com/).
2. No portal do Azure, selecione **bancos de dados SQL** no menu esquerdo e, em seguida, selecione o `SSISDB` banco de dados de **bancos de dados SQL** página. 
3. No **visão geral** página para o `SSISDB` de banco de dados, examine o nome totalmente qualificado do servidor, conforme mostrado na imagem a seguir. Passe o mouse sobre o nome do servidor para ativar o **clique para copiar** opção.

    ![Informações de conexão do servidor](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. Se você tiver esquecido as informações de logon para o servidor de banco de dados SQL, navegue até a página do banco de dados do SQL server. Lá você pode exibir o administrador do servidor nomear e, se necessário, redefinir a senha.

## <a name="connect-with-ssms"></a>Conecte-se com o SSMS
1. Abra o SQL Server Management Studio.

2. **Conectar ao servidor**. No **conectar ao servidor** caixa de diálogo, digite as seguintes informações:

   | Configuração       | Valor sugerido | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de Banco de Dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome totalmente qualificado do servidor | O nome deve estar neste formato: **mysqldbserver.database.windows.net**. |
   | **Autenticação** | Autenticação do SQL Server | Este guia de início rápido usa a autenticação do SQL. |
   | **Logon** | A conta de administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha para sua conta de administrador do servidor | Esta é a senha que você especificou quando criou o servidor. |

3. **Conecte-se ao banco de dados SSISDB**. Selecione **opções** para expandir o **conectar ao servidor** caixa de diálogo. Em expandidos **conectar ao servidor** caixa de diálogo, selecione o **propriedades de Conexão** guia. No **conectar-se ao banco de dados** campo, selecione ou digite `SSISDB`.

    > [!IMPORTANT]
    > Se você não selecionar `SSISDB` quando você se conectar, você poderá não ver o catálogo do SSIS no Pesquisador de objetos.

4. Em seguida, selecione **conectar**.

5. No Pesquisador de objetos, expanda **catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados de catálogo do SSIS.

## <a name="next-steps"></a>Próximas etapas
- Implante um pacote. Para obter mais informações, consulte [implantar um projeto do SSIS com o SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Execute um pacote. Para obter mais informações, consulte [executar um pacote do SSIS com o SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Agende um pacote. Para obter mais informações, consulte [SSIS de agendamento de execução de pacote no Azure](ssis-azure-schedule-packages.md)

