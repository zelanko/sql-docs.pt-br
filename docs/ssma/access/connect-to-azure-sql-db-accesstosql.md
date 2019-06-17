---
title: Conectar-se ao banco de dados SQL do Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 57a745385de80a3040897310ddc5b43b1301ea86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63138748"
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Conectar-se ao banco de dados SQL do Azure (AccessToSQL)
Use a opção conectar à caixa de diálogo do SQL Azure para se conectar ao banco de dados do SQL Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo sobre o **arquivo** menu, selecione **conectar-se ao SQL Azure**. Se você tiver se conectado anteriormente, o comando é **reconectar-se ao SQL Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para se conectar ao SQL Azure.  
  
**Backup de banco de dados**  
  
Selecione, digite ou **procurar** o nome do banco de dados.  
  
> [!IMPORTANT]  
> O SSMA para Access não dá suporte a conexão ao banco de dados mestre no SQL Azure.  
  
**Nome de usuário**  
  
Insira o nome de usuário que usará o SSMA para se conectar ao banco de dados do SQL Azure  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**Encrypt**  
  
O SSMA recomenda conexão criptografada para o SQL Azure.  
  
## <a name="create-azure-database"></a>Criar banco de dados do Azure  
Para criar um novo banco de dados do azure, siga as etapas a seguir  
  
1.  Clique no botão Procurar que está presente em conectar-se a caixa de diálogo do SQL Azure  
  
2.  Se não houver nenhum banco de dados, dois itens de menu aparecem  
  
    1.  **(nenhum banco de dados encontrado)**  que é desabilitado e esmaecido sempre  
  
    2.  **Criar novo banco de dados** que está sempre habilitado, permitindo que o usuário criar um novo banco de dados do azure na conta do SQL Azure. Ao clicar neste item de menu, criar caixa de diálogo banco de dados do azure está presente com o nome do banco de dados e tamanho.  
  
3.  No momento da criação do banco de dados, esses dois parâmetros é dado como entrada.  
  
    1.  **Nome do banco de dados:** Insira o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** Selecione o tamanho do banco de dados que você precisa criar na conta do SQL Azure.  
  
