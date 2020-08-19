---
description: Conectar-se ao banco de dados SQL do Azure (AccessToSQL)
title: Conectar-se ao banco de dados SQL do Azure (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 15882852544113881b52f3641e0c85ec684add22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418562"
---
# <a name="connect-to-azure-sql-database-accesstosql"></a>Conectar-se ao banco de dados SQL do Azure (AccessToSQL)
Use a caixa de diálogo conectar a SQL Azure para se conectar ao banco de dados no banco de dados SQL do Azure que você deseja migrar.  
  
Para acessar essa caixa de diálogo, no menu **arquivo** , selecione **conectar-se a SQL Azure**. Se você tiver se conectado anteriormente, o comando será **reconectado a SQL Azure.**  
  
## <a name="options"></a>Opções  
**Nome do servidor**  
  
Selecione ou insira o nome do servidor para se conectar ao SQL Azure.  
  
**Banco de dados**  
  
Selecione, insira ou **procure** o nome do banco de dados.  
  
> [!IMPORTANT]  
> O SSMA para Access não oferece suporte à conexão com o banco de dados mestre no SQL Azure.  
  
**Nome de usuário**  
  
Insira o nome de usuário que o SSMA usará para se conectar ao banco de dados SQL do Azure  
  
**Senha**  
  
Digite a senha para o nome de usuário.  
  
**Encrypt**  
  
O SSMA recomenda a conexão criptografada com SQL Azure.  
  
## <a name="create-database"></a>Criar banco de dados  
Para criar um novo banco de dados, siga as etapas a seguir  
  
1.  Clique no botão procurar que está presente na caixa de diálogo conectar a SQL Azure  
  
2.  Se não houver bancos de dados, serão exibidos dois itens de menu  
  
    1.  **(nenhum banco de dados encontrado)** que está desabilitado e esmaecido o tempo todo  
  
    2.  **Crie um novo banco de dados** que esteja sempre habilitado, permitindo que o usuário crie um novo banco de dados. Ao clicar nesse item de menu, a caixa de diálogo Criar banco de dados estará presente com o nome e o tamanho do banco de dados.  
  
3.  No momento da criação do banco de dados, esses dois parâmetros são fornecidos como entrada.  
  
    1.  **Nome do banco de dados:** Insira o nome do banco de dados.  
  
    2.  **Tamanho do banco de dados:** Selecione o tamanho do banco de dados que você precisa criar na conta SQL Azure.  
  
