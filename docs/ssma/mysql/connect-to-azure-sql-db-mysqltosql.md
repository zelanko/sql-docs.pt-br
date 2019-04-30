---
title: Conectar-se ao banco de dados SQL do Azure (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 713a0ba96a2e82f10d4150b337d51f9f1774548f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253152"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Conectar-se ao BD SQL do Azure (MySQLToSQL)
Use a opção conectar à caixa de diálogo do SQL Azure para se conectar ao banco de dados do SQL Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo sobre o **arquivo** menu, selecione **conectar-se ao SQL Azure**. Se você tiver se conectado anteriormente, o comando é **reconectar-se ao SQL Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para se conectar ao SQL Azure.  
  
**Backup de banco de dados**  
  
Selecione, digite ou **procurar** o nome do banco de dados.  
  
> [!IMPORTANT]  
> SSMA para MySQL não oferece suporte a conexão ao banco de dados mestre no SQL Azure.  
  
**Nome de usuário**  
  
Insira o nome de usuário que usará o SSMA para se conectar ao banco de dados do SQL Azure  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**Encrypt**  
  
O SSMA recomenda conexão criptografada para o SQL Azure.  
  
## <a name="create-azure-database"></a>Criar banco de dados do Azure  
Se não houver nenhum banco de dados na conta do SQL Azure, você pode criar o banco de dados primeiro.  
  
Para criar um novo banco de dados pela primeira vez, siga as etapas a seguir  
  
1.  Clique no botão Procurar que está presente em conectar-se a caixa de diálogo do SQL Azure  
  
2.  Se não houver nenhum banco de dados, os seguintes itens de dois menu aparecem.  
  
    1.  **(nenhum banco de dados encontrado)**  que é desabilitado e esmaecido sempre  
  
    2.  **Criar novo banco de dados** que é habilitado somente quando não há nenhum banco de dados na conta do SQL Azure. Ao clicar neste item de menu, caixa de diálogo Criar banco de dados está presente com o tamanho e o nome do banco de dados.  
  
3.  No momento da criação do banco de dados, os dois parâmetros a seguir são fornecidos como entrada:  
  
    1.  **Nome do banco de dados:** Insira o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** Selecione o tamanho do banco de dados que você precisa criar na conta do SQL Azure.  
  
