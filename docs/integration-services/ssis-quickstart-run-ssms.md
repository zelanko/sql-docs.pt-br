---
title: Executar um pacote do SSIS com o SSMS | Microsoft Docs
ms.date: 09/25/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ec5b6f4e368b52f849a22d014da21dd14e5e1090
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>Executar um pacote do SSIS com o SSMS (SQL Server Management Studio)
Este guia de início rápido demonstra como usar o SSMS (SQL Server Management Studio) para se conectar ao banco de dados do Catálogo do SSIS e, em seguida, executar um pacote do SSIS por meio do Pesquisador de Objetos no SSMS.

O SQL Server Management Studio é um ambiente integrado para gerenciar qualquer infraestrutura do SQL, do SQL Server ao Banco de Dados SQL. Para obter mais informações sobre o SSMS, consulte [SSMS (SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Prerequisites

Antes de começar, verifique se você tem a última versão do SSMS (SQL Server Management Studio). Para baixar o SSMS, consulte [Baixar o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Conectar-se ao banco de dados SSISDB

Use o SQL Server Management Studio para estabelecer uma conexão com o Catálogo do SSIS. 

> [!NOTE]
> Um servidor de Banco de Dados SQL do Azure escuta na porta 1433. Se estiver tentando se conectar a um servidor de Banco de Dados SQL do Azure em um firewall corporativo, essa porta deverá estar aberta no firewall corporativo para que você se conecte com êxito.

1. Abra o SQL Server Management Studio.

2. Na caixa de diálogo **Conectar-se ao Servidor**, insira as seguintes informações:

   | Configuração       | Valor sugerido | Obter mais informações | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Mecanismo de banco de dados | Esse valor é necessário. |
   | **Nome do servidor** | O nome do servidor totalmente qualificado | Se estiver se conectando a um servidor de Banco de Dados SQL do Azure, o nome estará neste formato: `<server_name>.database.windows.net`. |
   | **Autenticação** | Autenticação do SQL Server | Este guia de início rápido usa a autenticação do SQL. |
   | **Logon** | A conta do administrador do servidor | Essa é a conta que você especificou quando criou o servidor. |
   | **Senha** | A senha de sua conta do administrador do servidor | Essa é a senha que você especificou quando criou o servidor. |

3. Clique em **Conectar**. A janela Pesquisador de Objetos será aberta no SSMS. 

4. No Pesquisador de Objetos, expanda **Catálogos do Integration Services** e, em seguida, expanda **SSISDB** para exibir os objetos no banco de dados do Catálogo do SSIS.

## <a name="run-a-package"></a>Executar um pacote

1. No Pesquisador de Objetos, selecione o pacote que você deseja executar.

2. Clique com o botão direito do mouse e selecione **Executar**. A caixa de diálogo **Executar Pacote** se abre.

3.  Configure a execução de pacote usando as configurações nas guias **Parâmetros**, **Gerenciadores de Conexões** e **Avançado** na caixa de diálogo Executar Pacote.

4.  Clique em OK para executar o pacote.

## <a name="next-steps"></a>Próximas etapas
- Considere outras maneiras de executar um pacote.
    - [Executar um pacote do SSIS com o Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Executar um pacote do SSIS com o Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Executar um pacote do SSIS no prompt de comando](./ssis-quickstart-run-cmdline.md)
    - [Executar um pacote do SSIS com o PowerShell](ssis-quickstart-run-powershell.md)
    - [Executar um pacote do SSIS com o C#](./ssis-quickstart-run-dotnet.md) 
