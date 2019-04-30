---
title: Usando parâmetros de instrução | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- ODBC, parameters
- statements [ODBC], parameters
- parameter markers [ODBC]
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
ms.assetid: 2427d886-ec6c-49d7-b0b6-0d998b64cdb9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a16f070623503dcb17788bc75bd5695bc1584d7e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200250"
---
# <a name="using-statement-parameters"></a>Usando parâmetros de instrução
  Um parâmetro é uma variável em uma instrução SQL que pode permitir a aplicativo ODBC:  
  
-   Fornecer valores com eficiência para colunas em uma tabela.  
  
-   Aprimorar a interação do usuário na construção dos critérios de consulta.  
  
-   Gerencie **texto**, **ntext**, e **imagem** dados e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-tipos de dados C específicos.  
  
 Por exemplo, uma **partes** tabela tem colunas nomeadas **PartID**, **descrição**, e **preço**. Adicionar uma parte sem parâmetros exige a criação de uma instrução SQL como, por exemplo:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Embora essa instrução seja aceitável para inserir uma linha com um conjunto conhecido de valores, é estranho quando um aplicativo precisa inserir várias linhas. O ODBC resolve isso permitindo que um aplicativo substitua um valor de dados em uma instrução SQL por um marcador de parâmetro. Isto é indicado por um ponto de interrogação (?). No seguinte exemplo, três valores de dados com marcadores de parâmetro são substituídos:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Os marcadores de parâmetro são associados a variáveis do aplicativo. Para inserir uma nova linha, o aplicativo só precisa definir os valores das variáveis e executar a instrução. O driver recupera os valores atuais das variáveis e os envia para a fonte de dados. Caso a instrução seja executada várias vezes, o aplicativo pode tornar o processo até mesmo mais eficiente, preparando a instrução.  
  
 Cada marcador de parâmetro é referenciado por seu número ordinal atribuído aos parâmetros da esquerda para a direita. O marcador de parâmetro à esquerda em uma instrução SQL tem um valor ordinal igual a 1; o próximo é ordinal 2 e assim por diante.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Associando parâmetros](using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>Consulte também  
 [Executando consultas &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
