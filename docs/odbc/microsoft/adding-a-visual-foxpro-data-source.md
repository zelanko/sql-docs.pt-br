---
description: Adicionar uma fonte de dados do Visual FoxPro
title: Adicionando uma fonte de dados do Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22ac95b51d543ca223148b169b53acb9c334d9f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494799"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Adicionar uma fonte de dados do Visual FoxPro
Para acessar dados do Visual FoxPro do seu aplicativo, você deve ter uma fonte de dados. Você pode criar uma fonte de dados da seguinte maneira:  
  
-   Em um aplicativo, como o Microsoft® Word, o Microsoft Excel ou o Microsoft Access, que usa drivers ODBC.  
  
-   Fora de seu aplicativo, usando o painel de controle do Microsoft Windows® 95, Microsoft Windows 98 ou Microsoft Windows NT®/Windows 2000.  
  
 Depois que uma fonte de dados existir no seu sistema, você poderá reutilizar a mesma fonte de dados sempre que desejar acessar os dados do Visual FoxPro. Se você tiver vários bancos de dados ou tabelas diferentes que deseja acessar, você poderá criar uma fonte de dados separada para cada banco de dado ou diretório.  
  
 O procedimento a seguir cria uma fonte de dados usando o painel de controle. Para obter mais informações sobre como criar uma fonte de dados de um aplicativo, consulte [acessando dados do Visual FoxPro do Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Para adicionar uma fonte de dados do Visual FoxPro  
  
1.  Em computadores que executam o Windows 2000, abra o painel de controle do Windows e clique duas vezes em ferramentas administrativas.  
  
2.  Clique duas vezes em fontes de dados (ODBC) para abrir a caixa de diálogo administrador de fonte de dados ODBC. Esse ícone estará disponível depois que você tiver instalado o driver ODBC do Visual FoxPro ou qualquer software de driver ODBC.  
  
    > [!NOTE]  
    >  Se você estiver executando uma versão anterior do Windows, abra o painel de controle do Windows e clique duas vezes em ODBC de 32 bits ou ODBC para abrir a caixa de diálogo administrador de fonte de dados ODBC.  
  
3.  Clique em Adicionar.  
  
4.  Na caixa de diálogo Criar nova fonte de dados, selecione Microsoft Visual FoxPro driver e clique em concluir.  
  
5.  Na [caixa de diálogo configuração do ODBC do Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), digite o nome e a descrição da fonte de dados, selecione o tipo de banco de dado, selecione o banco de dados ou o diretório e clique em OK.  
  
     O novo nome da fonte de dados é exibido na lista fontes de dados do usuário na guia DSN do usuário da caixa de diálogo administrador de fonte de dados ODBC.  
  
6.  Clique em OK para salvar a nova fonte de dados e fechar a caixa de diálogo administrador de fonte de dados ODBC.
