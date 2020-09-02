---
description: O teste ODBC é um aplicativo habilitado para ODBC que você pode usar para testar drivers ODBC e o Gerenciador de driver ODBC.
title: Teste do ODBC
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC test [ODBC]
- ODBC drivers [ODBC], testing
- gtrtst32.dll
- gtrts32w.dll [ODBC]
- odbct32w.exe [ODBC]
- odbcte32.exe [ODBC]
- testing ODBC drivers [ODBC]
ms.assetid: 7f13894c-5697-436c-be3d-fe16e1a02325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39869fe1230be75d9a76e13b8ba3938ec31ee5ee
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288241"
---
# <a name="odbc-test"></a>Teste do ODBC

## <a name="about"></a>Sobre

O teste ODBC do Microsoft® é um aplicativo habilitado para ODBC que você pode usar para testar drivers ODBC e o ODBC Driver Manager. O teste ODBC é incluído como parte do [Microsoft Data Access Components (MDAC) 2,8 Software Development Kit](https://www.microsoft.com/download/details.aspx?id=21995).

O ODBC 3,51 inclui versões ANSI e habilitadas para Unicode do teste do ODBC. Os arquivos correspondentes são os seguintes:

- `Odbcte32.exe` e `Gtrtst32.dll` , para a versão ANSI.

- `Odbct32w.exe` e `Gtrts32w.dll` , para a versão Unicode.

Para usar o teste ODBC, você deve entender a API ODBC, a linguagem C e o SQL. Para obter mais informações sobre a API ODBC, consulte a [referência do programador de ODBC](../odbc/reference/odbc-programmer-s-reference.md).

Os tópicos de ajuda que foram incluídos anteriormente nesta seção da documentação agora estão contidos no programa de teste ODBC. Abra `Odbcte32.exe` `Odbct32w.exe` o ou o, abra o menu **ajuda** e clique em **Tópicos da ajuda**.

Observe que as versões de 64 bits desses aplicativos, destinadas a sistemas operacionais Microsoft Windows de 64 bits, têm os mesmos nomes que as versões de 32 bits, embora sejam arquivos separados. ou seja, o nome da versão Unicode da versão de 64 bits do teste do ODBC é `odbct32w.exe` .

## <a name="open-source"></a>Software livre

O teste ODBC é de software livre. Para exibir o código e criar a versão mais recente do teste do ODBC por conta própria, vá para o [repositório do GitHub para teste do ODBC](https://github.com/microsoft/ODBCTest).
