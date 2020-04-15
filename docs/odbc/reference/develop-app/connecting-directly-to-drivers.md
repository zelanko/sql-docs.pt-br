---
title: Conectando diretamente aos motoristas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6aacb5d3df985949e04cdd47a9fe460cddbde6a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299076"
---
# <a name="connecting-directly-to-drivers"></a>Conectar-se diretamente a drivers
Como foi discutido na [escolha de uma fonte de dados ou driver,](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)no início desta seção, alguns aplicativos não querem usar uma fonte de dados. Em vez disso, eles querem se conectar diretamente a um motorista. **O SQLDriverConnect** fornece uma maneira de o aplicativo se conectar diretamente a um driver sem especificar uma fonte de dados. Conceitualmente, uma fonte de dados temporária é criada em tempo de execução.  
  
 Para se conectar diretamente a um driver, o aplicativo especifica a palavra-chave **DRIVER** na seqüência de conexões em vez da palavra-chave **DSN.** O valor da palavra-chave **DRIVER** é a descrição do driver como devolvido por **SQLDrivers**. Por exemplo, suponha que um driver tenha a descrição Paradox Driver e exija o nome de um diretório contendo os arquivos de dados. Para se conectar a este driver, o aplicativo pode usar qualquer uma das seguintes strings de conexão:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Com a primeira corda, o motorista não precisaria de nenhuma informação adicional. Com a segunda seqüência, o driver precisaria solicitar o nome do diretório contendo os arquivos de dados.
