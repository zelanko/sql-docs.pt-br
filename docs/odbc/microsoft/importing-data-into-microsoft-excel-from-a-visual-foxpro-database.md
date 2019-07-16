---
title: Importar dados para o Microsoft Excel a partir de um banco de dados do Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c65635132c5f98b0565391122877f2e3c0a6714
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085556"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importar dados para o Microsoft Excel de um banco de dados do Visual FoxPro
Você pode importar dados do Visual FoxPro em sua planilha do Microsoft Excel, se você tiver definido uma fonte de dados para ele. Para obter informações sobre como criar uma fonte de dados do Visual FoxPro, consulte [acessar uma fonte de dados Visual FoxPro do Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Para importar dados do Visual FoxPro para uma planilha do Microsoft Excel  
  
1.  Abra uma planilha do Microsoft Excel.  
  
2.  No menu de dados, escolha obter dados externos. Microsoft Query é aberto.  
  
3.  Na caixa de diálogo Selecionar fonte de dados, selecione uma fonte de dados do Visual FoxPro e, em seguida, clique em usar.  
  
4.  Se o banco de dados acessado por sua fonte de dados incluir tabelas, selecione uma tabela da caixa de diálogo Adicionar tabelas. Microsoft Query exibe a tabela adicionada na metade superior do designer de consulta.  
  
    > [!NOTE]  
    >  A lista de proprietários não está disponível na caixa de diálogo porque o driver não oferece suporte para os proprietários. A lista de banco de dados não está disponível porque o driver não oferece suporte a vários bancos de dados em uma fonte de dados.  
  
5.  Selecione campos para a sua consulta arrastando-os da tabela para a inferior metade do designer.  
  
6.  Feche o Microsoft Query. Os dados que você selecionou são importados na sua planilha do Microsoft Excel.
