---
title: Subchaves de especificação do tradutor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad21943c5313edcb09aba88d45ea21132aa9757f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296036"
---
# <a name="translator-specification-subkeys"></a>Subchaves de especificação do conversor
Cada tradutor listado na subchave ODBC Translators tem uma subchave própria. Esta subchave tem o mesmo nome do valor correspondente sob a sub-chave ODBC Translators. Os valores sob esta subchave listam os caminhos completos das DLLs de configuração do tradutor e do tradutor e da contagem de uso. Os formatos dos valores são mostrados na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|Tradutor|REG_SZ|*tradutor-DLL-caminho*|  
|Instalação|REG_SZ|*setup-DLL-path*|  
|Contagem de usos|REG_DWORD|*contagem*|  
  
 Para obter informações sobre contagem de uso, consulte [Contagem de uso](../../../odbc/reference/install/usage-counting.md) anteriormente nesta seção.  
  
 Os aplicativos não devem definir a contagem de uso. A ODBC manterá essa contagem.  
  
 Por exemplo, suponha que o Microsoft Code Page Translator tenha uma DLL de tradução chamada Mscpxl32.dll, que as funções de configuração do tradutor estão na mesma DLL e que o tradutor foi instalado três vezes. Os valores sob a sub-chave do Microsoft Code Page Translator podem ser os seguintes:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
