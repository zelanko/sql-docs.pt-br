---
title: Conectar-se ao BD SQL do Azure (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 0b26ddaef1373544e0df2fd9186cdf56fdafd801
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68040634"
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>Conectar-se ao BD SQL do Azure (AccessToSQL)
Use a caixa de diálogo Conectar-se a SQL Azure para se conectar ao banco de dados do SQL Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no menu **arquivo** , selecione **conectar-se a SQL Azure**. Se você tiver se conectado anteriormente, o comando será **reconectado a SQL Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para se conectar ao SQL Azure.  
  
**Backup de banco de dados**  
  
Selecione, insira ou **procure** o nome do banco de dados.  
  
> [!IMPORTANT]  
> O SSMA para Access não oferece suporte à conexão com o banco de dados mestre no SQL Azure.  
  
**Nome de usuário**  
  
Insira o nome de usuário que o SSMA usará para se conectar ao banco de dados de SQL Azure  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**Encrypt**  
  
O SSMA recomenda a conexão criptografada com SQL Azure.  
  
## <a name="create-azure-database"></a>Criar banco de dados do Azure  
Para criar um novo banco de dados do Azure, siga as etapas a seguir  
  
1.  Clique no botão procurar que está presente na caixa de diálogo conectar a SQL Azure  
  
2.  Se não houver bancos de dados, serão exibidos dois itens de menu  
  
    1.  **(nenhum banco de dados encontrado)** que está desabilitado e esmaecido o tempo todo  
  
    2.  **Crie um novo banco de dados** que esteja sempre habilitado, permitindo que o usuário crie um novo banco de dados do azure em SQL Azure conta. Ao clicar nesse item de menu, a caixa de diálogo Criar banco de dados do Azure está presente com o nome e o tamanho do banco de dados.  
  
3.  No momento da criação do banco de dados, esses dois parâmetros são fornecidos como entrada.  
  
    1.  **Nome do banco de dados:** Insira o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** Selecione o tamanho do banco de dados que você precisa criar na conta SQL Azure.  
  
