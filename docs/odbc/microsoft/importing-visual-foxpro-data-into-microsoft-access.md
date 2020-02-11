---
title: Importando dados do Visual FoxPro para o Microsoft Access | Microsoft Docs
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
ms.openlocfilehash: 557b5505b9eb6a15080a7d0495df2e63aefd2d76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085538"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importar dados do Visual FoxPro para Microsoft Access
Você pode importar os dados armazenados em um banco de dado do Visual FoxPro para um Microsoft Access usando a opção de importação.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Para importar dados do Visual FoxPro para um banco de dado do Microsoft Access  
  
1.  Abra um banco de dados do Microsoft Access.  
  
2.  No menu arquivo, escolha obter dados externos e importar.  
  
3.  Na caixa de diálogo Importar, selecione bancos de dados ODBC na lista arquivos do tipo.  
  
4.  Na caixa de diálogo fontes de dados do SQL, selecione a fonte de dados do Visual FoxPro que se conecta aos dados do FoxPro que você deseja consultar e clique em OK.  
  
5.  Na caixa de diálogo importar objetos, selecione uma ou mais tabelas que você deseja importar e clique em OK. Os nomes das tabelas do Visual FoxPro que você importou são exibidos na guia tabelas do banco de dados do Microsoft Access.  
  
 Agora você pode usar o Microsoft Access para manipular os dados nas tabelas importadas do Visual FoxPro. Os dados importados são um instantâneo dos dados armazenados no Visual FoxPro; as alterações feitas nos dados importados não são enviadas de volta para a fonte de dados do Visual FoxPro.  
  
 Se você quiser as alterações feitas no Microsoft Access para alterar os dados na fonte de dados do Visual FoxPro, consulte [consultando e atualizando dados do Visual FoxPro do Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
