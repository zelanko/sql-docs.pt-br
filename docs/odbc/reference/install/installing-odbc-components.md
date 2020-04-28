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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd0a6aeba8073ce14b08b8635396b1f231895fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298976"
---
# <a name="installing-odbc-components"></a>Instalar componentes ODBC
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 Esta seção descreve como os componentes ODBC são instalados e removidos. Como os desenvolvedores de driver sempre instalam um componente ODBC (seu driver), eles precisam ler esta seção. Os desenvolvedores de aplicativos precisarão ler esta seção somente se enviarem componentes ODBC com seus aplicativos. Os componentes ODBC incluem o Gerenciador de driver, Drivers, tradutores, a DLL do instalador, a biblioteca de cursores e todos os arquivos relacionados. Para os fins desta seção, os aplicativos ODBC não são considerados componentes ODBC.  
  
> [!NOTE]  
>  Esta seção é específica para plataformas Microsoft Windows. O modo como os componentes ODBC são instalados em outras plataformas é específico da plataforma.  
  
 Os componentes ODBC são instalados e removidos de componentes por componente, não uma base de arquivo por arquivo. Por exemplo, se um tradutor consistir no próprio tradutor e em um número de arquivos de dados, esses arquivos serão instalados e removidos como um grupo; Eles não devem ser instalados e removidos de acordo com o arquivo. O motivo disso é garantir que apenas os componentes completos existam no sistema.  
  
 Para fins de instalação e remoção de componentes, os seguintes são definidos para serem componentes ODBC:  
  
-   **Componentes principais.** O Gerenciador de driver, a biblioteca de cursores, a DLL do instalador e quaisquer outros arquivos relacionados compõem os componentes principais e devem ser instalados e removidos como um grupo.  
  
-   **Seus.** Cada driver é um componente separado.  
  
-   **Tradutores.** Cada tradutor é um componente separado.  
  
 Com o suporte do Unicode no ODBC 3,5 e posterior, é necessário considerar uma consideração para o uso de componentes OLE DB com o ODBC. A versão 1,1 do provedor de OLE DB para ODBC foi gravada em especificações Unicode específicas no ODBC 3,0. Como essas especificações foram alteradas no ODBC 3,5, é necessário ter a versão 1,5 ou posterior do provedor ao usar o ODBC 3,5 e posterior. Esta seção contém os seguintes tópicos.  
  
-   [Componentes de instalação](../../../odbc/reference/install/installation-components.md)  
  
-   [Contagem de uso](../../../odbc/reference/install/usage-counting.md)
