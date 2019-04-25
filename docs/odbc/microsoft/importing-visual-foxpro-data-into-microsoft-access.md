---
title: Importando dados do Visual FoxPro para Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f19b58ba93c94088c4cae19f1093d89c8decb843
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471297"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importar dados do Visual FoxPro para Microsoft Access
Você pode importar os dados armazenados em um banco de dados do Visual FoxPro para um banco de dados do Microsoft Access usando a opção de importação.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Para importar dados do Visual FoxPro para um banco de dados do Microsoft Access  
  
1.  Abra um banco de dados do Microsoft Access.  
  
2.  No menu Arquivo, escolha que obter dados externos, em seguida, importar.  
  
3.  Na caixa de diálogo de importação, selecione os bancos de dados do ODBC nos arquivos da lista de tipos.  
  
4.  Na caixa de diálogo de fontes de dados SQL, selecione a fonte de dados do Visual FoxPro que se conecta aos dados FoxPro que você deseja consultar e clique em Okey.  
  
5.  Na caixa de diálogo Importar objetos, selecione uma ou mais tabelas que você deseja importar e clique em Okey. Os nomes das tabelas do Visual FoxPro importados são exibidos na guia de tabelas do banco de dados Microsoft Access.  
  
 Agora você pode usar o Microsoft Access para manipular os dados nas tabelas do Visual FoxPro importados. Dados importados por você são um instantâneo dos dados armazenados no Visual FoxPro; as alterações feitas aos dados importados não são enviadas para a fonte de dados do Visual FoxPro.  
  
 Se você quiser que as alterações feitas no Microsoft Access para alterar os dados na fonte de dados do Visual FoxPro, consulte [consultando e atualizando Visual FoxPro dados do Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
