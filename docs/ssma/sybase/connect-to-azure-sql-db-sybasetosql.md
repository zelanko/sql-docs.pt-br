---
title: Conecte-se ao banco de dados do SQL Azure (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1267aecb68c344b6de0fad2c7c129a0b6ab2205c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>Conecte-se ao banco de dados do SQL Azure (SybaseToSQL)
Use a conectar-se a caixa de diálogo banco de dados do Azure SQL para se conectar ao banco de dados Azure SQL DB que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no **arquivo** menu, selecione **conectar-se ao banco de dados do Azure SQL**. Se você se conectou anteriormente, o comando é **reconectar-se ao banco de dados de SQL do Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para se conectar ao banco de dados de SQL do Azure.  
  
**Backup de banco de dados**  
  
Selecione, digite ou **procurar** o nome do banco de dados.  
  
> [!IMPORTANT]  
> SSMA para Sybase não oferece suporte a conexão ao banco de dados mestre no banco de dados de SQL do Azure.  
  
**User name**  
  
Insira o nome de usuário SSMA usará para se conectar ao banco de dados do banco de dados de SQL do Azure  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**Criptografar**  
  
O SSMA recomenda conexão criptografada para o banco de dados do Azure SQL.  
  
## <a name="create-azure-database"></a>Criar banco de dados do Azure  
Se não houver nenhum banco de dados na conta de banco de dados de SQL do Azure, você pode criar o primeiro banco de dados.  
  
Para criar um novo banco de dados pela primeira vez, siga as etapas a seguir  
  
1.  Clique no botão Procurar que está presente em conectar-se a caixa de diálogo banco de dados de SQL do Azure  
  
2.  Se não houver nenhum banco de dados, os seguintes itens de dois menu aparecem.  
  
    1.  **(nenhum banco de dados encontrado)**  que é desabilitado ou esmaecido sempre  
  
    2.  **Criar novo banco de dados** que é habilitado apenas quando não há nenhum banco de dados na conta de banco de dados de SQL do Azure. Ao clicar neste item de menu, caixa de diálogo Criar banco de dados do Azure está presente com o nome do banco de dados e tamanho.  
  
3.  No momento da criação do banco de dados, os dois parâmetros a seguir recebem como entrada:  
  
    1.  **Nome do banco de dados:** digite o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** selecione o tamanho do banco de dados que você precisa criar conta de banco de dados de SQL do Azure.  
  
