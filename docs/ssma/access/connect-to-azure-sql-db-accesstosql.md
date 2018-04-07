---
title: Conecte-se ao banco de dados do SQL Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 511c652a221ffb3fe4392dd8f4c365de129efe13
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Conecte-se ao banco de dados do SQL Azure (AccessToSQL)
Use a conectar-se a caixa de diálogo do SQL Azure para se conectar ao banco de dados do SQL Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no **arquivo** menu, selecione **conectar-se ao SQL Azure**. Se você se conectou anteriormente, o comando é **reconectar-se ao SQL Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para conectar-se ao SQL Azure.  
  
**Banco de dados**  
  
Selecione, digite ou **procurar** o nome do banco de dados.  
  
> [!IMPORTANT]  
> O SSMA para Access não dá suporte a conexão ao banco de dados mestre no SQL Azure.  
  
**Nome de usuário**  
  
Insira o nome de usuário SSMA usará para se conectar ao banco de dados do SQL Azure  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**Encrypt**  
  
O SSMA recomenda conexão criptografada para o SQL Azure.  
  
## <a name="create-azure-database"></a>Criar banco de dados do Azure  
Para criar um novo banco de dados do azure, siga as etapas a seguir  
  
1.  Clique no botão Procurar que está presente em conectar-se a caixa de diálogo do SQL Azure  
  
2.  Se não houver nenhum banco de dados, dois itens de menu aparecem  
  
    1.  **(nenhum banco de dados encontrado)**  que é desabilitado ou esmaecido sempre  
  
    2.  **Criar novo banco de dados** que está sempre habilitado, permitindo que o usuário crie um novo banco de dados do azure na conta do SQL Azure. Ao clicar neste item de menu, criar caixa de diálogo banco de dados do azure está presente com o nome do banco de dados e tamanho.  
  
3.  No momento da criação do banco de dados, esses dois parâmetros é fornecido como entrada.  
  
    1.  **Nome do banco de dados:** digite o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** selecione o tamanho do banco de dados que você precisa criar na conta do SQL Azure.  
  
