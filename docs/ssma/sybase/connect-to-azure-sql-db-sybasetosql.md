---
description: Conectar-se ao banco de dados SQL do Azure (SybaseToSQL)
title: Conectar-se ao banco de dados SQL do Azure (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3717cce895ca602a550d47ea5c569af4c80963a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492309"
---
# <a name="connect-to-azure-sql-database--sybasetosql"></a>Conectar-se ao banco de dados SQL do Azure (SybaseToSQL)
Use a caixa de diálogo conectar ao banco de dados SQL do Azure para se conectar ao banco de dados do banco de dados SQL do Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no menu **arquivo** , selecione **conectar ao banco de dados SQL do Azure**. Se você tiver se conectado anteriormente, o comando será **reconectado ao banco de dados SQL do Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para se conectar ao banco de dados SQL do Azure.  
  
**Banco de dados**  
  
Selecione, insira ou **procure** o nome do banco de dados.  
  
> [!IMPORTANT]  
> O SSMA para Sybase não oferece suporte à conexão com o banco de dados mestre no banco de dados SQL do Azure.  
  
**Nome de usuário**  
  
Insira o nome de usuário que o SSMA usará para se conectar ao banco de dados do banco de dados SQL do Azure  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**Encrypt**  
  
O SSMA recomenda a conexão criptografada com o banco de dados SQL do Azure.  
  
## <a name="create-azure-database"></a>Criar banco de dados do Azure  
Se não houver nenhum banco de dados na conta do Azure SQL Database, você poderá criar o primeiro banco de dados.  
  
Para criar um novo banco de dados pela primeira vez, siga as etapas a seguir  
  
1.  Clique no botão procurar que está presente na caixa de diálogo conectar ao banco de dados SQL do Azure  
  
2.  Se não houver bancos de dados, os dois itens de menu a seguir serão exibidos.  
  
    1.  **(nenhum banco de dados encontrado)** que está desabilitado e esmaecido o tempo todo  
  
    2.  **Crie um novo banco de dados** que esteja habilitado somente quando não houver bancos de dados na conta do banco de dados SQL do Azure. Ao clicar nesse item de menu, a caixa de diálogo Criar banco de dados do Azure está presente com o nome e o tamanho do banco de dados.  
  
3.  No momento da criação do banco de dados, os dois parâmetros a seguir são fornecidos como entrada:  
  
    1.  **Nome do banco de dados:** Insira o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** Selecione o tamanho do banco de dados que você precisa criar na conta do banco de dados SQL do Azure.  
  
