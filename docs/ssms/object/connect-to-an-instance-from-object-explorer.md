---
title: Conectar ao SQL Server ou ao Banco de Dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fa363c2715057a0f81a691911a7e06b5104c5501
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65088752"
---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>Conectar ao SQL Server ou ao Banco de Dados SQL do Azure

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Para trabalhar com servidores e bancos de dados, primeiro é preciso conectar-se ao servidor. É possível conectar-se a vários servidores ao mesmo tempo.

O [SSMS (SQL Server Management Studio)](../download-sql-server-management-studio-ssms.md) dá suporte a vários tipos de conexões. Este artigo fornece detalhes para a conexão ao SQL Server e ao Banco de Dados SQL do Azure (conexão a um único banco de dados ou pool elástico do Azure SQL). Para obter informações sobre as outras opções de conexão, consulte os [links](#see-also) na parte inferior desta página.
  
## <a name="connecting-to-a-server"></a>Conectando a um servidor  

1. Em **Pesquisador de Objetos**, clique em **Conectar > Mecanismo de Banco de Dados...**.

   ![connect](../media/connect-to-server/connect-db-engine.png)

1. Preencha o formulário **Conectar ao Servidor** e clique em **Conectar**:

   ![conectar ao servidor](../media/connect-to-server/connect.png)

1. Se estiver conectando-se a um Azure SQL Server, talvez será necessário entrar para criar uma regra de firewall. Clique em **Entrar...** (caso contrário, vá para a etapa 6 abaixo)

   ![firewall](../media/connect-to-server/firewall-rule-sign-in.png)

1. Depois de entrar com êxito, o formulário é preenchido previamente com o seu endereço IP específico. Se o seu endereço IP é alterado com frequência, pode ser mais fácil permitir acesso a um intervalo, portanto selecione a opção mais adequada ao seu ambiente. 

   ![firewall](../media/connect-to-server/new-firewall-rule.png)

1. Para criar a regra de firewall e conectar-se ao servidor, clique em **OK**.

1. Após a conexão ser bem-sucedida, o servidor aparecerá no **Pesquisador de Objetos**:

   ![conectado](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>Next Steps

[Projetar, criar e atualizar tabelas](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>Consulte Também

[SSMS (SQL Server Management Studio)](../sql-server-management-studio-ssms.md)  
[Baixar o SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)  
[Serviços de Integração](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)  
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)  
[Armazenamento do Azure](../f1-help/connect-to-microsoft-azure-storage.md)  
