---
title: Conecte-se ao banco de dados do SQL Azure (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d28b5df73e5c22bfd3651aa36190e0ce9179777d
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34775892"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Conecte-se ao banco de dados do SQL Azure (MySQLToSQL)
Use a conectar-se a caixa de diálogo do SQL Azure para se conectar ao banco de dados do SQL Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no **arquivo** menu, selecione **conectar-se ao SQL Azure**. Se você se conectou anteriormente, o comando é **reconectar-se ao SQL Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para conectar-se ao SQL Azure.  
  
**Backup de banco de dados**  
  
Selecione, digite ou **procurar** o nome do banco de dados.  
  
> [!IMPORTANT]  
> SSMA para MySQL não oferece suporte a conexão ao banco de dados mestre no SQL Azure.  
  
**Nome de usuário**  
  
Insira o nome de usuário SSMA usará para se conectar ao banco de dados do SQL Azure  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**Encrypt**  
  
O SSMA recomenda conexão criptografada para o SQL Azure.  
  
## <a name="create-azure-database"></a>Criar banco de dados do Azure  
Se não houver nenhum banco de dados na conta do SQL Azure, você pode criar o primeiro banco de dados.  
  
Para criar um novo banco de dados pela primeira vez, siga as etapas a seguir  
  
1.  Clique no botão Procurar que está presente em conectar-se a caixa de diálogo do SQL Azure  
  
2.  Se não houver nenhum banco de dados, os seguintes itens de dois menu aparecem.  
  
    1.  **(nenhum banco de dados encontrado)**  que é desabilitado ou esmaecido sempre  
  
    2.  **Criar novo banco de dados** que é habilitado apenas quando não há nenhum banco de dados na conta do SQL Azure. Ao clicar neste item de menu, caixa de diálogo Criar banco de dados do Azure está presente com o nome do banco de dados e tamanho.  
  
3.  No momento da criação do banco de dados, os dois parâmetros a seguir recebem como entrada:  
  
    1.  **Nome do banco de dados:** digite o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** selecione o tamanho do banco de dados que você precisa criar na conta do SQL Azure.  
  
