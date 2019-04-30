---
title: Instalando componentes ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5f033ac12569c7de61af071930d6c8d58d8b611
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198233"
---
# <a name="installing-odbc-components"></a>Instalar componentes ODBC
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, ODBC está incluído no sistema operacional Windows. Você deve instalar apenas explicitamente ODBC em versões anteriores do Windows.  
  
 Esta seção descreve como os componentes ODBC são instalados e removidos. Como os desenvolvedores de driver sempre instalar um componente ODBC (seu driver), eles precisam ler esta seção. Os desenvolvedores de aplicativos precisam ler esta seção somente se eles serão são fornecidos componentes ODBC com seus aplicativos. Componentes ODBC incluem o Gerenciador de Driver, drivers, conversores, a DLL do instalador, a biblioteca de cursores e todos os arquivos relacionados. Para os fins desta seção, os aplicativos ODBC não são considerados para ser componentes ODBC.  
  
> [!NOTE]  
>  Esta seção é específica para plataformas Microsoft Windows. Como os componentes ODBC são instalados em outras plataformas é específico da plataforma.  
  
 Componentes ODBC são instalados e removidos em uma base de componente a componente, não uma base por arquivo. Por exemplo, se um tradutor consiste o tradutor em si e um número de arquivos de dados, esses arquivos são instalados e removidos como um grupo; eles não devem ser instalados e removidos em uma base por arquivo. A razão para isso é para certificar-se de que os componentes completos só existem no sistema.  
  
 Para fins de instalação e remoção de componentes, a seguir é definidos para serem componentes ODBC:  
  
-   **Componentes principais.** O Gerenciador de Driver, biblioteca de cursores, DLL do instalador e qualquer outro relacionadas a arquivos compõem os principais componentes e devem ser instalados e removidos como um grupo.  
  
-   **Drivers.** Cada driver é um componente separado.  
  
-   **Tradutores.** Cada tradução é um componente separado.  
  
 Com o suporte de Unicode no ODBC 3.5 e versões posteriores, alguma consideração deve ser fornecida ao uso de componentes do OLE DB com ODBC. A versão 1.1 do OLE DB Provider for ODBC foi escrito para as especificações de Unicode específicas no ODBC 3.0. Como essas especificações alterado no ODBC 3.5, é necessário ter a versão 1.5 ou posterior do provedor ao usar o ODBC 3.5 e posterior. Esta seção contém os tópicos a seguir.  
  
-   [Componentes de instalação](../../../odbc/reference/install/installation-components.md)  
  
-   [Contagem de uso](../../../odbc/reference/install/usage-counting.md)
