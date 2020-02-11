---
title: Conectar-se ao BD SQL do Azure (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 81623d27-25af-444f-9779-1edb8c6fb470
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 12da1aa42f468b92e1833410e635183aabf3a384
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103240"
---
# <a name="connect-to-azure-sql-db-mysqltosql"></a>Conectar-se ao BD SQL do Azure (MySQLToSQL)
Use a caixa de diálogo Conectar-se a SQL Azure para se conectar ao banco de dados do SQL Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no menu **arquivo** , selecione **conectar-se a SQL Azure**. Se você tiver se conectado anteriormente, o comando será **reconectado a SQL Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para se conectar ao SQL Azure.  
  
**Backup de banco de dados**  
  
Selecione, insira ou **procure** o nome do banco de dados.  
  
> [!IMPORTANT]  
> O SSMA para MySQL não dá suporte à conexão com o banco de dados mestre no SQL Azure.  
  
**Nome de usuário**  
  
Insira o nome de usuário que o SSMA usará para se conectar ao banco de dados de SQL Azure  
  
**Senha**  
  
Insira a senha para o nome de usuário.  
  
**Criptografe**  
  
O SSMA recomenda a conexão criptografada com SQL Azure.  
  
## <a name="create-azure-database"></a>Criar banco de dados do Azure  
Se não houver nenhum banco de dados na conta de SQL Azure, você poderá criar o primeiro.  
  
Para criar um novo banco de dados pela primeira vez, siga as etapas a seguir  
  
1.  Clique no botão procurar que está presente na caixa de diálogo conectar a SQL Azure  
  
2.  Se não houver bancos de dados, os dois itens de menu a seguir serão exibidos.  
  
    1.  **(nenhum banco de dados encontrado)** que está desabilitado e esmaecido o tempo todo  
  
    2.  **Crie um novo banco de dados** que esteja habilitado somente quando não houver bancos de dados na conta SQL Azure. Ao clicar nesse item de menu, a caixa de diálogo Criar banco de dados do Azure está presente com o nome e o tamanho do banco de dados.  
  
3.  No momento da criação do banco de dados, os dois parâmetros a seguir são fornecidos como entrada:  
  
    1.  **Nome do banco de dados:** Insira o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** Selecione o tamanho do banco de dados que você precisa criar na conta SQL Azure.  
  
