---
title: Adicionando uma fonte de dados Visual FoxPro | Microsoft Docs
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
ms.openlocfilehash: 1fd0c0f929ca00b7cf731dc92f07f69b6503f884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307137"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Adicionar uma fonte de dados do Visual FoxPro
Para acessar os dados do Visual FoxPro do seu aplicativo, você deve ter uma fonte de dados. Você pode criar uma fonte de dados da seguinte forma:  
  
-   Em um aplicativo, como microsoft® Word, Microsoft Excel ou Microsoft Access, que usa drivers ODBC.  
  
-   Fora do seu aplicativo, usando o Microsoft Windows® 95, Microsoft Windows 98 ou Microsoft Windows NT®/Windows 2000 Control Panel.  
  
 Depois que uma fonte de dados existe em seu sistema, você pode reutilizar a mesma fonte de dados toda vez que quiser acessar os dados do Visual FoxPro. Se você tiver vários bancos de dados ou tabelas diferentes que deseja acessar, você pode criar uma fonte de dados separada para cada banco de dados ou diretório.  
  
 O procedimento a seguir cria uma fonte de dados usando o Painel de Controle. Para obter mais informações sobre como criar uma fonte de dados a partir de um aplicativo, consulte [Acessando os dados visuais foxpro do Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Para adicionar uma fonte de dados Visual FoxPro  
  
1.  Em computadores que estão executando o Windows 2000, abra o painel controle do Windows e clique duas vezes em Ferramentas Administrativas.  
  
2.  Clique duas vezes em Fontes de dados (ODBC) para abrir a caixa de diálogo Administrador de Origem de Dados ODBC. Este ícone está disponível depois de ter instalado o Driver Visual FoxPro ODBC ou qualquer software de driver ODBC.  
  
    > [!NOTE]  
    >  Se você estiver executando uma versão anterior do Windows, abra o painel Controle do Windows e clique duas vezes em ODBC ou ODBC de 32 bits para abrir a caixa de diálogo Administrador de Origem de Dados ODBC.  
  
3.  Clique em Adicionar.  
  
4.  Na caixa de diálogo Criar nova fonte de dados, selecione Microsoft Visual FoxPro Driver e clique em Concluir.  
  
5.  Na [caixa de diálogo Configuração Visual FoxPro do ODBC,](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)digite o nome e a descrição da fonte de dados, selecione o tipo de banco de dados, selecione o banco de dados ou diretório e clique em OK.  
  
     O novo nome de origem dos dados é exibido na lista Fontes de dados do usuário na guia DSN do usuário da caixa de diálogo Administrador de Origem de Dados oDBC.  
  
6.  Clique em OK para salvar a nova fonte de dados e feche a caixa de diálogo Administrador de Origem de Dados oDBC.
