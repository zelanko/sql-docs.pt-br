---
title: Adicionando uma fonte de dados do Visual FoxPro | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d158cf38e5755e0e443d6cb47e4053bd05d45287
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="adding-a-visual-foxpro-data-source"></a>Adicionando uma fonte de dados do Visual FoxPro
Para acessar dados do Visual FoxPro do seu aplicativo, você deve ter uma fonte de dados. Você pode criar uma fonte de dados da seguinte maneira:  
  
-   Em um aplicativo, como o Microsoft® Word, Microsoft Excel ou Microsoft Access, que usa os drivers ODBC.  
  
-   Fora de seu aplicativo, usando o Microsoft Windows® 95, Microsoft Windows 98 ou painel de controle do Microsoft Windows/Windows 2000.  
  
 Depois de uma fonte de dados existe em seu sistema, você pode reutilizar a mesma fonte de dados sempre que você deseja acessar dados do Visual FoxPro. Se você tiver vários bancos de dados diferentes ou tabelas que você deseja acessar, você pode criar uma fonte de dados separado para cada banco de dados ou diretório.  
  
 O procedimento a seguir cria uma fonte de dados usando o painel de controle. Para obter mais informações sobre como criar uma fonte de dados de um aplicativo, consulte [acessando Visual FoxPro dados do Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Para adicionar uma fonte de dados do Visual FoxPro  
  
1.  Em computadores que executam o Windows 2000, abra o painel de controle do Windows e clique duas vezes em Ferramentas administrativas.  
  
2.  Clique duas vezes em fontes de dados (ODBC) para abrir a caixa de diálogo Administrador de fonte de dados ODBC. Esse ícone está disponível depois que você instalou o Driver de ODBC do Visual FoxPro ou qualquer software de driver ODBC.  
  
    > [!NOTE]  
    >  Se você estiver executando uma versão anterior do Windows, abra o painel de controle do Windows e clique duas vezes em 32 bits ODBC ou ODBC para abrir a caixa de diálogo Administrador de fonte de dados ODBC.  
  
3.  Clique em Adicionar.  
  
4.  Na caixa de diálogo Criar nova fonte de dados, selecione o Driver do Microsoft Visual FoxPro e, em seguida, clique em Concluir.  
  
5.  No [caixa de diálogo a instalação do Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), digite o nome da fonte de dados e a descrição, selecione o tipo de banco de dados, selecione o banco de dados ou diretório e clique em Okey.  
  
     O novo nome de fonte de dados é exibido na lista de fontes de dados do usuário na guia DSN de usuário da caixa de diálogo Administrador de fonte de dados ODBC.  
  
6.  Clique em Okey para salvar a nova fonte de dados e fechar a caixa de diálogo Administrador de fonte de dados ODBC.

