---
title: Conecte-se ao banco de dados do SQL Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
ms.openlocfilehash: d61eab04dffa1723c6d77a118033eee535a917e2
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773442"
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Conecte-se ao banco de dados do SQL Azure (AccessToSQL)
Use a conectar-se a caixa de diálogo do SQL Azure para se conectar ao banco de dados do SQL Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no **arquivo** menu, selecione **conectar-se ao SQL Azure**. Se você se conectou anteriormente, o comando é **reconectar-se ao SQL Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para conectar-se ao SQL Azure.  
  
**Backup de banco de dados**  
  
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
  
