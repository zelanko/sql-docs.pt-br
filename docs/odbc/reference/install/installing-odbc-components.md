---
title: Instalando componentes ODBC | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 26592f5fdc0be2a5e5b9dc35945d07ec2ef3c101
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="installing-odbc-components"></a>Instalar os componentes ODBC
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 Esta seção descreve como os componentes ODBC são instalados e removidos. Como os desenvolvedores de driver sempre instalar um componente do ODBC (seu driver), eles precisam ler esta seção. Os desenvolvedores de aplicativos precisam ler esta seção somente se eles fornecerá componentes ODBC com seus aplicativos. Componentes ODBC incluem o Gerenciador de Driver, drivers, tradutores, o DLL do instalador, a biblioteca de cursores e todos os arquivos relacionados. Para os fins desta seção, os aplicativos ODBC não são considerados componentes ODBC.  
  
> [!NOTE]  
>  Esta seção é específica para plataformas Microsoft Windows. Como os componentes ODBC são instalados em outras plataformas é específica da plataforma.  
  
 Componentes ODBC são instalados e removidos em uma base por componente, não uma base por arquivo. Por exemplo, se um conversor consiste o tradutor de si mesmo e um número de arquivos de dados, esses arquivos são instalados e removidos como um grupo. eles não devem ser instalados e removidos em uma base por arquivo. A razão para isso é certificar-se de que apenas completos componentes existem no sistema.  
  
 Para fins de instalação e remoção de componentes, a seguir é definidos para serem componentes ODBC:  
  
-   **Componentes principais.** O Gerenciador de Driver, biblioteca de cursores, instalador DLL e qualquer outro relacionam arquivos compõem os principais componentes e devem ser instalados e removidos como um grupo.  
  
-   **Drivers.** Cada driver é um componente separado.  
  
-   **Tradutores.** Tradutor é um componente separado.  
  
 Com o suporte de Unicode no ODBC 3.5 e versões posteriores, alguma consideração deve ser dada à usando componentes de OLE DB com ODBC. A versão 1.1 do provedor OLE DB para ODBC foi escrita em especificações de Unicode específicas no ODBC 3.0. Como essas especificações alterado no ODBC 3.5, é necessário ter a versão 1.5 ou posterior do provedor ao usar o ODBC 3.5 e versões posteriores. Esta seção contém os tópicos a seguir.  
  
-   [Componentes de instalação](../../../odbc/reference/install/installation-components.md)  
  
-   [Contagem de uso](../../../odbc/reference/install/usage-counting.md)
