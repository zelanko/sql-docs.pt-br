---
title: Importando dados do Visual FoxPro para Microsoft Access | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6bdf35fb9c9b7b4688aa7f5bf4173b2a6a9eefb5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importando dados do Visual FoxPro para Microsoft Access
Você pode importar dados armazenados em um banco de dados do Visual FoxPro para um banco de dados do Microsoft Access usando a opção de importação.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Para importar dados do Visual FoxPro para um banco de dados do Microsoft Access  
  
1.  Abra um banco de dados do Microsoft Access.  
  
2.  No menu Arquivo, escolha que obter dados externos, em seguida, importar.  
  
3.  Na caixa de diálogo de importação, selecione bancos de dados ODBC nos arquivos da lista de tipo.  
  
4.  Na caixa de diálogo fontes de dados do SQL, selecione a fonte de dados do Visual FoxPro que se conecta aos dados FoxPro que você deseja consultar e clique em Okey.  
  
5.  Na caixa de diálogo Importar objetos, selecione uma ou mais tabelas que você deseja importar e clique em Okey. Os nomes das tabelas do Visual FoxPro importados são exibidos na guia tabelas do banco de dados Microsoft Access.  
  
 Agora você pode usar o Microsoft Access para manipular os dados nas tabelas do Visual FoxPro importados. Os dados que você importar são um instantâneo dos dados armazenados no Visual FoxPro; as alterações feitas nos dados importados não são enviadas para a fonte de dados do Visual FoxPro.  
  
 Se você quiser que as alterações feitas no Microsoft Access para alterar os dados na fonte de dados do Visual FoxPro, consulte [consultar e atualizar Visual FoxPro dados do Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).

