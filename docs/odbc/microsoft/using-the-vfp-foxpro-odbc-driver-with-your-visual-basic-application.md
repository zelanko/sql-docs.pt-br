---
title: Use o driver VFP FoxPro ODBC com seu aplicativo visual básico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 871c392166fa2f5726e6f9e8651bf758dc144a00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292696"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Usar o Driver ODBC do VFP FoxPro com seu aplicativo Visual Basic
O aplicativo ® Visual Basic® da Microsoft pode se comunicar com os dados do Visual FoxPro criando um controle de dados que se conecta a uma fonte de dados Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Para conectar-se aos dados do Visual FoxPro usando o Controle de Dados no Visual Basic  
  
1.  Crie uma fonte de dados chamada "teste" que se conecta ao banco de dados de amostras TasTrade incluído no Visual FoxPro. A instalação padrão do Visual FoxPro coloca o banco de dados de amostras TasTrade no local:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  No Visual Basic, crie um novo formulário e coloque uma caixa de texto e um controle de dados sobre ele.  
  
3.  Alterar a propriedade Connect do controle de dados da seguinte forma:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Altere a propriedade RecordsetType para o seguinte:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Altere a propriedade RecordSource para o seguinte:  
  
    ```  
    customer  
    ```  
  
6.  Altere a propriedade DataSource para a caixa de texto para o nome padrão do controle De dados para o seguinte:  
  
    ```  
    data1  
    ```  
  
7.  Altere a propriedade DataField da caixa de texto para o seguinte:  
  
    ```  
    customer_id  
    ```  
  
8.  Execute o formulário e use o controle de dados para pular os campos de id do cliente a partir do banco de dados de amostras Visual FoxPro TasTrade.
